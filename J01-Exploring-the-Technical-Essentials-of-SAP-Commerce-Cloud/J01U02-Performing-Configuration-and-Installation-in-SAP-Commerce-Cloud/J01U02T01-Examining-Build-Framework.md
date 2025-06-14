## Examining the Build Framework

> ### Learning Objective
>
> - To summarize the key aspects of the SAP Commerce platform build framework.

#### Build Framework

- SAP Commerce Cloud has a custom build framework based on **Apache Ant**.
  - Ant handles :
    - source-code generation
    - compilation
    - a number of automation tasks.
- There are two ways to build SAP Commerce -

  - Platform-wide,
  - Extension-wide.

| Scope              | Ant call directory               | Extensions built                                                                                               |
| ------------------ | -------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| Platoform-wide     | <HYBRIS_BIN_DIR>/**platform**    | **Platform and all extensions listed in localextensions.xml**                                                  |
| Extension-specific | <HYBRIS_BIN_DIR>/{extensionhome} | **Current extension only**<br> (even if other extensions are connected to it via dependency, they are ignored) |

- "Build" means executing an **ant target**, such as **ant all** or **ant clean all**
- Extension-specific builds work as each extension has an Ant **build.xml** file, which is generated when it is intially built.

  - We generally use the build.xml in platform extension to build entire suite.

- When you call **ant**, the build framework:

  - generates and compiles **Model** classes
    - according to the definitions in the <b>\*-items.xml</b> files
    - in the order required by declared extension dependencies.
  - collects localization properties from respective property files (like **locales_XY.properties**)
  - updates configuration of the Commerce Server
  - generates new folders in the installation base folder (only in the **first run**).
    - a **config** folder for storing platform-wide configuration files such as localextensions.xml and local.properties.
    - a **data** folder for keeping developer-mode database files, media files, search-engine index files, hotfolders, and other types of data-storage files.
    - a **log** folder for keeping log files.

#### Build Targets

- The ant build framework is configured with a number of predefined **build targets** for our use. Few examples are :

  | Ant target | Command        | Description                                                                  |
  | ---------- | -------------- | ---------------------------------------------------------------------------- |
  | all        | ant all        | Builds the extension or platform and configures the server                   |
  | build      | ant build      | Builds the extension or platform                                             |
  | clean      | ant clean      | Cleans-up the platform and extensions. <br> (deletes generated .class files) |
  | extgen     | ant extgen     | Generates an individual extension based on an **extension template**         |
  | initialize | ant initialize | Initializes the system <br> (Re-creates and populates database tables)       |
  | -p         | ant -p         | Shows a list of all available Ant targets                                    |

---

Next Lesson: [Exploring Extensions in SAP Commerce Cloud](J01U02T02-Exploring-Extensions-in-SAP-Commerce-Cloud.md)

Learning Journey: [Exploring the Technical Essentials of SAP Commerce Cloud](..)
