## Initializing and Updating SAP Commerce Cloud

> ### Learning Objective
>
> - We will be able to evaluate the Initialization and Update processes of the SAP Commerce Platform.

#### Initialization and Update of SAP Commerce Cloud

- As a technical professional working on SAP Commerce cloud, Initialization and Update are the two key maintenance processes or actions one must perform.
- An SAP Commerce installation is dependent on the data stored in an **Relational database**.
- The **platform** allows us to extend the data structures provided out of the box.
  - We can extend or update the existing type definitions,
  - We can define new types.
- In both the cases, the initialization and update processes will ensure that the structures outlined in the **type definitions are reflected in the database**.

#### Initialization process

- During the installation, a new SAP Commerce instance can only be started and accessed once its type definitions are reflected in the database.
- Initialization process involves:
  1. **dropping existing tables**, should any exist,
  1. **reading the type defintions** contained in **items.xml** files,
  1. using the type definitions to **create tables** matching the definitions,
  1. once the tables are created, **essential and project data** are imported into database.

#### Update process

- Update process is similar to initialization.
- During update process :
  1. **tables** maybe **created** for **new types** defined in **items.xml** file,
  1. **existing tables** may be **altered** to reflect changes to existing types.
  1. **essential and project data** are imported into database.
     > **Note**:
     >
     > - Update process **doesn't drop any tables**.
     > - It also **doesn't delete** any existing data.

#### Initialization vs Update processes comparision

| **Initialization**                                                                                              | **Update**                                                                                                         |
| --------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| Used to **create new database** instance during installation.                                                   | Used to **reflect changes** to the type system into database.                                                      |
| It can be **invoked later** to **reset** the database to its **initial state**.                                 | It can be invoked later to update or **reflect type system changes** into database.                                |
| Any existing stored **data will be lost**                                                                       | **No** data loss                                                                                                   |
| Can be run from HAC by navigating to **Platform > Initialization**                                              | Can be run from HAC by navigating to **Platform > Update**                                                         |
| Can be executed from command line using ant command even if server is stopped.<br>platform % **ant initialize** | Can be executed from command line using ant command even if server is stopped.<br> platform % **ant updatesystem** |

> **Note:**
>
> 1. If we are planning to run the update several time during development, we can create a JSON configuration file by opening HAC > Platform > Update, then selecting the desired configurations and export it as a JSON file by clicking on "Dump Configuration" option available. We can then invoke update with that same configuration file by specifying it on the command line.
> 1. For both the processes, we can mention the tenant affected by the ant command, and provide optional parameters using a JSON configuration file like -
>
>    platform % **ant initialize** -Dtenant=master -DconfigFile=path/to/config.json<br>
>    platform % **ant updatesystem** -Dtenant=master -DconfigFile=path/to/config.json

- The above steps are useful for local setup and development.
- For deploying SAP Commerce Cloud in the public cloud (or ccv2), administrators have different ways to perform these actions. We tackle these methods in the advanced course on [Managing Build and Deployment Processes](https://learning.sap.com/learning-journeys/expand-upon-technical-essentials-of-sap-commerce-cloud/managing-build-and-deployment-processes_be740a06-e869-4c9f-8b13-59b922dd78ff).

---

Refer: [Managing Build and Deployment Processes](https://learning.sap.com/learning-journeys/expand-upon-technical-essentials-of-sap-commerce-cloud/managing-build-and-deployment-processes_be740a06-e869-4c9f-8b13-59b922dd78ff)

---

Next Lesson: [Getting to Know the SAP Commerce Installer](J01U02T07-Getting-to-Know-the-SAP-Commerce-Installer.md)

Learning Journey: [Exploring the Technical Essentials of SAP Commerce Cloud](..)
