# Auto Bean Wiring of Spring


As we previously discussed that the Spring container is responsible for creating the beans in your application and coordinating the relationship between those objects vi DI. The act of creating these associations between application objects in the essence of dependency injection(DI) and is commonly referred to as wiring.

### Different Types of Bean Wiring
Spring Offers three primary wiring mechanism

  * An explicit configuration in XML
  * An explicit configuration in Java
  * An Implicit bean discovery and automatic wiring

In this post, I am going to write notes about Spring's automatic wiring, I will write about the other two in later posts.

### Automatically wiring beans
Spring attacks automatic wiring from two angles:

  * **Component scanning** - Spring automatically discovers beans to be created in the application context

  * **Autowiring** - Spring automatically satisfies bean dependencies

To understand those concepts properly we will create a project for an online store, let's create a new maven project first

![Create Maven Project](/images/create-maven-project.gif)

### Add Dependency

Now we need to add spring dependency to our `pom.xml` file

    <?xml version="1.0" encoding="UTF-8"?>
    <project xmlns="http://maven.apache.org/POM/4.0.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>

        <groupId>com.rimonmostafiz</groupId>
        <artifactId>spring-diary</artifactId>
        <version>1.0-SNAPSHOT</version>

        <dependencyManagement>
            <dependencies>
                <dependency>
                    <groupId>org.springframework</groupId>
                    <artifactId>spring-framework-bom</artifactId>
                    <version>5.0.6.RELEASE</version>
                    <type>pom</type>
                    <scope>import</scope>
                </dependency>
            </dependencies>
        </dependencyManagement>

        <dependencies>
            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-core</artifactId>
            </dependency>

            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-context</artifactId>
            </dependency>

            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-test</artifactId>
            </dependency>

            <dependency>
                <groupId>junit</groupId>
                <artifactId>junit</artifactId>
                <version>4.12</version>
                <scope>test</scope>
            </dependency>
        </dependencies>


    </project>

We are adding `spring-core`, `spring-context`, `spring-test`, and `junit`for our dependency for now.

Before going to the next part wait a minute and first think about an online store. Every online store has some items for sale, so the item is a dependency for a store.

So we need an item for our store. The following listing shows Item, an interface that defines an item for the store.

    package com.rimonmostafiz;

    public interface Item {
        void readyForSell();
    }

As we added Item as an Interface we can have several Item implementations. Let's add one implementation of `Item` for now called `FoodItem`

    package com.rimonmostafiz;

    import org.springframework.stereotype.Component;

    @Component
    public class FoodItem implements Item {

        String name = "Pizza";
        String price = "10.09$";

        public void readyForSell() {
            System.out.println(name + " is ready for sell at " + price);
        }
    }

`FoodItem` is a simple class which implements the Item interface. what is important is `FoodItem` is annotated with `@Component.`

### @Component

`@Component` Indicates that the annotated class is a "component". Such classes are considered as candidates for auto-detection when using annotation-based configuration and classpath scanning. This annotation tells spring container that a bean should be created for the class.

Now we need to write an explicit configuration to tell Spring to seek out all classes that are annotated with `@Component` and to create beans from them.
The configuration class in the following listing shows the minimal configuration to make this possible.

    package com.rimonmostafiz;

    import org.springframework.context.annotation.ComponentScan;
    import org.springframework.context.annotation.Configuration;

    @Configuration
    @ComponentScan
    public class StoreConfig { }

If we observe that `StoreConfig` doesn’t explicitly define any beans itself. Instead, it’s annotated with `@ComponentScan` to enable component scanning in Spring.
### @ComponentScan

The @ComponentScan annotation is used with the @Configuration annotation to tell Spring the packages to scan for annotated components.
@ComponentScan also used to specify base packages and base package classes using basePackages or basePackageClasses attributes of @ComponentScan.
@ComponentScan will default to scanning the same package as the configuration class.

Therefore, because `StoreConfig` is in the `com.rimonmostafiz` package, Spring will scan that package and any sub-packages underneath it, looking for classes that are annotated with `@Component` . It should find the Item class and automatically create a bean for it in Spring.

The above configuration class is same as the XML listed bellow


    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns:context="http://www.springframework.org/schema/context"
        xsi:schemaLocation="http://www.springframework.org/schema/beans
            http://www.springframework.org/schema/beans/spring-beans.xsd
            http://www.springframework.org/schema/context
            http://www.springframework.org/schema/context/spring-context.xsd">

        <context:component-scan base-package="soundsystem" />

    </beans>

In the above XML we are using Spring's `context`namespace to turn on component scanning via XML configuration. Even though XML is an option for enabling component scanning, I’m going to focus on using the preferred Java-based configuration for the remainder of this discussion.

To test that component scanning is working we can write a simple JUnit test that creates a Spring application context and asserts that the Item bean is, in fact, created.

    package com.rimonmostafiz;

    import org.junit.Test;
    import org.junit.runner.RunWith;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.test.context.ContextConfiguration;
    import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;

    import static org.junit.Assert.assertNotNull;

    @RunWith(SpringJUnit4ClassRunner.class)
    @ContextConfiguration(classes = StoreConfig.class)
    public class StoreTest {

        @Autowired
        Item foodItem;

        @Test
        public void foodItemIsNotNull() {
            assertNotNull(foodItem);
        }
    }

Here the `@ContextConfiguration` annotation tells it to load its configuration from the `StoreConfig`class. Because that configuration class includes `@ComponentScan` ,  the resulting application context should include the `Item` bean. To prove that, the test has a property of type `Item` that is annotated with `@Autowired` to inject the `Item` bean into the test.
Finally, a simple test method asserts that the foodItem property isn’t null. If it’s not null, that means Spring was able to discover the `Item` class, automatically create it as a bean in the Spring application context, and inject it into the test.

### @Autowired

Aautowiring is a means of letting Spring automatically satisfy a bean’s dependencies by finding other beans in the application context that are a match to the bean’s needs. To indicate that autowiring should be performed, we can use `@Autowired` annotation.



### Test
If you now run the test it will pass.
<iframe width="600" height="400" src="/videos/autowiring-test-spring-diary.mp4" frameborder="0" allowfullscreen></iframe>

