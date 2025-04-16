---
description: Learn how to install Kerno on your Kubernetes cluster
---

# Install Kerno

{% hint style="warning" %}
We're currently aware of compatibility issues with Docker on Apple M4 machines. For now, if you're installing Kerno using Docker, please use a Mac with an Intel, M1, M2, or M3 chip. We're actively working on a fix and will share updates soon.
{% endhint %}

{% hint style="info" %}
To install Kerno on your cluster, you will need your invite code. You can request an invite code [here](https://forms.gle/ZpoXJv5YjdGXRYH26).
{% endhint %}

Go to [app.kerno.io](https://app.kerno.io/?origin=docs), sign up using your email address, and follow the onboarding instructions.

{% tabs %}
{% tab title="Install on AWS" %}
### **Prerequisites**

1. **AWS Login**: Log into AWS with admin privileges.
2.  **OIDC (OpenID Connect) Provider**

    An [OIDC Provider](https://docs.aws.amazon.com/eks/latest/userguide/enable-iam-roles-for-service-accounts.html) is required for your EKS cluster to support Kerno’s functionality. This is typically configured for EKS clusters. Since the OIDC Provider can be used for multiple services, including Kerno, we recommend you manage it within your cluster setup.

    * [Set Up OIDC Provider on EKS »](https://docs.aws.amazon.com/eks/latest/userguide/enable-iam-roles-for-service-accounts.html)

Depending on whether you have set your AWS credentials as environment variables or in the `.aws/credentials` Use one of the following methods:

#### **Using AWS Config File**

Set your AWS Credentials as environment variables, add the missing values to the script, and run the script.

<figure><img src="../.gitbook/assets/Screenshot 2025-02-17 at 20.27.16 (1).png" alt=""><figcaption><p>Install Kerno Using AWS Config File</p></figcaption></figure>

{% hint style="info" %}
Your `<k4-key>` is automatically generated when you create your account. Each account has a single key, so store it securely.
{% endhint %}

#### **Using Environment Variables**

Set your AWS Credentials as environment variables, add the missing values to the script, and run the script.

<figure><img src="../.gitbook/assets/Screenshot 2025-02-17 at 20.27.33 (1).png" alt=""><figcaption><p>Install Kerno Using Environment Variables</p></figcaption></figure>

If you encounter issues or have questions, [message us on Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA), and we’ll gladly help.
{% endtab %}

{% tab title="Install on GCP" %}
### Installing Kerno

1. To install, a gcloud login must be present on the host machine
2. Log into GCP with admin privileges.
3. Add the missing values to the script, and run the script.

<figure><img src="../.gitbook/assets/Kerno GCP Installation.png" alt=""><figcaption><p>Kerno GCP Installation</p></figcaption></figure>

{% hint style="info" %}
Your `<API-key>` is automatically generated when you create your account. Each account has a single key, so store it securely.
{% endhint %}

If you encounter issues or have questions, [message us on Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA), and we’ll gladly help.
{% endtab %}

{% tab title="K8s-Only Mode" %}
### How it works <a href="#user-content-how-it-works" id="user-content-how-it-works"></a>

Kerno’s K**8s-only installation mode** is cloud-agnostic and does **not include managed object storage** by default. This means:

* **Logs, payloads, and stack traces are not stored persistently.**
* Temporary samples are written to the main container of the `nanobe` deployment, at `/tmp/samples`.
*   These samples are stored in **ephemeral storage**, which is automatically cleaned up by the container runtime. By default, the ephemeral storage is configured with the following limits:

    ```yaml
    resources:
      requests:
        ephemeral-storage: "2Gi"
      limits:
        ephemeral-storage: "4Gi"
    ```

When the container reaches the **4Gi limit**, older data is automatically **overwritten** to make room for new samples. This ensures the container doesn’t exceed its storage quota, but it also means that sample data is **not guaranteed to persist** over time.

{% hint style="info" %}
> We're working on an option to let you connect your own cloud storage (like AWS S3) for persistent storage.
{% endhint %}

Kerno still sends a limited set of **non-PII metrics** to our backend, including:

* **Resource usage**: CPU and memory stats for Pods and Nodes
* **Request metrics**: Service-to-service request activity
* **Kubernetes metadata**: Pods, Namespaces, DaemonSets, etc.
* **Kubernetes events**: Scheduling, restarts, failures, etc.

### Requirements <a href="#user-content-requirements" id="user-content-requirements"></a>

* Access to a Kubernetes cluster.
* Cloud provider credentials mounted into the container. This is necessary because `kubectl` often requires access tokens retrieved through cloud SDKs or CLIs, which in turn depend on local credentials.

### Docker Installation <a href="#user-content-docker-installation" id="user-content-docker-installation"></a>

```bash
docker run -it --pull always \
  -e API_KEY=<kerno-api-key> \
  -v ~/.config/gcloud:/root/.config/gcloud \   # Cloud-specific credentials (GCP)
  -v ~/.kube/config:/root/.kube/config \
  public.ecr.aws/fyck.io/installer-kubernetes:main
```

{% hint style="warning" %}
Ensure you mount the correct path for your cloud credentials: - **AWS:** `-v ~/.aws:/root/.aws` - **Azure:** `-v ~/.azure:/root/.azure` - **GCP:** `-v ~/.config/gcloud:/root/.config/gcloud`
{% endhint %}

The cloud credential mount can be omitted if accessing the cluster does not require cloud credentials (e.g., via static kubeconfig).

### Uninstalling Kerno via Docker <a href="#user-content-uninstalling-kerno-via-docker" id="user-content-uninstalling-kerno-via-docker"></a>

```bash
docker run -it --pull always \
  -e API_KEY=<kerno-api-key> \
  -e UNINSTALL=true \
  -v ~/.config/gcloud:/root/.config/gcloud \   # Cloud-specific credentials (GCP)
  -v ~/.kube/config:/root/.kube/config \
  public.ecr.aws/fyck.io/installer-kubernetes:main
```

### Installing via  YAML Manifest <a href="#user-content-installing-via-manifest-yaml" id="user-content-installing-via-manifest-yaml"></a>

#### Download the manifest:

```bash
curl -H "x-kerno-api-key: <kerno-api-key>" \
     -o kerno-installation.yaml \
     https://ingestion.kerno.io/k8s-bridge/installation/yaml
```

{% hint style="warning" %}
The manifest contains sensitive information an auth token to be stored as a secret, an installation id so Kerno can uniquely identify the installation, and the API key.
{% endhint %}

{% hint style="info" %}
For development environments, add the environment variable `ENVIRONMENT=development` to the Docker command.
{% endhint %}

Apply the manifest:

```bash
kubectl apply -f kerno-installation.yaml
```

Alternatively, download and apply in a single step:

```bash
curl -H "x-kerno-api-key: <kerno-api-key>" \
     -o kerno-installation.yaml \
     https://ingestion.kerno.io/k8s-bridge/installation/yaml && \
kubectl apply -f kerno-installation.yaml
```

{% hint style="info" %}
For development installations, use the URL: [`https://ingestion.dev.kerno.io/k8s-bridge/installation/yaml`](https://ingestion.dev.kerno.io/k8s-bridge/installation/yaml).
{% endhint %}

### Uninstalling Kerno via YAML Manifest <a href="#user-content-uninstalling-kerno" id="user-content-uninstalling-kerno"></a>

To uninstall:

*   With the manifest in your present working directory:

    ```bash
    kubectl delete -f kerno-installation.yaml
    ```
*   Or remove the entire namespace:

    ```bash
    kubectl delete namespace kerno
    ```
{% endtab %}
{% endtabs %}
