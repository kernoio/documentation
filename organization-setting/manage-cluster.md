---
description: >-
  Kerno supports multi-cluster installations, allowing you to manage multiple
  clusters under a single organization.
---

# Manage Cluster

### Add a New Cluster

To add a new cluster, follow the steps below:

**1. Navigate to the Installations Page**

* Go to **Settings**.
* Under **Organization**, click **Installations**.

**2. Register a New Cluster**

* Click the **Register a New Cluster** button.
* In the dialog that appears, enter a **Display Name** for your new cluster
* Click **Register Cluster** to confirm.

Once registered, your cluster will appear in the table under **Installation Details**, but it will not be fully installed yet.

**3. Install the Cluster**

* In the **Installation Details** table, locate your newly registered cluster.
* Click **Install cluster** in the **Actions** column for that cluster.
* Follow the installation steps in the wizard or prompts that appear. These steps typically involve providing any required configuration or credentials.

**4. Confirm the Installation**

After the installation process is complete, return to the **Installation Details** table and verify that the **Status** for your new cluster shows as **Active**. This indicates your cluster is successfully installed and ready for use.

### Delete a Cluster

If you no longer need a cluster, you can remove it from Kerno. This process involves generating a unique uninstallation script and running it on the cluster you wish to delete.

1. **Open the Installations Page**
   * In the Kerno app, go to **Settings** → **Installations**.
   * Under **Uninstall a Cluster**, click **Uninstall Cluster**.
2. **Select and Generate the Uninstallation Script**
   * In the **Select Cluster** dropdown, choose the cluster you want to remove.
   * (Optional) Provide a **Reason for Uninstalling** (e.g., “This cluster was installed as a test”).
   * Click **Generate Uninstallation Script**.
3. **Run the Uninstallation Command**
   * A Docker command (uninstallation script) will be displayed.
   * Copy and paste the command into your terminal, replacing placeholders with values specific to your environment.

Once this command is complete, your cluster should be removed. You’ll no longer see it under **Installation Details** in the Kerno UI.

{% hint style="success" %}
If you encounter issues or have questions, [message us on Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA), and we’ll gladly help.
{% endhint %}
