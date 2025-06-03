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

{% hint style="warning" %}
We're currently aware of compatibility issues with Docker on Apple M4 machines. For now, if you're installing Kerno using Docker, please use a Mac with an Intel, M1, M2, or M3 chip. We're actively working on a fix and will share updates soon.
{% endhint %}

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

{% hint style="info" %}
Your `<API-key>` is automatically generated when you create your account. Each account has a single key, so store it securely.
{% endhint %}

If you encounter issues or have questions, [message us on Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA), and we’ll gladly help.
