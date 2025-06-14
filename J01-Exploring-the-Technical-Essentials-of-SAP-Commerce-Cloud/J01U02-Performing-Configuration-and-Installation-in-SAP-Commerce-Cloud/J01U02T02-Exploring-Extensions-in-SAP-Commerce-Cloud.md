## Exploring Extensions in SAP Commerce Cloud

> ### Learning Objective
>
> - To explore the ways to create and modify extensions in SAP Commerce Cloud for your data model and business logic.

#### Extensions in SAP Commerce Cloud

- Extensions serve as the **building blocks** of SAP Commerce Cloud.
- They support out-of-the-box, custom, and new functionalities for your implementations.

#### Where to begin SAP Commerce Cloud development?

- Starting any new project involves creating one or more extensions.
  - Each extension will contribute a part of the greater whole, including modifying or adding to the data model, business logic, backoffice tools configuration, web application, APIs etc.
  - The Extension approach will allow our **custom project code to remain separate** from SAP Commerce's standard framework code.
    - This facilitiates code reuse, and simplifies migration to future versions of SAP Commerce.
  - SAP Commerce bundles a **proprietary code generator** that can create a new extension.
- Extensions are the **packaging mechanism** for SAP Commerce cloud features.
- Everything, from the platform to user-customized functionality is packaged as extensions.
- **Template extensions** are the predefined out-of-the-box extensions meant to be duplicated as a starting point for creating a new extension.
- An extension contains predefined directories and files that organize its content.
- The Structure of a common extension is as follows:
  1. a **src** source directory contains **business logic** implementation, such as Java source files.
  2. a **classes** directory is automatically generated during the build process to store the **compiled Java classes**.
  3. the **lib** library directory is used to store external **third party libraries**, usually packaged as **jar files**.
  4. the **resources** directory contains SAP Commerce-related configuration data such as :
     - impexs,
     - type definition,
     - localozation files,
     - **{extensionname}-items.xml** - this is the type definition file used to define the extension's custom data model.
     - **{extensionname}-spring.xml** - this is the file used to configure the customizations's spring context
     - **{extensionname}-beans.xml** - this is the file used to add data transfer object beans.
  5. the **testsrc** test source directory contains JUnit Java source files of unit and integration tests.
  6. **build.xml** and **buildcallbacks.xml** are used by the Apache Ant build framework by providing parameters for Platform's build file, and to implement custom build framework logic, repectively.
  7. **extensioninfo.xml** contains the extension specific configuration.
  8. **external-dependencies.xml** file is used to configure external dependencies for the extension.
  9. the **web** directory contains the webmodule components like JSP files and libraries.
  10. **project.properties** file is used to store configuration properties of the extension to be used in the server.

#### Where to begin SAP Commerce Cloud development?

- **Extensions should not be created manually**.
- Instead, use **ant extgen** to programtically create an extension based on a predefined template.
- We need to select a template that suits the purpose. For example-

  - yempty is one of the most frequestly used templates, and is used to create an extension with minimal configuration.
  - yocc can be chosen to create an OCC extension.
  - ybackoffice provides the structure for a custom backoffice extension.
  - yhacext adds custom functionality to HAC.

- To create a single extension, we need to invoke **ant extgen**.

```console
> cd hybris/bin/platform
> setantenv.bat
> ant extgen
  > select extension template = yempty
  > select extension name = training
  > select package name = org.training
#Build Successful.
```

- After an extension is generated,

  - we should reference any extensions it requires in its **extensioninfo.xml**.
  - we should add the extension to **config/localextensions.xml**.

    ```xml
    <hybrisconfig>
    <extensions>
    ...
    ...
    <extension name="training"/>
    </extensions>
    </hybrisconfig>
    ```

  - invoke ant all to build changes.
    ```console
    #Triggering platform build in same console where ant extgen was run
    #cd hybris/bin/platform
    > ant all
    > hybrisserver.bat
    ```

---

- Most extensions use a template like:
  |Template|Description|
  |---|---|
  |**yempty**| The copy serves as starting point for creating a new extension, typically used for customer specific implementations.|
  |**yocc**|It serves as a starting point for creating a new extensions for Commerce Web Services, with minimal implementations necessary to create OCC Extension.|
  |yoccaddon|It serves as a starting point for creating a new AddOn for Commerce Web Services, and is essentially an empty extension with minimal implementations needed to create an AddOn.|
  |**ybackoffice**|It is used to create a custom backoffice extension.|
  |**yaddon**|It serves as a starting point for creating a new AddOn, with the most typical use-case being for customer-specific implementations.|
  |ycommercewebservices|It exposes part of the Commerce Facades as REST-based web services, including calls for product search and product details, and was created to enable third parties to extend and customize Web services using the addon concept.|
  |yhacext|It allows us to add your own functionalities to SAP Commerce Administration Console.|
  |yvoid| It is a simpler alternative for the yempty extension template.|
  |yacceleratorcore|It is the template business layer extension for your project|
  |yacceleratorfacades|It is a starting point template for a project to extend the functionality provided by the commercefacades extension. It enables you to add additional project-specific facades, as well as extending or adding further data objects, customizing, or adding new converters and adding additional populators.|
  |yacceleratorstorefront|It is a template for a ready-to-be-adapted web frontend. It uses the Spring MVC.|
  |yacceleratorcockpits|It is a template extension that demonstrates how a project can apply software customization to one or more existing cockpits without needing to create a project specific versions of a cockpit using the ycockpit template.|
  |yacceleratorinitialdata|It provides a framework for your B2C store and sites. It also provides an option to import the sample data|
  |yacceleratortest|It provides testing tools, configuration, and data for the SAP Commerce Accelerator.|
  |yacceleratorordermanagement|It is a template extension thats main orchestration is for orders, shipments and returns. This includes order workflow, order cancellation and order update, shipment workflow, pick, pack, ship, cancel, decline, split, reallocate, sourcing, return workflow, cancel, auto/manual refund, and return reviews.|
  |yacceleratorfulfilmentprocess||
  |yatddtests||
  |ycommercewebservicestest|It is used to enable third parties to extend and extension provides a set of tests written in Groovy that are intended to test ycommercewebservices REST calls.|
  |ydocumentcart|It allows us to store selected types in an alternative storage. It uses the polyglot persistence query language.|
  |yocctests|It is used to generate a new testing extension and provides manual and integration tests that allow for testing all functionality of the OCC Extension.|

[Available Extension Templates](https://help.sap.com/docs/SAP_COMMERCE/b490bb4e85bc42a7aa09d513d0bcb18e/f3e96825c2f647be93191293bf8533cf.html)

---

Refer: [About Extensions](https://help.sap.com/docs/SAP_COMMERCE/b490bb4e85bc42a7aa09d513d0bcb18e/8b49cab88669101489be9ac91a5f1ebb.html)

---

Next Lesson: [Examining the Build Framework](..\J01U02-Performing-Configuration-and-Installation-in-SAP-Commerce-Cloud\J01U02T01-Examining-Build-Framework.md)

Learning Journey: [Exploring the Technical Essentials of SAP Commerce Cloud](..)
