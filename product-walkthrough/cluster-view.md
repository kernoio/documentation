---
description: >-
  The Cluster View consolidates metrics from all services running in your
  cluster and infrastructure services, allowing you to monitor the overall
  health of your cluster and detect issues.
---

# Cluster View

### **Cluster View Use-Cases**

Use the cluster view to:

1. **Monitor Overall Cluster Health**:
   * Use the **Global Metrics Overview** to track key trends, such as spikes in failed requests or increases in latency.
2. **Analyze Service Performance**:
   * Sort the **Service List** table by metrics like **Error %** or **Latency** to identify problematic services.
   * Click on a service to access additional insights or related traces and logs.
3. **Inspect Infrastructure**:
   * Review the **Infrastructure Details** panel to monitor resource usage across nodes.
   * Drill down into individual nodes or pods to diagnose resource bottlenecks or issues.

### Key Components

#### **Global Metrics Overview**&#x20;

* **Requests/Second**: Tracks the average number of requests being processed per second in your cluster, allowing you to monitor workload intensity.
* **% of Failed Requests**: Displays the percentage of failed and rejected requests, helping you identify potential reliability issues.
* **Baseline Comparison**: The dotted line represents the 7-day mean, providing a historical reference for understanding performance trends.

#### **Service List**&#x20;

* A table displaying all services and system components in your cluster. Key metrics include:
  * **Req/s**: The number of requests handled per second by each service.
  * **Latency**: The average response time (in milliseconds) for each service.
  * **Error %**: The percentage of failed requests for each service.
  * **Rejected %**: The percentage of requests actively rejected.
  * **Issues**: The number of detected issues associated with the service.

#### **Infrastructure Details**

* Provides real-time insights into node-level metrics for your cluster, including:
  * **Nodes**: Number of active nodes in the cluster.
  * **Pods**: Number of pods running on each node.
  * **CPU and Memory Usage**: Resource utilization for each node, helping you identify potential bottlenecks or overutilized nodes.

### **Drill Down into Node and Pod Details**

**Node Details**: Clicking on a node in the **Infrastructure Details** panel opens a detailed view of its metrics, including CPU and memory usage over time, and a list of pods running on the node.

**Pod Details**: Clicking on a specific pod from the **Node Details** view provides granular insights, including:

* **Pod Metadata**: Name, namespace, IP address, and creation timestamp.
* **Conditions**: Current status of the pod (e.g., initialized, ready, scheduled).
* **Containers**: A breakdown of all containers running within the pod, including their statuses and resource usage.

{% hint style="success" %}
If you encounter issues or have questions, [message us on Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA), and we’ll gladly help.
{% endhint %}

