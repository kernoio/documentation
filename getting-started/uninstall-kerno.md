---
description: Learn how to uninstall Kerno.
---

# Uninstall Kerno

Follow these steps to uninstall a cluster from Kerno.

{% hint style="info" %}
If you installed Kerno in K8s-only mode, follow the uninstall steps for [Docker](install-kerno.md#user-content-uninstalling-kerno-via-docker) or for the [YAML manifest](install-kerno.md#user-content-uninstalling-kerno), depending on your setup.
{% endhint %}

### 1. Navigate to the Installation Section

* In the **Kerno dashboard**, click on **Settings** (bottom-left corner).
* Select **Installation** from the left-hand menu.

### 2. Select the Cluster to Uninstall

* Under **Installations Details**, locate the cluster you want to remove.
* Click on **Uninstall Cluster**.

### 3. Generate the Uninstallation Script

* Choose the cluster from the dropdown menu in the **Uninstall a Cluster** window.
* Optionally, provide a reason for uninstalling.
* Click **Generate Uninstallation Script**.

### 4. Execute the Uninstallation Command

#### **Option 1: Using SSO Profile**

* Select the **SSO Profile** tab.
* Fill in the required details:
  * **AWS Cluster Name**
  * **Region**
  * **AWS Profile**
* Copy the generated command&#x20;
* Open your terminal and execute the copied command.

***

#### **Option 2: Using Environment Variables**

* Select the **Environment Variables** tab.
* Fill in the required details:
  * **AWS Cluster Name**
  * **Region**
  * **AWS Access Credentials**
* Copy the generated command
* Open your terminal and execute the copied command.

### 5. Confirm Uninstallation

* Wait for the script to complete.
* You can now delete the cluster from the **Installation Details** table.

{% hint style="info" %}
This will delete all Kerno components from your Kubernetes Cluster but not your S3 Bucket, where your Logs and traces are stored.
{% endhint %}

If you encounter issues or have questions, [message us on Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA), and we’ll gladly help.
