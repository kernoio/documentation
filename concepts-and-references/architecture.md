# Architecture

### Key Design Principles

1. **Data Privacy & Ownership**
   * Sensitive data (like logs and traces containing potentially identifiable information) should always remain in your environment, ensuring you retain full control over how it is stored, accessed, and retained.
2. **Security**
   * **No inbound ports**: Kerno does not open any ports into your cluster; instead, a single outbound connection securely transmits data.
   * **Least privilege**: Uses tightly scoped IAM policies and Kubernetes RBAC to minimize security risks.
   * **Encryption**: Encrypts data both in transit and at rest to comply with modern data protection standards.
3. **Minimal Maintenance Burden**
   * **One command deployment**: Installs Kerno’s components and cloud resources in a single step, reducing operational overhead.
   * **Automated updates**: Streamlined updates follow the same simple install process.
4. **Minimal System Footprint**
   * **Lightweight DaemonSets**: Runs only a few small components in one dedicated namespace, minimizing resource usage.
   * **Focus on what matters:** Process data at the edge to filter out noise and use smart sampling strategies to store only high‐value logs, traces, metrics, and error data to minimize unnecessary data transfer, lower bandwidth costs, reduce storage overhead, and focus on the insights that matter most.

### **High Level Architecture**

Kerno is deployed into your Kubernetes cluster in a dedicated `kerno` namespace. Below is a high-level summary of the components.

<figure><img src="../.gitbook/assets/Kerno Architecture (1).png" alt=""><figcaption><p>Kerno Architecture Overview</p></figcaption></figure>

{% hint style="info" %}
Each monitored Kubernetes Cluster will have its own Nanobe, Vector, Preon, and Object Storage components.
{% endhint %}

### Components Installed in Your Environment

**Preon (DaemonSet):** Kerno's eBPF agent that captures real‐time traffic metrics, errors, and spans.

{% hint style="info" %}
Preon runs on a separate pod in a separate namespace. Therefore, it has no impact on your monitored applications.
{% endhint %}

**Vector (DaemonSet):** Collects and parses logs before forwarding them to `Nanobe`

**Nanobe (Deployment):** Aggregates and filters data from Vector, Preon, and the Kubernetes API Server.  It then sends logs and traces to your Objects Storage and metrics, errors, and key Kubernetes events Metadata to Kerno’s Cloud over a secure outbound WebSocket connection.

**Amazon S3 Bucket:** Stores your logs and traces.

{% hint style="success" %}
If you encounter issues or have questions, [message us on Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA), and we’ll gladly help.
{% endhint %}
