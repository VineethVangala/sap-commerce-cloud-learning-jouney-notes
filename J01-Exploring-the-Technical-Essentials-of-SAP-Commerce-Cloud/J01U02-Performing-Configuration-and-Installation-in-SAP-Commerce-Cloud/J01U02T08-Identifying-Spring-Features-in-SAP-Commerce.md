## Identifying Spring Features in SAP Commerce Cloud

> ### Learning Objective
>
> - We will be able to identify the Spring features used in SAP Commerce Cloud that help you effectively manage your projects.

#### Spring Features in SAP Commerce

- In SAP Commerce Cloud, the Spring Framework takes care of object management, a key aspect of any Java-based application.
- SAP Commerce cloud is a very **complex** application. However, it is **not a monolithic** system.
- It is implemented in a **modular** way so that all complexity is divided into small and manageable parts.
- Spring's **Core Framework** manages these small manageable parts, configures them and puts them all together.
- Spring Framework has many features and consists of many subprojects like Spring Core, Spring MVC, Spring Transactions, Spring Security, Inversion of Control (IOC), etc.

#### Features of Spring Core Framework

- **Spring IoC Container** is a container offered by Spring Core that controls the life cycle of every class instance, including how they are initialized, how they all connect to one another.
- **Application Context** is the container which manages our class instances and resources. It can be further extended as needed.
- One of the main features that affect all systems using Spring, is **Inversion of Control (IoC)** , more specifically the **Dependency Injection**.

  - With IoC, we no longer are responsible for instantiating classes ad-hoc.

  ```java
   package com.example.spring;
   public class MyCustomerFacade{
       private CustomerSerice customerService = null;
       public MyCustomerFacade(){
           ❌customerService❌= new DefaultCustomerService();❌
       }

   }
  ```

  - Rather, the instances are managed by the **Application Context**, that allows us to configure declaratively which class instances or other resources are to be injected into which other class instances.

    ```xml
    <beans>
        <alias name="myCustomerFacade" alias="customerFacade"/>
        <bean id="myCustomerFacade" class="com.example.spring.MyCustomerFacade">

            <!-- Dependency Injection using setter method -->
            <property name="customerService" ref="customerService"/>
        </bean>
    </beans>
    ```

    ```java
    package com.example.spring;
    public class MyCustomerFacade{

        // This instance will be injected by Spring Container, via setter method
        private CustomerSerice customerService;

        // Spring Container injects the dependency using this setter method
        public void setCustomerService(CustomerService customerService)
        {
            this.customerService = customerService;
        }

        public MyCustomerFacade(){
            ...
        }

    }
    ```

- SAP Commerce Cloud uses **Spring MVC** for handling all interactions within a web application between **models, views, and their controllers**.
- We also use **Spring Security** for managing several aspects such as **Authentication** and **Authorization**, and all kinds of access control, secure communication to all web pages and web services, encryption of important data, and much more.
- SAP Commerce also benefits from **Spring Transaction Management**.
  - With that, any persistence-layer operation bounded by a Java method can be made transactional, thus, trating all of its constituent data manipulations as though they were a single, larger operation that either succeeds as a whole or not at all if any of its smaller steps fails.
  - This way, operations that are partially successful wont need to be cleaned up.
    ```java
    // Using @Transactional annotation to set the method as transactional
    @Transactional
    public void updateCustomerData(CustomerData customerData){
        customerService.updateCustomer(customerData);
    }
    ```

---

Next Lesson: [Getting an Overview of the Backoffice Framework](../J01U03-Understanding-Backoffice-Framework/J01U03T01-Getting-an-Overview-of-the-Backoffice-Framework.md)

Learning Journey: [Exploring the Technical Essentials of SAP Commerce Cloud](..)
