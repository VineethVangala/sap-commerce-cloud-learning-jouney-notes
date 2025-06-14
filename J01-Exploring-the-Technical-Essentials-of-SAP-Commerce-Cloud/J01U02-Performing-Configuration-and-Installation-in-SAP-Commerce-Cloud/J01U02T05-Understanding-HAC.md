## Understanding the SAP Commerce Administration Console

> ### Learning Objective
>
> - We will be able to discover how the Administration Console enables we to effectively administer, monitor, and configure SAP Commerce Cloud.

#### SAP Commerce Administration Console

- It is the first SAP Commerce Cloud GUI a technical user can encounter is the SAP Commerce Administration Console, or HAC (Hybris Administration Console).
- If SAP Commerce Cloud is deployed locally for development or testing purposes, we can visit HAC at the following URL: https://localhost:9002.
- If SAP Commerce Cloud is deployed in the public cloud, we can access it by visiting the assigned endpoint: Endpoint URL/hac.
- The HAC is a web application equipped with tools for **administering, monitoring, and configuring** your SAP Commerce Cloud solution.
- Its major functionalities are:
  1. **Administration**:
     - We can use HAC to perform various administrative tasks such as :
       1. Activating or viewing **tenants**.
       1. Managing logging levels for specific **loggers**
       1. **Initializing or updating** the system
       1. **Generating SQL scripts** for either initialization or updates
       1. Verifying **license** information
       1. Downloading support **log files** (such as console, access, solr, jdbc, and so on)
       1. Employing the **PK Analyzer** to examine the primary keys
  2. **Monitoring**:
     - We can also use the HAC to monitor the system at runtime.
       1. On the **Cache** page, we'll see parameters, statuses, and statistics for activated caches.
       1. The **Cluster** page shows us the statuses of the available cluster nodes.
       1. For **database monitoring**, we have four aspects:
          1. The **Data Sources** tab where we can find all configured data sources along with their status parameters.
          1. The **Table Size** tab presents a comprehensive list of database tables for the configured data source with their current sizes.
          1. The **JDBC Logging** tab allows us to enable logging to the configured log file and also download it.
          1. The **JDBC Log Analysis** tab helps us identify JDBC statements that either execute frequently or take unusually long to execute.
       1. we can use the **Thread Dump** function to generate a system thread dump.
  3. **Configuration**:
     - The HAC allows us to create, search, or modify configuration properties during runtime.
       > **Note**: The runtime changes made in the HAC are **not permanent**. When the server restarts, all settings revert to their original values from the corresponding properties files.

---

Refer: [Administration Console](https://help.sap.com/docs/SAP_COMMERCE_CLOUD_PUBLIC_CLOUD/3aa47afb5d494fb6837998dd0772f056/8be770da8669101487a5b744fb536106.html)

---

Next Lesson: [Initializing and Updating SAP Commerce Cloud](J01U02T06-Initializing-and-Updating-SAP-Commerce-Cloud.md)

Learning Journey: [Exploring the Technical Essentials of SAP Commerce Cloud](..)
