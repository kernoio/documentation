---
description: >-
  In this release, we've introduced several new features and enhancements to
  make troubleshooting faster and more efficient, along with bug fixes to
  improve the overall stability of the platform.
---

# August

## **New Features:**

* **Interactive Service Maps for Issue Resolution:** A real-time visual representation of service interactions, showing request flows, error rates, and performance metrics across your system so you can quickly pinpoint issues and identify affected services for faster troubleshooting.
* **Native Stack Trace Support for Java, JavaScript, and Golang:** Provides language-specific error tracing, allowing developers to quickly identify and resolve issues in their codebases with detailed, language-tailored stack information.
* **Endpoint Grouping Enhancement:** Consolidates and groups similar endpoint URLs by abstracting away dynamic parameters, reducing noise and helping developers focus on identifying problematic endpoints without being overwhelmed by unnecessary detail.

## **Improvements:**

* **Consistent 'Empty Data' Messages:** Standardized the 'Empty Data' messages across the app for a more uniform experience.
* **Infrastructure Color Coding:** Updated bullet points in the infrastructure details to reflect status-based colors, indicating the health or status of components more clearly.
* **Interactive Graphs:** Enhanced graphs to be interactive, allowing for better filtering of errors and events.
* **Persistent Table Sorting:** Table sorting now persists throughout a session for a smoother experience.

### **Bug Fixes:**

* **K8s Metrics:** Fixed an issue where null usage metric values were not being sent.
* **Missing Resources in Infrastructure Details:** Now all relevant resources are displayed regardless of their creation/update date.
* **Issue Details Window Resize Glitch:** Fixed a glitch where the chart on the Issue Details page would behave erratically during window resizing.
* **UI Improvements and Minor Fixes:** Addressed various small bugs, including UI inconsistencies, incorrect labels, and graph sizing issues.
