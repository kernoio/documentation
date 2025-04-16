# November

### New Features

* **Trace Sampling & Correlation:** Introduced sampling for HTTP trace data, storing header and body samples on correlating HTTP traces for deeper error correlation and better visibility into request behavior.
* **Structured Logging Support:** Implemented structured logging support with Node.js and Winston, enabling better trace correlation and visibility for JSON-based logs.

***

### Improvements

* **Trace Correlation Logic:** Enhanced the trace correlation process in `nanobe` to better link HTTP traces with stack traces, improving root cause identification for errors.
* **Updated Metrics Handling:** Improved global metrics endpoint to include rejected fields, providing clearer visibility into request handling and failures.
* **Improved Installation Experience:** Updated installation instructions, removing unnecessary fields and simplifying the process for faster deployment.

***

### Bug Fixes

* **Latency Chart Fix:** Resolved latency chart scaling issues, ensuring better visibility of high and low spikes.
* **Timezone Handling Fix:** Corrected pod metrics reporting to reflect user timezones accurately.
* **Namespace Logic Fix:** Adjusted namespace logic to prevent data duplication across environments.
* **Stack Trace Display Fix:** Corrected an issue where stack traces appeared above charts in issue detail views.
