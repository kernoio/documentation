---
description: >-
  Kerno automatically collects logs from all pods and namespaces, using smart
  filtering to retain only the most relevant data for troubleshooting and
  monitoring.
---

# Logs

### **Automatic Log Collection**

Once Kerno is installed, **logs are automatically collected from every pod across all namespaces without** additional configuration. Kerno supports multiple log formats including JSON, plain text, and NGINX Logs, and **automatically extracts key-value pairs** from structured logs, making them easy to query and analyze.

### **Smart Log Filtering**

Kerno processes **100% of logs** but applies **smart filtering** at the edge to retain only the most relevant data while reducing storage costs and noise. Filtering is performed **before logs are stored**, ensuring efficient resource usage without losing critical information.

Logs are selectively retained based on:

* **Error Logs**: Entries indicating failures, crashes, or unexpected behavior.
* **High-Signal Logs**: Logs related to anomalies, performance issues, or service disruptions.
* **Baseline Logs**: A representative sample of normal operations to provide context.

This approach ensures that logs remain **actionable, relevant, and easy to analyze** without overwhelming users with unnecessary data.

### **Log Enrichment**

Each log entry is enriched with additional context to streamline troubleshooting:

* **Service and Container Metadata**: Pod name, namespace, container image, and environment variables.
* **Correlated Metrics**: Logs are linked with relevant application and infrastructure metrics, allowing you to **view all related data in a single pane**.
* **Kubernetes Events**: Logs are enriched with Kubernetes events that may have impacted the service.

This deep correlation helps you quickly **trace issues back to their root cause** and gain better insights into your system’s behavior.

### **Log Storage & Retention**

Like traces, **logs are stored inside your own environment** within an **S3 bucket**, ensuring that **sensitive data never leaves your cloud**. This provides full control over log data while maintaining security and compliance.

By default, logs are retained for **30 days**, but you can customize the retention period based on your organization’s needs.

{% hint style="success" %}
If you encounter issues or have questions, [message us on Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA), and we’ll gladly help.
{% endhint %}
