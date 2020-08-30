# A Bit of Spring


## Spring MVC Java Configuration

Spring traditionally supports two types of configurations:

  * XML based configuration
  * Annotation-based configuration

This post is about a bare minimum annotation-based configuration of spring MVC.

#### 1. Maven Dependencies

    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-framework-bom</artifactId>
                <version>5.0.1.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
        </dependency>

        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>4.0.0-b02</version>
        </dependency>
    </dependencies>

#### 2. Configure DispatcherServlet

    package com.rimonmostafiz.config;

    import org.springframework.web.servlet.support.AbstractAnnotationConfigDispatcherServletInitializer;

    public class WebAppInitializer extends AbstractAnnotationConfigDispatcherServletInitializer {

        protected String[] getServletMappings() {
            return new String[] {"/"};
        }

        protected Class<?>[] getServletConfigClasses() {
            return new Class<?>[] {RootConfig.class};
        }

        protected Class<?>[] getRootConfigClasses() {
            return new Class<?>[] {WebConfig.class};
        }
    }



In a Servlet 3.0, If an application has any class in the classpath which implements  `javax.servlet.ServletContainerInitializer` interface, then that class is used to configure the servlet container.

Spring has an implementation of that interface called `SpringServletContainerInitializer` which seeks out any classes that implement `WebApplicationInitializer` and delegates to them for configuration.

Spring 3.2 introduced a convenient base implementation of `WebApplicationInitializer` called `AbstractAnnotationConfigDispatcherServletInitializer.`

Because our `WebAppInitializer` Class extends `AbstractAnnotationConfigDispatcherServletInitializer` (and thus implements `WebApplicationInitializer`), it will be automatically discovered when deployed in a Servlet 3.0 container and be used to configure the servlet context.

WebAppInitializer overrides three methods. Let's talk about them a bit

**_getServletMappings() :_**

  * This method Identifies one or more paths that DispatcherServlet will be mapped to.
  * In this case, it’s mapped to "/", indicating that it will be the application’s default servlet.
  * It will handle all requests coming into the application.

**_getServletConfigClasses() :_**
  * When DispatcherServlet starts up, it creates a Spring application context and starts loading it with beans declared in the configuration files or classes that it’s given.
  * Here we are asking Dispatcher-Servlet to load its application context with beans defined in the WebConfig configuration class.

**_getRootConfigClasses() :_**
  * In Spring web applications, there’s often another application context.
  * This other application context is created by `ContextLoaderListener`
  * Whereas DispatcherServlet is expected to load beans containing web components such as controllers, view resolvers, and handler mappings, ContextLoaderListener is expected to load the other beans in your application.
  * These beans are typically the middle-tier and data-tier components that drive the back end of the application.

#### 3. Enable Web MVC and WebConfig.class

    package com.rimonmostafiz.config;

    import org.springframework.context.annotation.Bean;
    import org.springframework.context.annotation.ComponentScan;
    import org.springframework.context.annotation.Configuration;
    import org.springframework.web.servlet.ViewResolver;
    import org.springframework.web.servlet.config.annotation.DefaultServletHandlerConfigurer;
    import org.springframework.web.servlet.config.annotation.EnableWebMvc;
    import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;
    import org.springframework.web.servlet.view.InternalResourceViewResolver;

    @Configuration
    @EnableWebMvc
    @ComponentScan({"com.rimonmostafiz"})
    public class WebConfig implements WebMvcConfigurer {

        @Bean // configure a jsp view resolver
        ViewResolver viewResolver() {
            InternalResourceViewResolver resolver = new InternalResourceViewResolver();
            resolver.setPrefix("/WEB-INF/views/");
            resolver.setSuffix(".jsp");
            resolver.setExposeContextBeansAsAttributes(true);
            return resolver;
        }

        public void configureDefaultServletHandling(DefaultServletHandlerConfigurer configurer) {
            configurer.enable();
        }
    }

WebConfig class is annotated with

  * _**@Configuration**_ as it is a configuration class, It indicates that a class declares one or more `@Bean` methods and may be processed by the Spring container to generate bean definitions and service requests for those beans at runtime
  * _**@EnableWebMvc**_ as we are using java configuration so we are using this annotation to enable Spring MVC.
  * _**@ComponentScan**_ so that the `rimonmostafiz.web` package will be scanned for components.


We have added a ViewResolver bean. It’s an InternalResourceViewResolver.
It’s configured to look for JSP files by wrapping view names with a specific prefix and suffix.
Here, prefix = "/WEB-INF/views/" and suffix = ".jsp"

WebConfig class implements `WebMvcConfigurer` and overrides its `configureDefaultServletHandling()` method.
By calling `enable()` on the given `DefaultServletHandlerConfigurer`, we are asking DispatcherServlet to forward requests for static resources to the servlet container’s default servlet and not to try to handle them itself.


#### 4. Minimum RootConfig.class

    package com.rimonmostafiz.config;

    import org.springframework.context.annotation.ComponentScan;
    import org.springframework.context.annotation.Configuration;
    import org.springframework.context.annotation.FilterType;
    import org.springframework.web.servlet.config.annotation.EnableWebMvc;

    @Configuration
    @ComponentScan(basePackages={"rimonmostafiz"},
            excludeFilters={@ComponentScan.Filter(type= FilterType.ANNOTATION, value=EnableWebMvc.class)})
    public class RootConfig {}

