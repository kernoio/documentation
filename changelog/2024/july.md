---
description: >-
  This month, we prioritized resolving issues and enhancing features based on
  the valuable feedback from our Public Beta launch.
---

# July

### **Improvements**

* **Cost**—We optimized our infrastructure and refactored our data handling to keep offering you flat and predictable pricing.
* **Dashboard Performance**—We optimized queries and table partition keys, resulting in over a 5X improvement in loading performance for metrics graphs.
* **Service Map**—Enhanced navigability with improved controls (Zoom in/out and recenter), auto-zoom on component selection, and path highlights to illustrate inter-service communications.
* **Dockerized Installer**—Kerno can now be installed using Docker, simplifying the setup process.
* **Global Search**—Pagination has been added to improve data management and user experience using global search functionality.
* **User list** - Pagination has been added to improve data management and user experience when managing users and teams.

### **Bug Fixes**

* **Stack Traces**—Resolved an issue where stack traces either failed to appear or took several seconds to load in the portal.
* **Metrics Graphs**—Fixed an issue causing metrics graphs to fail to load.
* **Kafka Consumer Lag**—Addressed a problem where Kafka consumers were falling behind.
* **User Invites**—Corrected an issue that prevented users from being reinvited.
