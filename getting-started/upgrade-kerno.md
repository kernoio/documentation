---
description: Learn how to upgrade your Kerno agent.
---

# Upgrade Kerno

To upgrade your Kerno agent to the latest version, follow these steps:

### **1. Navigate to the Installation Section**

* In the **Kerno dashboard**, click on **Settings** (bottom-left corner).
* Select **Installation** from the left-hand menu.

### **2. Select the Cluster to Update**

* Under **Installation Details**, find the cluster you want to update.
* Click on the **Actions menu** (three dots).
* Select **Update Cluster** from the dropdown.

### **3. Choose the Update Method**

#### **Option 1: Using SSO Profile**

* Select the **SSO Profile** tab.
* Fill in the required details:
  * **AWS Cluster Name**
  * **Region**
  * **AWS Profile**
* Copy the generated command

#### **Option 2: Using Environment Variables**

* Select the **Environment Variables** tab.
* Fill in the required details:
  * **AWS Cluster Name**
  * **Region**
  * **AWS Access Credentials**
* Copy the generated command

### **4. Run the Update Command**

* Open your terminal and execute the copied command.
* Wait for the update process to complete.

### **5. Verify the Update**

* Return to the **Kerno dashboard**.
* Confirm that the data is and everything works as expected.

If you encounter issues or have questions, [message us on Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA), and we’ll gladly help.
