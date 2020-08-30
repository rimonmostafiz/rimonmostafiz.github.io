# Spring Application Context and Configuration Metadata


In the [last post](https://rimonmostafiz.com/post/auto-bean-wiring-of-spring/) of Spring Diary, we discussed the basics of spring IoC Container and we saw a high-level view of how Spring Container works.

In this post, we will learn about how can we Instantiate a Spring IoC container(using `ApplicaitonContext` Interface) and configure that container using configuration metadata.

Spring IoC container consumes a form of configuration metadata. This configuration metadata represents how you as an application developer tell the Spring container to instantiate, configure, and assemble the objects in your application.

We have three choices to configure container using configuration metadata

  * **XML-based configuration:** Configuration metadata is traditionally supplied in a simple and intuitive XML format. Spring configuration consists of at least one and typically more than one bean definition that the container must manage. XML-based configuration metadata shows these beans configured as `<bean/>` elements inside a top-level `<beans/>` element.

  * **[Annotation-based configuration](https://docs.spring.io/spring/docs/current/spring-framework-reference/core.html#beans-annotation-config):** Spring 2.5 introduced support for annotation-based configuration metadata.

  * **[Java-based configuration](https://docs.spring.io/spring/docs/current/spring-framework-reference/core.html#beans-java):** Starting with Spring 3.0, many features provided by the Spring JavaConfig project became part of the core Spring Framework. Thus you can define beans external to your application classes by using Java rather than XML files.


## Basic Structure of XML-based Configuration
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

        <bean id="..." class="...">
        <!-- collaborators and configuration for this bean go here -->
        </bean>  

        <bean id="..." class="...">
        <!-- collaborators and configuration for this bean go here -->
        </bean>

        <!-- more bean definitions go here -->
    </beans>

The above example shows the basic structure of XML-based configuration metadata, where The attribute`id` is a string that you use to identify the individual bean definition. The attribute`class` defines the type of the bean and uses the fully qualified class name. The value of the id attribute refers to collaborating objects.

## Instantiating a container using the application context

Spring comes with several flavors of the application context. Here are a few that you’ll most likely encounter:

  * **AnnotationConfigApplicationContext:** Loads a Spring application context from one or more Java-based configuration classes

  * **AnnotationConfigWebApplicationContext:**  Loads a Spring web application context from one or more Java-based configuration classes

  * **ClassPathXmlApplicationContext:** Loads a context definition from one or more XML files located in the classpath, treating context-definition files as class-path resources

  * **FileSystemXmlApplicationContext:** Loads a context definition from one or more XML files in the filesystem

  * **XmlWebApplicationContext:** Loads context definitions from one or more XML files contained in a web application


Let's see first how can we load beans from `FileSystemXmlApplicationContest` and from the application’s `classpath` using `ClassPathXmlApplicationContext`, both of them are quite similar

    ApplicationContext context = new FileSystemXmlApplicationContext("/home/rimonmostafiz/Projects/spring-diary/beans.xml");

    ApplicationContext context = new ClassPathXmlApplicationContext("service.xml", "daos.xml");

The following example shows the service layer objects `(services.xml)` configuration file:

        <?xml version="1.0" encoding="UTF-8"?>

        <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
              http://www.springframework.org/schema/beans/spring-beans.xsd">

          <!-- services -->

          <bean id="petStore" class="org.rimonmostafiz.samples.jpetstore.services.PetStoreServiceImpl">
              <property name="accountDao" ref="accountDao"/>
              <property name="itemDao" ref="itemDao"/>
              <!-- additional collaborators and configuration for this bean go here -->
          </bean>

          <!-- more bean definitions for services go here -->

        </beans>

The following example shows the data access objects `daos.xml` file:

    <?xml version="1.0" encoding="UTF-8"?>

    <beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans.xsd">

      <bean id="accountDao"
          class="org.rimonmostafiz.samples.jpetstore.dao.jpa.JpaAccountDao">
          <!-- additional collaborators and configuration for this bean go here -->
      </bean>

      <bean id="itemDao" class="org.rimonmostafiz.samples.jpetstore.dao.jpa.JpaItemDao">
          <!-- additional collaborators and configuration for this bean go here -->
      </bean>

      <!-- more bean definitions for data access objects go here -->

    </beans>

In the preceding example, the service layer consists of the class `PetStoreServiceImpl`, and two data access objects of the type `JpaAccountDao` and `JpaItemDao` (based on the JPA Object/Relational mapping standard). The `property name` element refers to the name of the JavaBean property, and the `ref` element refers to the name of another bean definition. This linkage between `id` and `ref` elements expresses the dependency between collaborating objects.

Now if we want to load application context from a Java configuration, we can use `AnnotationConfigApplicationContext`, Instead of specifying an XML file from which to load the Spring application context, `AnnotationConfigApplicationContext` loads configuration metadata from a configuration class

    ApplicationContext context = new AnnotationConfigApplicationContext(com.rimonmostafiz.springdiary.config.AppConfig.class);

Instead of specifying an XML file from which to load the Spring application context,
`AnnotationConfigApplicationContext` has been given a configuration class from
which to load beans. With an application context in hand, we can retrieve beans from the Spring container by calling the context’s `getBean()` method.

