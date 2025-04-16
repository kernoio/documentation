---
description: >-
  The Issues View provides all the context and tools necessary to manage,
  prioritize issues affecting your Kubernetes cluster
---

# Issues View

The **Issues View** offers a centralized list of all detected issues affecting your applications and infrastructure. It lets you filter and analyze issue details to understand the problem better and triage effectively.

Kerno automatically aggregates and groups similar issues to reduce noise, helping you focus on the most critical problems. This grouping allows you to track how frequently a problem occurs and understand its impact on your services.

### **Issue Details**

Each issue in the list includes comprehensive details to help you understand and triage problems effectively:

* **Issue Name**: A clear description of the detected problem (e.g., application error or exceeded HTTP 5xx rate).
* **Occurrences**: Tracks how often the issue has been detected, offering insight into its frequency.
* **Components Impacted**: Lists affected services or infrastructure components, helping you identify the scope of the issue.
* **First Seen / Last Seen**: Indicates when the issue was first detected and when it most recently occurred, helping you track its progression.
* **Known Issues**: If the issue has occurred before, it will display a **"Known" tag**. This tag provides historical context, including how the issue was resolved previously, allowing you to apply similar solutions to recurring problems.
* **Status**: Shows the current state of the issue, enabling better triage:
  * **Open**: The issue has been detected but has not yet been addressed.
  * **In Progress**: The issue is being actively investigated.
  * **Closed**: The issue has been resolved or dismissed.
* **Assigned**: Identifies the person or team responsible for addressing the issue, ensuring accountability.

### **Issue Triage**

From the **Issues View**, you can begin to triage. You can:

* **Assign**: Assign issues to specific team members.
* **Ignore**: Dismiss issues that are not relevant or require no action.
* **Set Status**: Manually update the status of an issue to reflect its progress:
  * **Open**
  * **In Progress**
  * **Closed**
* **Set Priority**: Assign a priority level to issues to focus on critical problems.

{% hint style="success" %}
If you encounter issues or have questions, [message us on Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA), and we’ll gladly help.
{% endhint %}
