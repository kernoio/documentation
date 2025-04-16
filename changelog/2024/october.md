# October

### New Features

* **Add service map to the issues detail page**: Integrated a service map within the issues detail page for better visualization.
* **Logs for exception**: Implemented a feature to capture and store logs when stack traces occur for better error diagnosis.
* **Issue filters**: Introduced filters for issues such as "my issues," "unassigned," and "known."&#x20;

***

### Improvements

* **Combined k8s-resource-processor and k8s-service**: Combined two services to reduce traffic and improve platform stability)
* **Invite users through search input**: Added the ability to invite new users directly from the search input field.
* **Install Kerno page**: Added a dedicated landing page to guide users through installation.
* **Remove events filter**: Cleaned up unnecessary event filters.
* **Uniformize 'Empty data' messages across the app**: Standardized empty data messages across the platform.
* **Table sort should be kept during session**: Persisted table sorting preferences within the same user session.&#x20;

***

### Bug Fixes

* Fixed issue duplication due to old UUID usage.&#x20;
* Fixed an error in the stack trace display.&#x20;
* **Metrics graph misalignment**: Fixed the alignment issues in the metrics graph.
* Corrected header display issues.
* Fixed back and forward button issues in the browser.
* Fixed the alignment of stacked graphs in component views.&#x20;
* Resolved segmentation fault in Preon.
* Fixed multiple tooltips displaying simultaneously on charts.
* Fixed a bug where non-existent components displayed empty states instead of redirecting.
* Corrected the paths table behavior for upstream and downstream components.
* Fixed an issue where negative request counts were shown in charts.&#x20;
* Enabled keyboard navigation for installations.
* Fixed broken buttons in the event timeline.
* Adjusted icons for better responsiveness on smaller screens.&#x20;
