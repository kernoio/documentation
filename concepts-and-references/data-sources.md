# Data Sources

Kerno uses **eBPF** to automatically instrument Kubernetes applications, capturing traces and metrics without requiring code changes or manual instrumentation.

Kerno currently supports the protocols, encryption libraries, and runtimes listed below.

{% hint style="success" %}
We're always expanding our coverage. Check out our [public roadmap](https://github.com/orgs/kernoio/projects/3) to see what's coming next, and let us know what you'd like us to support [on Slack](https://join.slack.com/t/kerno-community/shared_invite/zt-2tiblmlpx-c05QvbiOEZ_lWUtxECUKWA).
{% endhint %}

### Supported Protocols

Kerno supports tracing of traffic encrypted with the following protocols:

| Protocol | Status    | Notes |
| -------- | --------- | ----- |
| HTTP 1   | Supported |       |
| HTTP 1.1 | Supported |       |
| HTTP2    | Supported |       |
| gRPC     | Supported |       |

### Supported Encryption Libraries

Kerno supports tracing of traffic encrypted with the following libraries:

| Libraries | Status    | Notes                                                                                                                                                                                                                 |
| --------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| OpenSSL   | Supported | <p><strong>Languages</strong><br>Python, Ruby, PHP<br><br><strong>Web servers</strong> </p><p>Apache, Nginx, HAProxy, Lighttpd, H2O, Cherokee<br><br><strong>Application servers</strong></p><p>Gunicorn, Tornado</p> |

