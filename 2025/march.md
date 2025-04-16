# March

### New Features

* **PostgreSQL Tracing** – Kerno now automatically traces PostgreSQL queries, giving you detailed performance metrics and full visibility into request and response payloads, including headers and bodies, with zero code changes.
* **GKE Support** – You can now deploy Kerno to your Google Kubernetes Engine (GKE) cluster using a single Docker command.

<figure><img src="../.gitbook/assets/Screenshot 2025-04-13 at 18.04.07.png" alt=""><figcaption><p>Install Kerno on GKE</p></figcaption></figure>

* **AI-Powered Issue Investigation \[Beta]** – Kerno's AI agent can now assist with initial issue triage. When an issue is detected, it analyzes relevant signals and provides a summary along with suggested starting points for further investigation.

<figure><img src="../.gitbook/assets/GIFS.gif" alt=""><figcaption><p>AI Assited Investigation</p></figcaption></figure>

* **Kubernetes Alerts** – Kerno now supports alerting for Kubernetes pod and node-level events. You can configure alerts for pod restarts and crashes, as well as for node conditions such as NotReady, MemoryPressure, and DiskPressure.

<figure><img src="../.gitbook/assets/Screenshot 2025-04-13 at 18.08.56.png" alt=""><figcaption><p>Alert Configuration In Kerno</p></figcaption></figure>

* **Jira Integration** – You can now create Jira tickets directly from issues detected by Kerno. This allows you to link production issues with your existing issue tracking system for follow-up and resolution.

<figure><img src="../.gitbook/assets/Jira Integration.gif" alt=""><figcaption><p>Create a Jira Ticket</p></figcaption></figure>

* **Filter and Search** – You can now filter and search services and pods by namespace and name. This improves navigation and makes locating specific resources in large clusters easier.

<figure><img src="../.gitbook/assets/Filters.gif" alt=""><figcaption><p>Filtering &#x26; Search </p></figcaption></figure>

***

### Improvements

* **External Services on the Service Map** – The service map now includes external services that your Kubernetes cluster communicates with, giving you a more complete view of service dependencies.
* **Pod Health Summary in Service and Node Views** – Added pod-level health indicators to both the service and infrastructure views. This gives you a quick visual summary of how many pods are running, pending, failed, or succeeded across your services and nodes, making it easier to detect issues that might not yet impact top-level service metrics.

<figure><img src="../.gitbook/assets/Pod Context (1).png" alt=""><figcaption><p>Pod Health Context</p></figcaption></figure>

* **Pod Restart Events** – Pod restarts are now tracked as events in the timeline. You can view individual restart occurrences and see the total restart count per pod.

<figure><img src="../.gitbook/assets/Pod Restarts.png" alt=""><figcaption><p>Pod Restart Events</p></figcaption></figure>

* **Encrypted Traffic Detection for Ruby** – Updated the agent to support detection of SSL-encrypted traffic in Ruby applications, improving visibility in secure environments.
* **DaemonSet Toleration Support** – During installation, Kerno now detects node-level tolerations and automatically adds them to the DaemonSet configuration. This ensures components like Preon and Vector can run on nodes with custom scheduling constraints.
* **Preserve Issue Associations for Deleted Components** – Kerno now maintains links between issues and services that have been deleted. If a service is removed from the cluster, issues previously associated with it are still displayed and marked as deleted, ensuring historical context is preserved.
* **Improved Service Navigation** – The service preview now links directly to the full service detail view, allowing for a seamless transition when inspecting service-level data.
* **Toggle Deleted Pods and Nodes** – You can now show or hide deleted pods and nodes in the UI. This helps reduce visual noise while preserving the option to inspect recently removed resources.
* **Faster Event Loading** – Optimized event data retrieval to reduce load times in large clusters, improving responsiveness in dashboards and timelines.
* **Activity Tab UI Improvements** – Updated the activity tab to better differentiate between system events and user actions, improving readability and traceability.
* **Consistent Ordering and Scroll Behavior** – Standardized message ordering and scroll position for the chat and activity log views. The latest updates now load predictably at the bottom.
* **Improved Infrastructure Metrics Display** – Refined how CPU and memory usage, requests, and limits are visualized to improve clarity and make resource utilization easier to interpret.
* **Faster Data Loading in High-Volume Clusters** – Optimized front-end queries to improve load performance for clusters with large datasets.

***

### Bugs

* **Clear Issue List on Cluster Switch** – Fixed an issue where switching clusters would leave previously loaded issues visible, potentially causing confusion.
* **Fix Null in HTTP Traces** – Resolved a backend issue where some HTTP trace entries were missing destination identifiers, restoring complete trace information.
* **Prevent Internal Traffic Duplication in Preon** – Fixed a bug in Preon that caused internal service-to-service traffic to be counted multiple times.
* **Correct Issue Occurrence Counts** – Fixed a bug that caused mismatches between reported and actual issue occurrence counts in the UI.
* **Fix Text Clipping in Overflow Tooltips** – Ensured tooltip and popover content is fully visible, even for long strings or overflowing text.
* **Fix Infinite Scroll in Service Map** – Resolved a UI issue that caused the service map to scroll endlessly in certain cases.
* **Fix Service Map Positioning and Loading** – Addressed bugs that caused misalignment or incomplete loading of the service map in some environments.
* **Fix Paths Table Layout** – Adjusted the layout of the paths table to prevent overlapping elements and ensure consistent display.
* **Display Accurate Load Error Messages** – Implemented more specific error messaging when data fails to load, improving debugging and user feedback.
* **Fix Organization Creation Flow** – Resolved an issue that prevented some users from creating new organizations due to missing or restricted permissions.
* **Fix Slack Issue Links** – Updated Slack integration links so they open directly to the correct issue detail view instead of the general cluster overview.
* **Fix Intermittent Service Map Load Failures** – Fixed a bug where the service map would occasionally get stuck during loading.
