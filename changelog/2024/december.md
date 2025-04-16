# December

### New Features

* **HTTP Trace Visualization:** New design for HTTP spans visualization with improved graphical representation of request flows, making trace analysis more intuitive.
* **Installer Preview Mode:** Added a dry-run preview mode in the installer, allowing users to review changes before applying them, improving installation safety and transparency.
* **Nginx Reverse Proxy Support:** introduced compatibility with clusters using Nginx reverse proxies for better traffic visibility and component correlation.

***

### Improvements

* **Vector Integration for Log Handling:** Migrated log collection to `Vector` for improved performance and reliability in large clusters, reducing resource usage compared to previous solutions.
* **Slack Integration Enhancements:** Implemented Slack threading for issue updates, allowing better visibility and tracking of issue progress directly within Slack threads. Issue comments made in Slack now sync back to the Kerno dashboard for a two-way communication experience.
* **Request Sampling Enhancements:** Enhanced sampling of HTTP payloads and headers for better trace correlation, especially when linked with stack traces.
* **Login Session Management:** Extended the expiration time for login tokens to reduce unnecessary logouts.

***

### Bug Fixes

* **Fixed Known Issue Flagging:** Resolved a bug where new errors were incorrectly marked as known issues.
* **Fixed Slack Invitation Errors:** Addressed a bug when attempting to resend invitations from Slack.
* **Corrected IP Resolution in Nanobe:** Adjusted the component lookup process to avoid stale IP mappings from completed pods, reducing incorrect component associations.
* **UI Adjustments:**
  * Fixed issue with 4xx errors not displaying on service maps.
  * Corrected data scaling issues in the failed request graphs.
  * Fixed a bug where empty stack trace tabs were not greyed out.
