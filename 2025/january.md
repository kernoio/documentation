# January

### New Features

**Multi-Cluster Support** – Deploy Kerno across multiple Kubernetes clusters within your organization to centrally visualize and filter data across different environments. This improves observability and simplifies multi-cluster management.

**K8s Event Grouping** – Related Kubernetes events are now automatically grouped and linked to specific services or issues, reducing noise from isolated events and making root-cause analysis faster and more efficient.

**HTTPS Traffic Support** – Tracing encrypted traffic is now possible with OpenSSL across multiple languages (Python, Ruby, PHP) and popular servers (Apache, Nginx, HAProxy, Lighttpd, H2O, Cherokee, Gunicorn, Tornado). This ensures better visibility into secure communications without impacting performance.

***

### Improvements

**Option to Ignore Issues** – Issues can now be ignored directly within the issue view, helping to declutter reports and prioritize critical problems.

**Inspect Pods from Cluster View** – Access detailed pod information without leaving the cluster overview page, streamlining debugging and monitoring.

**Targeted Alerts** – Alerts can now be routed to specific channels in addition to the default Kerno alerts channel, improving team workflows and notification management.

**.NET Stack Traces** – Error tracking now includes full support for .NET stack traces, expanding Kerno’s coverage across more application environments.

**Simplified Installation** – The setup process no longer requires manually setting the Kubernetes context, reducing deployment complexity and potential configuration errors.

**Visibility of Deleted K8s Resources** – Deleted nodes and pods remain accessible for post-mortem analysis, ensuring historical data is available for auditing and debugging.
