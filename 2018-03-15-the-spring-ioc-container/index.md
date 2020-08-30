# The Spring IoC Container

There is some confusion these days over the meaning of _**inversion of control**_ due to the rise of _**IoC containers**_.

**An IoC container is a common characteristic of frameworks that implement Inversion of Control (IoC).**

Some people confuse the general principle here with the specific styles of inversion of control (such as dependency injection) that these containers use. It is a process whereby objects define their dependencies, that is, the other objects they work with, only through constructor arguments, arguments to a factory method, or properties that are set on the object instance after it is constructed or returned from a factory method. The container then __injects__ those dependencies when it creates the bean. This process is fundamentally the inverse, hence the name _Inversion of Control_ (IoC), of the bean itself controlling the instantiation or location of its dependencies by using a direct construction of classes, or a mechanism such as the _**Service Locator**_ pattern.

## Spring IoC Container

The container is at the core of the Spring Framework. Spring’s container uses DI to manage the components that make up an application. This container is responsible for instantiating, configuring and assembling objects known as _beans_, as well as managing their life-cycle.

Spring comes with several container implementations of IoC Container.
In Spring, `org.springframework.beans`and `org.springframework.context`packages are the basis of Spring's IoC Container.

  * **The [`BeanFactory`](https://docs.spring.io/spring-framework/docs/5.0.4.RELEASE/javadoc-api/org/springframework/beans/factory/BeanFactory.html)**: Defined by `org.springframework.beans.factory.BeanFactory` interface. It provides an advanced configuration mechanism capable of managing any type of object. It Provides the configuration framework and basic functionality.

  * **The [`ApplicationContext`](https://docs.spring.io/spring-framework/docs/5.0.4.RELEASE/javadoc-api/org/springframework/context/ApplicationContext.html)**: Defined by `org.springframework.context.ApplicationContext` interface. Its a sub-interface of `BeanFactory` It adds more enterprise-specific functionality like easier integration with Spring’s AOP features; message resource handling (for use in internationalization), event publication; and application-layer specific contexts.

## Overview of Container
The above interfaces represent the Spring IoC container and are responsible for instantiating, configuring, and assembling the aforementioned beans. The next question pop out from the brain, what the hack is a bean?

**Bean**

> Object in the Spring framework that we initialize through Spring container is called Spring Bean.
The objects that form the backbone of your application and that are managed by the __Spring IoC container__ are called __beans__.

>A bean is an object that is instantiated, assembled, and otherwise managed by a Spring IoC container. Otherwise, a bean is simply one of many objects in your application.Any normal __Java POJO__ class can be a Spring Bean if it’s configured to be initialized via container by providing configuration metadata information.

Now the questions are,
  1. How container loads the beans?
  2. How does the container know which beans to wire together?
  3. Is it happening magically?

Nothing is happening magically inside the container, In order to assemble beans, the container uses configuration metadata.
The container gets its instructions on what objects to instantiate, configure, and assemble by reading this configuration metadata. which can be represented in XML, Java annotations, or Java code. As an Application Developer, it's your job to write this configuration metadata.

![Container Magic](https://docs.spring.io/spring/docs/current/spring-framework-reference/images/container-magic.png)

The diagram is a high-level view of how Spring Container works. Your application classes are combined with configuration metadata so that after the `ApplicationContext` is created and initialized, you have a fully configured and executable system or application.

