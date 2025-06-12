---
description: A collection of answers to frequently asked questions.
---

# FAQs

<details>

<summary>What is Kerno?</summary>

**Kerno is a runtime intelligence platform.** Kerno streams runtime intelligence from pre-production and production into the IDE and integrates deeply with AI code agents to help developers ship 10x faster without breaking things and fix minor issues early before they escalate.

</details>

<details>

<summary>What's the easiest way to install Kerno?</summary>

Kerno can be installed in minutes using Helm or Docker on any Kubernetes environment without code changes, complex configurations, or application restarts. Check out our [installation guide](getting-started/install-kerno.md) for more details.

</details>

<details>

<summary>Does Kerno support my programming language?</summary>

Yes. Kerno uses eBPF to observe your systems at the kernel level, which means it works with applications written in any language. Whether your services are in Go, Python, Java, Node.js, Rust, or anything else, Kerno can collect runtime signals without requiring language-specific instrumentation.

</details>

<details>

<summary>Does Kerno replace my current observability and APM tools?</summary>

No. Kerno is a developer productivity tool.\
\
It strips away the noise and gives developers the right context to quickly understand and fix issues without digging through dashboards. It runs alongside your existing observability tools but is tightly integrated into the IDE and your AI code agent to streamline everyday workflows. There is no extra overhead, no maintenance burden, just actionable runtime context where developers need it.

</details>

<details>

<summary>How does Kerno integrate with my current observability and APM stack?</summary>

Kerno collects its own system signals. It analyzes every data point but only stores about 1%. Even if some services aren’t instrumented or existing telemetry breaks, Kerno still gathers what it needs to provide value.

</details>

<details>

<summary>What are the resource and cost implications of using Kerno? Does it introduce overhead in terms of storage, CPU, or memory?</summary>

Kerno is designed to be lightweight and low overhead. The Kerno sensor uses less than 2% of node CPU and under 50 MB of memory. It runs in its own namespace and does not interfere with your application workloads.

For storage, Kerno writes data to a cost-effective, scalable, and highly durable object store inside your cloud (e.g. S3).

</details>

<details>

<summary>How is pricing calculated every month?</summary>

We calculate billing based on the average number of active Kubernetes nodes monthly. This smooths out short-term spikes and protects you from being charged for temporary bursts in usage.

</details>

<details>

<summary>Where does Kerno store my data?</summary>

Logs, traces, and payloads remain securely inside your environment. Kerno stores sensitive data in object storage within your cloud account, so you stay in full control, avoid vendor lock-in, and manage your data retention. Only anonymized metric data is pulled into Kerno to power the analysis.

</details>

<details>

<summary>Does Kerno offer a self-hosted version?</summary>

No. Kerno's UI and analytics engine run on our side. All sensitive data such as logs, traces, and payloads is stored securely in your own cloud. You stay in control of your data while avoiding the operational burden of managing the platform yourself.

</details>

<details>

<summary>Can I run Kerno outside of Kubernetes?</summary>

Not yet. Kerno currently runs on Kubernetes only. We're actively working on support for containerized and serverless environments outside of Kubernetes.

</details>

<details>

<summary>Where can I get help, ask questions, or submit feature requests?</summary>

You can reach out to us [directly on Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA). Our engineering team monitors it closely and will help you with any issues, questions, or feedback.

</details>

