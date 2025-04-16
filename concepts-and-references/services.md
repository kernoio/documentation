# Services

### Service-Centric Observability Model

Modern applications are complex, spanning multiple environments, regions, and clusters. Despite this complexity, engineers naturally think about their applications in terms of services—the logical units that define how software operates and interacts. Teams focus on these services, not low-level infrastructure like deployments, pods, or clusters when building, deploying, and maintaining software.

At Kerno, **our goal is to align your team around a simple, service-centered observability model that matches how you naturally think about software and enables anyone to contribute to reliability**. That’s why we’ve built this model into everything we do, from collecting, storing, and analyzing data to how we present it and structure our pricing.

### Parent Workloads

A **workload** is any resource Kerno can observe, whether through logs, events, transport metrics (HTTP, gRPC, etc.), or resource metrics (CPU, memory). Workloads can exist independently or as part of a hierarchy with parent and child workloads.

For example, in **Kubernetes**, the smallest workload unit is a **Pod**, but Pods are typically managed by a **Deployment**. While a Deployment is just a configuration, Kerno treats it as the **parent workload** managing an application.

Therefore, parent workloads are usually **StatefulSets**, **Deployments**, or **DaemonSets**.

{% hint style="info" %}
Nodes themselves are **not** considered workloads. Instead, Kerno classifies them as **Compute Providers** since they allocate resources like CPU and memory for workloads to run. Workloads depend on them, but they are not observed in the same way.
{% endhint %}

### **Unique Service**

**A unique service represents a parent workload as a single entity, regardless of where it's deployed.**

Suppose you deploy a service in two regions and two environments across four Kubernetes Deployments in separate EKS clusters. In that case, Kerno treats them as a unique entity for which all associated workloads and observability data are automatically consolidated. This allows teams to monitor and reason about services holistically rather than as fragmented infrastructure components.

<figure><img src="../.gitbook/assets/Kerno&#x27;s Service Model.svg" alt=""><figcaption><p>Kerno's Service-Centric Observablity Mode</p></figcaption></figure>

{% hint style="success" %}
If you have any questions or suggestions, [message us on Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA), and we’ll gladly help.
{% endhint %}
