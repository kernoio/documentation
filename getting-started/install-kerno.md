---
description: Learn how to install Kerno on your Kubernetes cluster
---

# Install Kerno

Before installing Kerno, please make sure you meet the [requirements](system-requirements.md).

## Sign up to Kerno

The first step is to go to [app.kerno.io](https://app.kerno.io/?origin=docs), sign up using your email address, and follow the onboarding instructions.

When installing Kerno for the first time, you'll be asked to create an organization.

Enter your organization's name, then click **Create Organization** to proceed.

<figure><img src="../.gitbook/assets/Create Orgnization.png" alt=""><figcaption><p>Create an Organization</p></figcaption></figure>

{% hint style="info" %}
**Note**: The organization name will also be used to generate a unique slug (URL identifier) for your organization within Kerno. You can edit your organization's name and URL later.
{% endhint %}

Once your organization is set up, you'll be prompted to register a cluster where Kerno will run.

Enter a name for your cluster. This is how it will appear inside Kerno.

Then click **Register Cluster** to continue.

<figure><img src="../.gitbook/assets/Register Your Cluster.png" alt=""><figcaption><p>Register a Cluster</p></figcaption></figure>

{% hint style="info" %}
**Note**: You can edit your cluster name later.
{% endhint %}

{% hint style="warning" %}
**IMPORTANT**

Your \<API-key> is automatically generated when you install Kerno on a new Cluster. You will have one API Key per cluster. You'll need these key to update and delete Kerno. So make sure you store then securely
{% endhint %}

## Install Kerno Using Helm

You can install Kerno using the official Helm chart.

### **Step 1. Add the Helm Repository**

```bash
helm repo add kerno https://kernoio.github.io/helm-charts
```

### **Step 2.** Install the chart

Replace `<KERNO_API_KEY>` with your API key:

```bash
helm install kerno-agent kerno/agent \
  --create-namespace \
  --namespace kerno \
  --set apiKey="<KERNO_API_KEY>"
```

### **Step 3. Connect your Object Storage**

Kerno stores sensitive data, including logs and traces, inside your AWS accounts and GCP projects within an Object Store. Below are the steps to create and configure access to an object storage resource.

{% hint style="info" %}
If you don't connect an Object Store,  **Logs, payloads, and traces will be** written to the main container of the `nanobe` deployment, at `/tmp/samples`.

These samples are stored in **ephemeral storage**, which is automatically cleaned up by the container runtime. By default, the ephemeral storage is configured with the following limits:

```yaml
resources:
  requests:
    ephemeral-storage: "2Gi"
  limits:
    ephemeral-storage: "4Gi"
```

When the container reaches the **4Gi limit**, older data is automatically **overwritten** to make room for new samples. This ensures the container doesn’t exceed its storage quota, but it also means that sample data is **not guaranteed to persist** over time.
{% endhint %}

{% tabs %}
{% tab title="AWS S3 Bucket" %}
**Step 1. Create an S3 Bucket**

Create a bucket in S3 and note the name. This bucket will be used to store Kerno logs and traces.

**Step 2. Set Up IAM Role for EKS Access**

Create an IAM role that your EKS cluster can assume via its OIDC provider:

* **Trusted Entity Type**: Web Identity
* **Identity Provider**: Use your cluster's OIDC URL
* **Audience**: `sts.amazonaws.com`
* **Condition**:
  * **Key**: `<oidc-url>:sub`
  * **Operator**: `StringLike`
  * **Value**: `system:serviceaccount:kerno:*`

**Trust Policy Example**

Replace placeholders with your  values:

```bash
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Federated": "arn:aws:iam::<account-id>:oidc-provider/<oidc-provider-url-https-prefix-removed>"
      },
      "Action": "sts:AssumeRoleWithWebIdentity",
      "Condition": {
        "StringLike": {
          "<oidc-provider-url>:sub": "system:serviceaccount:kerno:*"
        },
        "StringEquals": {
          "<oidc-provider-url>:aud": "sts.amazonaws.com"
        }
      }
    }
  ]
}
```

**Step 3. Attach Permissions to the IAM Role**

Attach an inline policy granting access to the bucket:

```bash
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:*"],
      "Resource": [
        "arn:aws:s3:::<bucket-name>",
        "arn:aws:s3:::<bucket-name>/*"
      ]
    }
  ]
}
```

**Step 4. Update the Bucket Policy**

Allow the IAM role access to the bucket using the role arn from step 2:

```bash
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "<role-arn>"
      },
      "Action": "s3:*",
      "Resource": [
        "arn:aws:s3:::<bucket-name>",
        "arn:aws:s3:::<bucket-name>/*"
      ]
    }
  ]
}
```

**Step 5. Update `values.yaml`**

Set the following values in your `values.yaml`:

```bash
cloud: AWS
bucketName: <bucket-name>
serviceAccountAnnotations:
  eks.amazonaws.com/role-arn: <role-arn>
```

replacing `<bucket-name>` and `<role-arn>`.

An example can be found in `examples/aws-values.yaml`.

**Step 6. Install the Chart Using Your Config**

```bash
helm install kerno-agent kerno/agent \
  --create-namespace \
  --namespace kerno \
  -f path/to/values.yaml
```

{% hint style="warning" %}
_**IMPORTANT**_

Commit your `values.yaml` file to version control so it can be reused during upgrades.

Make sure to keep your API key secret by storing it securely outside of the file.
{% endhint %}
{% endtab %}

{% tab title="GCP Cloud Storage" %}
**Prerequisites**

* Ensure that **Workload Identity Federation** is enabled on the cluster.
* Enable the **GKE Metadata Server** on at least one node pool.

**Step 1. Create a Google Service Account**

In the GCP project, create a Service Account, noting its email address.

**Step 2. Allow Workload Identity Access to the Service Account**

1. Navigate to the Service Account in the IAM console.
2. Click **"Grant Access"**.
3. Add the following principal: `<project-id>.svc.id.goog[kerno/kerno-sa]`, replacing `<project-id>` with the GCP project id.
4. Select the `Service Account Admin` role.
5. Save the configuration.

**Step 3. Create a Cloud Storage Bucket**

Create a bucket in the same GCP project as the GKE cluster.

**Step 4. Grant the Service Account Access to the Bucket**

1. Navigate to the Cloud Storage bucket.
2. Click **"Grant Access"**.
3. For **Principal**, enter the Service Account's email.
4. For **Role**, select `Storage Admin`.
5. Save the changes.

**Step 5. Configure Helm Chart Values**

Update your `values.yaml` with the following content:

```
cloud: GCP
bucketName: <bucket-name>
serviceAccountAnnotations:
  iam.gke.io/gcp-service-account: <service-account-email>
```

replacing `<bucket-name>` and `<service-account-email>`.

An example can be found in `examples/gcp-values.yaml`.

#### 6. Install the Chart Using Your Config

```
helm install kerno-agent kerno/agent \
  --create-namespace \
  --namespace kerno \
  -f path/to/values.yaml
```

{% hint style="warning" %}
_**IMPORTANT**_

Commit your `values.yaml` file to version control so it can be reused during upgrades.

Make sure to keep your API key secret by storing it securely outside of the file.
{% endhint %}
{% endtab %}
{% endtabs %}

## Install Kerno Using Docker

Use the Kerno Docker to automate the installation process. The key benefit of this method is that **Kerno will automatically provision the required object storage and apply the correct roles and access policies for you.**&#x20;

### Prerequisites

#### **Kubernetes RBAC Permissions**

You'll need permission to deploy the following Kubernetes objects.

* **Namespace**
* **Deployment**&#x20;
* **DaemonSet**
* **ConfigMap**
* **Secret**&#x20;
* **Service**
* **ServiceAccount**
* **ClusterRole**
* **ClusterRoleBinding**

#### **Cloud Permissions**

You'll need the following permission for your cloud account:

* **IAM Role**
* **Role Policy**
* **Bucket**
* **Bucket Policy**

### **Install on AWS**

#### Step 1. Log into AWS with admin privileges.

**OIDC (OpenID Connect) Provider**

An [OIDC Provider](https://docs.aws.amazon.com/eks/latest/userguide/enable-iam-roles-for-service-accounts.html) is required for your EKS cluster to support Kerno’s functionality. This is typically configured for EKS clusters. Since the OIDC Provider can be used for multiple services, including Kerno, we recommend you manage it within your cluster setup.

* [Set Up OIDC Provider on EKS »](https://docs.aws.amazon.com/eks/latest/userguide/enable-iam-roles-for-service-accounts.html)

Depending on whether you have set your AWS credentials as environment variables or in the `.aws/credentials` Use one of the following methods:

#### Step 2 \[Option 1]. **Install Using AWS Config File**

Set your AWS Credentials as environment variables, add the missing values to the script, and run the script.

<figure><img src="../.gitbook/assets/Screenshot 2025-02-17 at 20.27.16 (1).png" alt=""><figcaption><p>Install Kerno Using AWS Config File</p></figcaption></figure>

{% hint style="info" %}
Your `<k4-key>` is automatically generated when you create your account. Each account has a single key, so store it securely.
{% endhint %}

#### Step 2 \[Option 2]. **Using Environment Variables**

Set your AWS Credentials as environment variables, add the missing values to the script, and run the script.

<figure><img src="../.gitbook/assets/Screenshot 2025-02-17 at 20.27.33 (1).png" alt=""><figcaption><p>Install Kerno Using Environment Variables</p></figcaption></figure>

### Install on GCP

#### Step 1. Log into GCP with admin privileges.

{% hint style="info" %}
To install, a gcloud login must be present on the host machine
{% endhint %}

#### Step 2. Add the missing values to the script, and run the script.

<figure><img src="../.gitbook/assets/Kerno GCP Installation.png" alt=""><figcaption><p>Kerno GCP Installation</p></figcaption></figure>

If you encounter issues or have questions, [message us on Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA), and we’ll gladly help.

## Upgrade Kerno

Uninstall Kerno using the same method you used to install it (e.g., Helm, Docker)

{% tabs %}
{% tab title="Helm" %}
```bash
helm upgrade --install kerno-agent kerno-dev/agent
--create-namespace
--namespace kerno
--set apiKey="<KERNO_API_KEY>"
--atomic
```
{% endtab %}

{% tab title="Docker" %}
To upgrade using Docker, run the same command you used to install Kerno.
{% endtab %}
{% endtabs %}

## Uninstall Kerno

Uninstall Kerno using the same method you used to install it (e.g., Helm, Docker). Just run the corresponding uninstall command.

{% tabs %}
{% tab title="Helm" %}
```
helm uninstall kerno-agent -n kerno
```
{% endtab %}

{% tab title="Docker" %}
To uninstall using Docker, run the same command you used to install Kerno, but add the uninstall flag.

```shell
-e UNINSTALL=true \
```
{% endtab %}
{% endtabs %}

## Troubleshoot your Installation.

These are some issues you might encounter when installing Kerno and how you can fix them.

<details>

<summary>Docker doesn't have enough memory</summary>

If your Docker doesn't have enough memory to install Kerno, you'll see the following error.

```bash
docker run -it --pull always \
-e AWS_REGION=<region> \
-e AWS_PROFILE=<profile> \
-e CLUSTER_NAME=<cluster_name> \
-e K4_KEY=<kerno_api_key> \
-v ~/.aws:/root/.aws \
public.ecr.aws/fyck.io/installer:main


main: Pulling from fyck.io/installer
Digest: sha256:ac79ed7e599bea1bec142fe418a1f1081787b3f537182d02eb35939f8c48d890
Status: Image is up to date for public.ecr.aws/fyck.io/installer:main
INFO: Installation target set to production
Interactive mode detected. Confirmation prompts will be used

Getting installation information from Kerno...
Installation information obtained

Setting Kubernetes context...
Using AWS_REGION [<profile>] and CLUSTER_NAME [<cluster_name>] to set context

Initializing Pulumi stack for Kerno installation...

/entrypoint.sh: line 114:    36 Segmentation fault      pulumi stack select -c "$K4_ID"b
```

**To resolve this issue:**

1. Open **Docker Desktop**
2. Go to **Settings**, then **Resources**
3. Increase the allocated memory (add 2–4 GB, depending on your workload)

**If the issue continues:**

1. Remove all containers created from the installer image
2. Delete the installer image
3. Re-run the installation command

</details>

<details>

<summary>Cloud profile isn't being detected</summary>

If you see an error like the one below, it means the selected profile cannot be used to connect to the cluster.

```bash

Diagnostics:
  pulumi:pulumi:Stack (installer-ab90fbbe-4d72-45ca-a2a7-ecaf8d9bf667):
    error: preview failed

  aws:s3:BucketV2 (kerno-samples-ab90fbbe-4d72-45ca-a2a7-ecaf8d9bf667):
    error: Preview failed: 1 error occurred:
    	* Retrieving AWS account details: validating provider credentials: retrieving caller identity from STS: operation error STS: GetCallerIdentity, https response error StatusCode: 403, RequestID: ebbb0a6a-494e-4e36-ab5c-bef7d6978b3b, api error InvalidClientTokenId: The security token included in the request is invalid

  aws:s3:BucketPolicy (kerno-samples-ab90fbbe-4d72-45ca-a2a7-ecaf8d9bf667-policy):
    error: Preview failed: 1 error occurred:
    	* Retrieving AWS account details: validating provider credentials: retrieving caller identity from STS: operation error STS: GetCallerIdentity, https response error StatusCode: 403, RequestID: ebbb0a6a-494e-4e36-ab5c-bef7d6978b3b, api error InvalidClientTokenId: The security token included in the request is invalid

  aws:iam:Role (kerno-samples-role-ab90fbbe-4d72-45ca-a2a7-ecaf8d9bf667):
    error: Preview failed: 1 error occurred:
    	* Retrieving AWS account details: validating provider credentials: retrieving caller identity from STS: operation error STS: GetCallerIdentity, https response error StatusCode: 403, RequestID: ebbb0a6a-494e-4e36-ab5c-bef7d6978b3b, api error InvalidClientTokenId: The security token included in the request is invalid

  aws:iam:RolePolicy (kerno-samples-ab90fbbe-4d72-45ca-a2a7-ecaf8d9bf667-policy):
    error: Preview failed: 1 error occurred:
    	* Retrieving AWS account details: validating provider credentials: retrieving caller identity from STS: operation error STS: GetCallerIdentity, https response error StatusCode: 403, RequestID: ebbb0a6a-494e-4e36-ab5c-bef7d6978b3b, api error InvalidClientTokenId: The security token included in the request is invalid

    [Pulumi Copilot] Would you like help with these diagnostics?
    https://app.pulumi.com/kernoio/installer/ab90fbbe-4d72-45ca-a2a7-ecaf8d9bf667/previews/bf99205d-b0f9-4991-a392-bbd95dd9b782?explainFailure

Resources:

There was a problem installing Kerno.
Please check your installation configuration and try again.
Should the issue persist, contact the Kerno team for support.
```

To resolve this issue, make sure you are using the correct profile:

1.  Run:

    ```bash
    aws sso login --profile <profile>
    ```
2.  If the issue persists, try using `assume` to get credentials:

    ```bash
    assume --export <profile>

    ```

</details>

<details>

<summary>MacOS M4 Installation Issue</summary>

If you're using Docker on Apple M4 machines, you may encounter an error that looks like this:

```bash

Diagnostics:
  pulumi:pulumi:Stack (installer-36755439-d238-44cd-b3d6-d7384e54ad73):
    #
    # A fatal error has been detected by the Java Runtime Environment:
    #
    #  SIGILL (0x4) at pc=0x0000ffff9633fc5c, pid=132, tid=133
    #
    # JRE version:  (21.0.6+7) (build )
    # Java VM: OpenJDK 64-Bit Server VM (21.0.6+7-LTS, mixed mode, sharing, tiered, compressed oops, compressed class ptrs, g1 gc, linux-aarch64)
    # Problematic frame:
    # j  java.lang.System.registerNatives()V+0 java.base@21.0.6
    #
    # No core dump will be written. Core dumps have been disabled. To enable core dumping, try "ulimit -c unlimited" before starting Java again
    #
    # An error report file with more information is saved as:
    # /pulumi/projects/hs_err_pid132.log
    [0.038s][warning][os] Loading hsdis library failed
    #
    # The crash happened outside the Java Virtual Machine in native code.
    # See problematic frame for where to report the bug.
    #

    error: an unhandled error occurred: '/opt/java/openjdk/bin/java -jar installer.jar' exited with non-zero exit code: -1

    [Pulumi Copilot] Would you like help with these diagnostics?
    https://app.pulumi.com/kernoio/installer/36755439-d238-44cd-b3d6-d7384e54ad73/previews/b1ef6df2-ad48-4219-acec-448f6bcaa863?explainFailure

```

To resolve this issue, first make sure you have the latest version of Docker and Docker Desktop installed. Then, try rerunning the command.

If the issue persists, add the following environment variable to the Kerno installation script and rerun it:

```bash
-e JAVA_TOOL_OPTIONS="-XX:UseSVE=0"
```

</details>
