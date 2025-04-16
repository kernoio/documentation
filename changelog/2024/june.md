# June

### New Features

### Discovery: service maps

Our first early alpha release of Kerno’s discovery module! In this release you get an out of the box service map outlining distributed components and their relationships in your microservices architecture! With visual hints and context brought from component monitoring! Say goodbye to manually updating IDPs or service catalogs forever more!

Soon to come into this view: routes, events, change history, errors and documentation!

#### Issue resolution module

Out of the box, Kerno monitors HTTP activity and detects issues from your application stack traces.

Assign branches, people and transition states from within Kerno.

Coming soon: desktop notifications and assignment suggestions based on Git and CI activity!

#### Event timeline in monitoring module

Kerno helps you cut through the noise by correlating events of interest with sudden spikes in errors and rejections with our new time series event timeline. Stay focused on what matters instead of getting distracted by dozens of alerts.

### Improvements

#### Lightweight as a preon

Our node-agent -_**preon**-_ currently works at \~5% CPU utilization. We measure this efficiency against aggressively -near 100% CPU utilization- saturated nodes with dummy services that only respond immediately to requests -at >3000 requests per second per core-. This places preon in the range of \~7000 messages analyzed per second per 0.1 core with a memory utilization rarely crossing the 60MiB baseline (we still do reserve more than that to prevent OOM kills). Our expectations regarding overhead in real-world scenarios are way better.

#### On-prem logs and trace management

Kerno captures and uniquevoquely identifies error samples to avoid over-transmission and storage of error trace data. Stack traces and metrics are sent to our cloud to guarantee a top-of-class user experience, but critical log and trace data is stored encrypted in your cloud with very low storage consumption thanks to our at-source sample deduplication techniques.
