## Configuring Properties Files

> ### Learning Objective
>
> - We will be able to define configuration properties files and their effects on the SAP Commerce platform.

#### Configuring Properties Files

- In SAP Commerce Cloud, there are **four** kind of important configuration files:

  1. **config/localextensions.xml** - It is used to decide which extensions need to be loaded during setup of the SAP Commerce server.
  2. **{extensioname}/extensioninfo.xml** - They are used to define the dependency of an extension on other extensions. <br>Example:

  ```xml
    <!-- add all dependent extensions -->
    <requires-extension name="basecommerce">
  ```

  > **Note**: If Eclipse IDE is being used, we also need to configure the dependencies in the Java build path window of the extension, as the defined dependencies are not automatically resolved by Eclipse.

  3. **{extensioname}/project.properties** - It is present in each extension and is used to define and expose configuration properties in the current extension.
  4. **config/local.properties** - It is used to override the default property value in each extension. <br>For example, we can override default server configuration like DB url and credentials.

- It is possible to define same property in different project.properties files.

#### How is the final property value determined?

- > TL;DR : through **project.properties precedence**.

- The final property value depends on the loading order of extensions, which obey following principles :

  - **All extensions implicitly depend on platform.**
  - **Dependency chain of extensions determine precedency.**
  - **All local.properties settings override all project.properties settings.**
  - **Cyclic dependencies are not allowed, and will be rejected by ant.**

- An example for the properties precedence (listed in **descending order**) based on dependency chain is shown below :
  |Precedence|file|comments|
  |---|---|---|
  ||**config/local.properties**|Overrides property from all extensions |
  |&#129033;| ...||
  |&#129033;|commercefacades/project.properties|Overrides property in its dependency commerceservices extension|
  |&#129033;|commerceservices/project.properties|Overrides property in its dependency basecommerce extension|
  |&#129033;|basecommerce/project.properties|Overrides property in platform extension|
  |&#129033;|platform/project.properties||

> **Conclusion** : Each project.properties overrides preceding ones in build / load order to determine system configuration. <br> Lastly, local.properties overrides all the others.

#### Summary on properties files:

- **Location** of config files:
  - Files **project.properties** and **extensioninfo.xml** are in each extension's base folder.
  - Files **local.properties** and **localextensions.xml** are in **hybris/config** folder.
- If you modify the **local.properties** or **project.properties** file :
  - **Restarting SAP commerce** server using **hybrisserver** is enough to reflect the change, and there is **no need to rebuild** SAP Commerce.
  - **Special case:** If we change any Tomcat related configuration settings like port, we need to:
    - invoke **ant server** target that copies settings to Tomcat installation, or
    - simply call **ant all** - it includes **build** and **server** targets.
- It is possible to check or dynamically change the properties at runtime in HAC.
  - However, the changed value will be reset after a server restart.

#### localextensions.xml: Load Required Extensions.

- It is used to determine the list of extensions used by the build framework.
- To configure extensions in the **local.extensions.xml** file :

  1.  We can specify the required extensions **explicitly by specifying the complete path** referring to the extension folder.

      ```xml
        <extensions>
          <extension dir="${HYBRIS_BIN_DIR}/ext-commerce/basecommerce"/>
        </extensions>
      ```

  2.  Or, we can use a **look up folder** and its nested subfolders, defined by their **path** tag.<br>
      <ul><li>This allows extensions to be loaded by name rather that path.</li><li>Also supports <b>lazy loading</b> because SAP Commerce searches path directories for any extension referenced by another extension, and pulls it into the current configuration automatically.</li></ul>

      - Example :

      ```xml
      <extensions>
        <path dir="${HYBRIS_BIN_DIR}">
        <extension name="commerceservices"/>
      </extensions>
      ```

      - Here, as the _commerceservices_ extension also depends on other extensions such as _basecommerce_, _payment_ and so on, those extensions are also pulled into the configuration even though they are not specified.

  3.  In addition, it is also possible to autoload entire extension directions with the **path** tag, and limit lookup to specific directories by using the **path autoload="true"** parameter and **depth** parameter.
      <ul><li>OOTB, the path parameter in localextensions.xml points to the <b>hybris/bin</b> folder without using the autoload option.</li><li><em>Be careful not to load more extensions than necessary</em>.</li></ul>

      - Example :

      ```xml
      <extensions>
        <path autoload="true" dir="${HYBRIS_BIN_DIR}/ext-backoffice" depth="3">
        <path dir="${HYBRIS_BIN_DIR}">
        <extension name="commerceservices"/>
        ...
      </extensions>
      ```

      - Here, in the first path, **autoload="true"** states that all extensions within the _ext-backoffice_ folder, **except** those found in subdirectories more than 3 levels deep.
      - The second path points to the hybris/bin folder and implies that all extensions listed after it (like _commerceservices_, here) will be loaded.

- Finally, when we start the SAP Commerce server, all loaded extensions will be listed in the console log.
- We can notice that all the dependency extensions are loaded before the dependent extension.

---

Next Lesson: [Recognizing SAP Commerce Server Features](J01U02T04-Recognizing-SAP-Commerce-Server-Features.md)

Learning Journey: [Exploring the Technical Essentials of SAP Commerce Cloud](..)
