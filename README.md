# Introduction

### What is Kerno?

**Kerno is a runtime intelligence platform.** Kerno streams runtime intelligence from pre-production and production into the IDE and integrates deeply with AI code agents to help developers ship 10x faster without breaking things and fix minor issues early before they escalate.

### **What Makes Kerno Different**

**Developer-Focused with Opinionated Workflows**: Kerno does the heavy lifting to provide only the essential data needed to troubleshoot application issues, using opinionated workflows that guide you to the right places to look without unnecessary noise or complexity. It's designed for developers of any experience level, so you don't need to be a power user or systems expert to contribute effectively.

**Event-Based Data Collection**: Kerno focuses on critical events by collecting data only when something breaks. It correlates and deduplicates information before presenting it, so you don't have to sift through logs, traces, or dashboards.

**Easy Installation and Low Maintenance**: The Kerno sensor gives you complete visibility without requiring SDK integrations, code changes, or application restarts. You won't need to instrument your code now or in the future, eliminating potential blind spots and ensuring consistent monitoring. The agent runs separately from your applications and uses minimal resources.

**Keep Control of Your Sensitive Data**: Kerno keeps all sensitive data within your cloud; no data leaves your infrastructure.

**Predictable Pricing**: Kerno is priced per node, not based on data volume, so you won't encounter surprise bills as you scale.

### **Zero-Code Instrumentation with eBPF**

**eBPF (extended Berkeley Packet Filter)** enhances the capabilities of the Linux kernel by providing a safe and efficient way to extend kernel functions without modifying kernel code. This technology has fundamentally transformed observability and performance monitoring in modern Linux environments.

#### **Key Benefits of Kerno’s eBPF Agent**

* **Out-of-the-Box, Language-Agnostic Visibility**: By leveraging specific kernel hook points, Kerno offers complete visibility into your applications without needing SDK integration, code modification, or application redeployment.
* **Minimal System Footprint**: Deployed as a DaemonSet, Kerno’s eBPF agent runs separately from your application, resulting in minimal CPU and memory impact and avoiding unexpected resource overhead on your infrastructure.
* **Granular Data Down to the Payload Level**: Kerno provides metrics, logs, and traces—including header and payload data for every request.

### **Stay in Control of Your Sensitive Data**

Kerno stores all your sensitive data inside your cloud, ensuring that your sensitive data, contained in logs and traces, never leaves your cluster. This data is pulled to the Kerno portal on-demand using double-blind encryption, so it's never exposed to Kerno or any third parties.

By leveraging Object Storage, Kerno stores this data cost-effectively while maintaining high availability and durability.

### **Fair and Predictable Pricing**

Kerno’s architecture enables Kerno to offer a fair, transparent, and predictable pricing model based on the number of nodes. **Data volumes don't affect your subscription price so that you can scale without unexpected costs.**
