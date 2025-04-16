---
description: >-
  Kerno automatically generates traces for supported technologies using its eBPF
  agent. These traces provide the deep visibility into service interactions
  without requiring manual instrumentation
---

# Traces

### **Automatic Trace Generation**

Kerno’s eBPF agent captures and generates traces **out-of-the-box**, with no configuration needed. Within seconds of installation, traces are available for every supported service in your stack. Each trace includes critical information, such as:

* **All participating services** (both client and server).
* **Accessed resources**, including URLs, endpoints, or database queries.
* **Full payloads**, which contain:
  * All headers.
  * All query parameters.
  * Complete request and response bodies.

{% hint style="info" %}
**Note:** Kerno's eBPF-based tracing does not currently support **distributed tracing**, but we're working on it!
{% endhint %}

### **Smart Trace Sampling**

Kerno processes **100% of requests** but applies **smart sampling** to store only the most relevant traces while maintaining an accurate picture of system behavior. Sampling is performed directly on the node, filtering traces based on:

* Requests with **unusually high or low latencies** for a given resource.
* Requests that returned **error responses** (e.g., HTTP 500).
* A baseline of **"normal" requests** to provide context.

This approach ensures efficient storage while preserving critical data for debugging and performance monitoring.

### **Trace Enrichment**

To provide deeper insights, Kerno enriches each trace with additional context, including:

* **Container Information**: Image details, environment variables, and pod names.
* **Logs**: Service-generated logs around the time of the trace.
* **Golden Signals**: Latency, error rate, and throughput data at the time of the trace.
* **Kubernetes Events**: Relevant cluster events affecting the service.
* **Resource Utilization**: CPU and memory usage of both the service and the node it runs on.

This enrichment allows users to correlate traces with logs, infrastructure metrics, and real-time performance data.

### **Trace Storage & Retention**

Unlike metrics, **traces are stored inside your environment** within your **S3 storage**, ensuring that **sensitive data never leaves your cluster**. This approach eliminates privacy concerns while giving you full control over your tracing data.

By default, traces are retained for **30 days**, but you can adjust the retention period based on your needs.

{% hint style="success" %}
If you encounter issues or have questions, [message us on Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA), and we’ll gladly help.
{% endhint %}
