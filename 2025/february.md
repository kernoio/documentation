# February

### New Features

**HTTP/2 Tracing** – Kerno now captures and analyzes HTTP/2 requests, providing detailed metrics and request and response payloads, including headers and body, without any code change.

**gRPC Tracing** – Kerno now captures and analyzes gRPC requests, providing detailed metrics and request and response payloads, including headers and body, without any code change.

**Config Change and Rollout Tracking** – Whenever you deploy a new release or modify settings in Kubernetes, Kerno detects these changes and highlights exactly what was updated. This includes changes to container images, environment variables, and configuration files. Seeing a clear diff makes it easier to connect new rollouts or tweaks with any issues that arise.

<figure><img src="../.gitbook/assets/Screenshot 2025-02-28 at 22.49.54.png" alt=""><figcaption><p>Kerno Deployment Diff Analysis</p></figcaption></figure>

**Local Installer for Kubernetes** – You can now install Kerno on a local Kubernetes cluster with a single Docker command. This gives you full access to Kerno’s eBPF-powered observability without relying on external cloud resources or complex setups.

***

### Improvements

**Single-Step Install and Update Flow** – Installing, uninstalling, or updating Kerno is now a more straightforward process with fewer manual steps.

**Faster Metrics Dashboard** – We optimized our metric store to make dashboards load 3x  faster, even under heavy workloads.

**Improved Issue Resolution** – The issue resolution screen now brings all relevant context front and center, making it easier to investigate and resolve issues faster. Key details like logs, traces, infrastructure metrics, and recent config changes are pre-filtered and correlated, reducing noise and helping you pinpoint the root cause with minimal effort.

<figure><img src="../.gitbook/assets/Screenshot 2025-02-28 at 22.56.16.png" alt=""><figcaption><p>Issue Resolution Screen</p></figcaption></figure>

**Updated Global Service Map** – We redesigned the map’s layout and added interactive features. You can quickly see pod status, traffic flows, and node health.

<figure><img src="../.gitbook/assets/Screenshot 2025-02-28 at 22.48.31.png" alt=""><figcaption></figcaption></figure>

**Better Infrastructure Metrics Display** – CPU and memory usage now appear as absolute values with a progress bar, making it easier to understand resource use.

<figure><img src="../.gitbook/assets/Screenshot 2025-02-28 at 22.58.39.png" alt=""><figcaption><p>K8s Pod Metrics</p></figcaption></figure>

**Reduced Memory Use in Nanobe** – Nanobe ignores Kubernetes-managed fields and uses an ephemeral cache, which boosts performance and lowers overhead.

**Ruby Stack Trace Support** – Kerno can capture and show Ruby stack traces, giving more visibility into errors in Ruby-based applications.

### Bug Fixes

* **Connection Reliability** – Fixed problems that caused Nanobe and Preon to disconnect randomly, ensuring a stable data flow.
* **Consistent Dashboard and Tables** – We fixed pagination and filtering for timelines, logs, and requests. Data is now consistent across views.
* **UI Layout and Time Filters** – Addressed layout glitches and improved handling of time zones so node and pod metrics line up with the selected time window.
* **Minor Visual and Workflow Fixes** – Fixed tooltip alignment, table expansions, and other minor issues to give you a smoother overall experience.
* **Slack Channels in Alerts** – All your Slack channels appear in alert settings, making it easy to pick the right one.
* **Minuscule Rejections** – Small rejection rates no longer round to “0%.”
* **Deleting Alerts** – You can fully remove any threshold alert, even if it’s the only one.
* **Latency Chart Color** – Latency spikes are now highlighted with distinct colors for quicker identification.
* **Sorting the Issue Table** – Changing sort order no longer disrupts or clears the graph filters.
* **Time Selection for Infra Graphs** – You can now refine the displayed timeframe in both Node and Pod graphs.
* **Global Search** – Fixed an indefinite loading bug, so searches now produce immediate results or a “no results” message.
* **Redirect for Orgs With Zero Installations** – If your organization has no clusters installed, the redirect now works correctly.
