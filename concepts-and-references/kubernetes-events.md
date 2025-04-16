---
description: >-
  Kerno collects, categorizes, and enriches Kubernetes events to provide
  actionable insights into what is happening in your cluster at any given
  moment.
---

# Kubernetes Events

### Event Collection & Classification

Kerno collects all Kubernetes events from your cluster, but Kubernetes does not inherently classify events by severity. To make events more actionable, Kerno applies its own logic to categorize them into three clear levels:

* **Info**: Expected system events that indicate normal behavior.
* **Warning**: Issues that Kubernetes can recover from without user intervention.
* **Error**: Critical issues that require manual intervention.

This classification helps reduce noise and lets you quickly focus on the events that matter most.

### Event Grouping

Kubernetes generates a high volume of often unstructured events and lack relationships, making it difficult to understand their context or root cause. For example, it’s unclear if an event was triggered by a deployment, a pod failure, or unrelated system activity. Kubernetes does not inherently group events or indicate whether they are part of a series or isolated.

Kerno groups related events and links them to specific services and issues. This ensures that when troubleshooting, you get the right context and a clear understanding of how events are connected, making it easier to identify and resolve the root cause of problems.

### **Event Storage and Retention**

Like metrics, Kubernetes events are securely stored in Kerno’s **cloud infrastructure** to reduce the operational burden on your cluster. Events are retained for **30 days** by default, with the option to adjust retention based on organizational needs.

{% hint style="success" %}
If you encounter issues or have questions, [message us on Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA), and we’ll gladly help.
{% endhint %}
