---
description: >-
  Kerno automatically detects, aggregates, and highlights issues across your
  Kubernetes cluster, helping you quickly identify and troubleshoot problems at
  both the application and infrastructure levels.
---

# Issues

### Types of Issues

Kerno identifies various application and infrastructure issues, giving you complete visibility into problems across your cluster. These issues are automatically detected and enriched with context, making it easier to understand their cause and impact.

Kerno can help you detect the following issues:

* **HTTP/gRPC Errors**:
  * Detects failed HTTP calls, such as **5xx server-side errors**, which indicate issues like application crashes, misconfigured endpoints, or unhandled exceptions.
  * Identifies **4xx rejected requests**, helping you diagnose problems such as client-side errors, rate-limiting, authentication failures, or overloaded services.
* **Application Exceptions –** Automatically captures exceptions thrown by your application, such as:
  * **Unhandled Errors**: Errors not caught in your application logic.
  * **Runtime Exceptions**: Issues like null pointer exceptions or type mismatches.
* **PostgreSQL Database Errors –** Monitors database interactions and flags common issues, such as:
  * **1146 — No Such Table**: Query references a table that doesn’t exist.
  * **1064 — Syntax Error**: SQL query contains invalid syntax.
  * **1040 — Too Many Connections**: Database connection limit exceeded, disrupting availability.
* **Node and Pod Scheduling Issues –** Identifies problems during pod scheduling, such as insufficient resources (e.g., CPU or memory) or taints that prevent pods from being assigned to nodes.
* **Pod Restarts and Crashes –** Detects pods that are restarting frequently or crashing unexpectedly, which may indicate:
  * **Resource Constraints**: Insufficient CPU or memory allocations.
  * **Configuration Errors**: Misconfigured environment variables, secrets, or volume mounts.
  * **Application-Level Problems**: Crashes caused by bugs or dependencies.
* **Deployment Failures –** Flags issues encountered during deployments, such as:
  * Pods failing to start due to readiness or liveness probe failures.
  * Rollout failures where new versions cannot be deployed successfully.
* **Latency Spikes –** Identifies unusual increases in response times for services or endpoints, often caused by:
  * **Resource Bottlenecks**: Overloaded nodes, network congestion, or throttled services.
  * **Database Slowdowns**: Long-running queries or contention for locks.

{% hint style="success" %}
If you encounter issues or have questions, [message us on Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA), and we’ll gladly help.
{% endhint %}
