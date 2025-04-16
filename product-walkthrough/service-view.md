---
description: >-
  The Service View in Kerno provides detailed insights into a specific service,
  allowing you to monitor performance, investigate issues, and understand
  dependencies for efficient troubleshooting.
---

# Service View

### Service View Use-Cases

Use the Service View to:

* **Monitor Service Performance**:
  * Use the **Performance Graph** to observe trends in traffic, latency, and errors.
  * Correlate performance dips with events displayed on the graph timeline.
* **Analyze Dependencies**:
  * Explore the **Endpoint Table** to identify problematic upstream or downstream paths.
  * Switch to the **Map View** for a visual representation of service dependencies.
* **Inspect Infrastructure Resources**:
  * Drill into individual pods in the **Infra Resources** panel to analyze their resource usage or investigate issues.
* **Troubleshoot Events and Issues**:
  * Review the **Event Timeline** to understand how Kubernetes or configuration changes impacted the service.
  * Use the **Issues Panel** to identify and resolve application-level errors.

### **Key Components**

#### **Performance Graph**

The graph offers a comprehensive overview of the service's performance over time, including:

* **Requests/Second**: Tracks the number of requests handled by the service.
* **% of Failed Requests**: Shows the percentage of requests that resulted in errors or were rejected.
* **Latency**: Displays the service's average response time (P90, P50, P95, P99).
* **Events**: Highlights correlated Kubernetes or change events (e.g., pod restarts, configuration changes) that impacted the service.

#### **Endpoint Table**

A detailed table listing all **upstream and downstream paths** (endpoints) connected to the service, with key metrics:

* **Requests/s**: The traffic rate for each path.
* **Latency**: Average response time for requests on the path.
* **Error %**: The percentage of requests that failed.
* **Rejected %**: The percentage of requests rejected by the service.

#### **Map View**

The **Map View** visualizes the service's interactions with other components in the cluster. This service map visually represents upstream and downstream dependencies, helping you understand the service's role within the architecture.

**Infrastructure Resources**\
The **Infra Resources** panel lists the pods running the service and provides their current status. Clicking on a pod reveals detailed information, including:

* **Resource Usage**: CPU and memory consumption over time.
* **Pod Metadata**: Name, namespace, IP, creation timestamp, and conditions.

#### **Event Timeline**

Displays a chronological list of Kubernetes and change events associated with the service. For example, pod terminations or restarts are shown here, allowing you to correlate events with performance changes.

#### **Issues**

Highlights detected issues within the service, such as application errors or exceptions, making it easy to identify potential root causes.

{% hint style="success" %}
If you encounter issues or have questions, [message us on Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA), and we’ll gladly help.
{% endhint %}

