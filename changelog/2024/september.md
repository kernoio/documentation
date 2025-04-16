---
description: >-
  Continuing our focus on faster issue resolution and better visibility, this
  release introduces several features and refinements to improve the
  troubleshooting experience.
---

# September

### **New Features:**

* **Normal State Metric Baseline:** Calculates a "normal state" for each metric based on historical behavior. This helps developers determine if observed metrics, like error rates, are within normal ranges or cause for concern.
* **Kubernetes Infrastructure Metrics:** Added Kubernetes infrastructure metrics at the cluster, node, and pod levels to provide better context during issue resolution, helping developers differentiate between infrastructure and application issues.
* **Slack Integration for New Issues:** Initial Slack integration sends notifications for new issues directly to a dedicated "Kerno" channel, keeping teams informed in real-time.
* **Log Capture for Issues:** Automatically collects detailed logs and attaches them to issue reports, giving developers immediate access to relevant logs for faster troubleshooting.
* **Cluster View:** A new feature providing a comprehensive overview of a Kubernetes cluster's health, allowing users to assess the system's overall state and identify potential issues more quickly.

### **Improvements:**

* **Issue Resolution Page Rework:** Redesigned for better clarity and usability, with unnecessary data removed, new informative visualizations added, and an improved layout.

### **Bug Fixes:**

* Minor UI consistency and alignment issues were fixed to enhance the overall user experience.
