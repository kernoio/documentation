---
description: >-
  Kerno provides a comprehensive, context-rich view of your k8s stack by
  collecting and correlating metrics from both application and infrastructure
  layers.
---

# Metrics

### Metric Collection

Kerno collects data from two primary sources:

* **Proprietary eBPF Agent**: Kerno's eBPF agent operates at the kernel level to collect detailed traffic metrics from any application, regardless of the programming language, including encrypted traffic. This method ensures high accuracy while maintaining minimal impact on cluster performance.
* **Kubernetes API**: Infrastructure metrics are gathered from Kubernetes components, such as kube-system workloads, nodes, and cluster-level resources, through the Kubernetes API. This provides a detailed view of cluster resource utilization and health.

### Metric Enrichment

Kerno goes beyond basic metric collection by enriching data to correlate application and infrastructure metrics. This process creates a transparent and actionable view of your Kubernetes ecosystem, enabling you to understand how application performance interacts with the underlying infrastructure.

By monitoring Kubernetes as an integral part of your application infrastructure rather than in isolation, Kerno highlights potential points of failure in the interconnected environment. This correlation provides actionable insights, such as:

* Identifying infrastructure bottlenecks impacting application performance.
* Detecting application behavior anomalies caused by cluster resource constraints.
* Offering a comprehensive understanding of how Kubernetes operations directly affect workloads.

### Metric Storage

Kerno securely stores all collected metrics in its cloud infrastructure, minimizing operational overhead and reducing resource consumption on your cloud environment.&#x20;

Metrics are retained for **30 days**, ensuring access to historical data for performance analysis and optimization.

Unlike logs and traces, which may contain sensitive information, **metrics are inherently non-sensitive by design**. This makes Kerno’s efficient and privacy-compliant storage approach, eliminating concerns about confidential data leaving your environment.

### Application Metrics

Application metrics provide visibility into the performance and behavior of your workloads. These metrics are essential for understanding how applications interact with the Kubernetes infrastructure and identifying bottlenecks or errors.

Kerno collects the following application metrics (aka Golden Signals):

* **Request Rate (Req/s)**: Tracks the number of requests processed by an application per second, helping you understand workload intensity.
* **Latency**: Monitors the response time for application requests, enabling you to identify slowdowns.
* **Error Rate**: Measures the percentage of failed requests, offering insights into application reliability.

These metrics are collected in real-time, enabling you to correlate application performance with underlying infrastructure metrics for root cause analysis.

### **Infrastructure Metrics**

Infrastructure metrics provide a detailed view of the cluster's resource usage and stability. These metrics ensure critical resources are correctly allocated to maintain cluster performance and prevent failures.

Kerno collects the following key infrastructure metrics :

* **Node & Pod CPU Consumption**: Monitors CPU usage to ensure workloads have sufficient processing power, preventing resource exhaustion and application failures.
* **Node & Pod Memory Utilization**: Ensures workloads have enough memory to prevent performance degradation and resource shortages.

By combining infrastructure metrics with application data, Kerno provides a unified view of cluster health and enables proactive resource management.

{% hint style="success" %}
If you encounter issues or have questions, [message us on Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA), and we’ll gladly help.
{% endhint %}
