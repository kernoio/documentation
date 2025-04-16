---
description: >-
  The Issue Details Page is the core of Kerno’s troubleshooting experience. This
  is where you’ll spend most of your time diagnosing and resolving issues.
---

# Issues Details

All information on this page is carefully distilled, filtered, and correlated to provide actionable insights while maintaining full context throughout your investigation.&#x20;

### Key Components

The **Issue Details Page** is designed to simplify and accelerate the troubleshooting process by providing a centralized, interactive view of all relevant data. With rich features and seamless navigation, it enables you to identify and resolve issues quickly and effectively.

#### **Interactive Graph**

The top graph provides a **visual timeline** of key metrics related to the issue, including:

* **Traffic**: Volume of requests over time.
* **Occurrences**: Frequency of the issue within the selected timeframe.
* **Latency**: Response time trends, highlighting potential performance bottlenecks.
* **Events**: Significant Kubernetes events (e.g., crashes, warnings, or deployments).

You can click on a **spike in occurrences** to:

* **Filter Related Requests**: View all requests contributing to the issue, including details like paths, sources, latency, and status codes.
* **Filter Related Logs**: Drill down into log entries tied to the selected occurrences, making it easier to pinpoint the root cause.

#### Requests, Logs, and Stack Traces Table

Below the graph, the **Requests, Logs, and Stack Traces Table** provides all the granular information you need to troubleshoot issues. Each section is interactive, allowing you to dive deeper into specific entries for a thorough investigation.

**Requests**

This section lists all the requests associated with the issue, including timestamps, paths, sources, latencies, and status codes.

Clicking on a request opens a detailed view where you can inspect:

* **Payload Information**: Access the request and response bodies, headers, and status codes. For example, you can identify incorrect payloads or missing parameters in the request body (as shown in the attached image).
* **Infrastructure Context**: View the CPU and memory utilization of nodes and pods processing the specific request, helping you identify resource constraints or anomalies.

**Logs**

Log entries are linked to the issue, along with their timestamps and values.

Clicking on a log entry reveals detailed attributes such as related resources and the infrastructure context at the time of the event. For instance, you can pinpoint a log entry that corresponds to a failure and identify if it’s related to a pod crash or a resource limit breach.

**Stack Traces**

For application-level errors, such as exceptions, the **Stack Trace** section shows the code paths that led to the issue. This makes it easier to trace the problem to the root cause in your application code.

Developers can quickly locate the exact function or line of code where the error originated, helping reduce the time to resolve bugs.

#### **Event Timeline**:

The Event Timeline provides a **chronological view** of all **Kubernetes events and changes** relevant to the issue, such as **new deployments** or **pod restarts**, offering a clear picture of the sequence of events that occurred in the issue’s context.

{% hint style="info" %}
It highlights only **warning**, **error**, and **change events** to reduce noise while focusing on actionable insights
{% endhint %}

Each event is interactive, and clicking on it reveals:

* **Event Details**: Key attributes, such as the event type, timestamp, and summary.
* **Affected Resources**: Specific pods, nodes, or other resources impacted by the event.
* **Related Informational Events**: A list of associated informational events that occurred immediately before and after the selected event, providing additional context for better analysis.

This timeline ensures a focused and comprehensive view of events, making it easier to understand the issue’s progression, pinpoint root causes, and identify related system changes.

#### **Activity Tab**:

The Activity Tab provides a comprehensive history of the issue, capturing all key actions and discussions. This includes:

* **Status Changes**: Updates such as when the issue was opened, marked as in progress, or resolved.
* **Assignments**: Details about who is responsible for addressing the issue.
* **Team Discussions**: Logs of comments and collaboration related to the issue.

If the **Slack Integration** is enabled, the Activity Tab also syncs conversations from Slack or other collaboration tools. This ensures that all context, whether it’s team discussions, proposed fixes, or relevant insights, is centralized within Kerno, making it easy to track and maintain a complete record of the issue’s lifecycle.

{% hint style="success" %}
If you encounter issues or have questions, [message us on Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA), and we’ll gladly help.
{% endhint %}
