## Getting to Know the SAP Commerce Installer

> ### Learning Objective
>
> - We will be able to discover the available recipes to install and configure SAP Commerce Cloud.

#### The SAP Commerce Installer

- The modularity of SAP Commerce Cloud is its major advantage and lets us customize functionality by selecting extensions included in the suite.
- The SAP Commerce installer uses a set of **Gradle**-based projects written in **Groovy** with the intention of automating the installation steps of SAP Commerce Cloud.
  > Note: A fully audited manual installation is recommended instead when configuring a Production environment.
- Each Gradle-based project is an automated script called a **Recipe**.

#### Recipe

- A Recipe will install a particular flavor of SAP Commerce, with the desired build structure and configuration.
- A Recipe contains all the setup data needed to install a given configuration.
- Recipes will include
  - three mandatory tasks :
    1. Setup,
    1. Initialize,
    1. Start
  - calls to required plugins such as installer-platform-plugin.jar,
  - the local.properties configuration,
  - the required extensions,
  - the database configuration,
  - the web archives, and
  - the AppServer setup

#### Creating a new custom Recipe

1. Open the directory **{HYBRIS_HOME_DIR}/installer/recipes/**.
1. Create a new folder for the custom recipe, with name "**recipe_demo**". Note that the name of this folder will be the name of the recipe.
1. Copy existing **build.gradle** and **readme.txt** files from an existing recipe into the newly created recipe folder - **{HYBRIS_HOME_DIR}/installer/recipes/recipe_demo**.
1. We should update new property or other configuration changes into **build.gradle** file as per need.

   1. Open build.gradle in any text editor.
   1. Add the custom property and extentions as per requirement, and save the changes.

   ```gradle
   apply plugin:'installer-platform-plugin'
   apply plugin:'installer-addon2-plugin'

   def pl= platform{
        localProperties{
            property 'build.parallel','true'
            property 'initialpassword.admin','nimda'

            //Adding the new property here
            property 'demo.recipes','true'
        }
   }
   afterSetup{
    ensureAdminPasswordSet()
   }
   extensions{
    extName 'adaptivesearchsolr'
    extName 'solrserver'
    ...

   }

   ```

1. The new custom recipe changes are saved and is now ready for installation.

#### Installing a Recipe

- Open a command line window in the directory **{HYBRIS_HOME_DIR}/installer**.
- In Windows OS, run the following **install.bat -r {recipe_name}** command to install the recipe.

```console
install.bat -r recipe_demo
```

- Once the installation has finished successfully, we'll use this new recipe to initialize SAP Commerce by running the recipe's **initialize** command for Windows OS.

```console
install.bat -r recipe_demo initialize
```

- Once the initialization has finished successfully (which may take 15 minutes or so), we'll use this new recipe to startup SAP Commerce by running the recipe's **start** command for Windows OS.

```console
install.bat -r recipe_demo start
```

- Once the server startup has been completed, we can open the HAC in browser, log in as an admin, and validate if the new configuration change is reflecting.

---

Next Lesson: [Identifying Spring Features in SAP Commerce Cloud](..\J01U02-Performing-Configuration-and-Installation-in-SAP-Commerce-Cloud\J01U02T01-Examining-Build-Framework.md)

Learning Journey: [Exploring the Technical Essentials of SAP Commerce Cloud](..)
