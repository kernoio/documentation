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
{% endtabs %}
