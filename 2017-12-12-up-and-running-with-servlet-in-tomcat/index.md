# Up and Running With Servlet in Tomcat

{{< youtube id="lTyAPWR6104" >}}

First, let's create a maven project and add the dependency.
As a prerequisite, JDK 8 will be needed. If you are using Linux based operating system then I have written a post on how to install and manage different versions of JDK in your system. You can visit [this post](https://wp.me/p94Vft-cK) if JDK 8 is not installed on your system.


### Maven Dependency

    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>3.1.0</version>
        <scope>provided</scope>
    </dependency>

### Creating a servlet Class

In Java, a Servlet is what receives and responds to requests from the end user. The Java EE API specification defines a Servlet as follows:


<blockquote>A Servlet is a small Java program that runs within a Web server. Servlets receive and respond to requests from Web clients, usually across HTTP, the HyperText Transfer Protocol.</blockquote>


Every Servlet implements the `javax.servlet.Servlet interface`, but usually not directly. In almost all cases, Servlets inherit from `javax.servlet.GenericServlet`GenericServlet is still a protocol-independent Servlet with the lone, abstract service method, but it contains several helper methods for logging and getting information about the application and Servlet configuration.

For responding to HTTP-specific requests, `javax.servlet.http.HttpServlet` extends `GenericServlet` and implements the service method to accept only HTTP requests.


    import javax.servlet.ServletException;
    import javax.servlet.http.HttpServlet;
    import javax.servlet.http.HttpServletRequest;
    import javax.servlet.http.HttpServletResponse;
    import java.io.IOException;

    public class StartingServlet extends HttpServlet { }



Above service is already prepared to accept an HTTP request and respond to it with an`405 Method Not Allowed` error.

So let us override the _**doGet**_ method to add support for the HTTP method GET:


    import javax.servlet.ServletException;
    import javax.servlet.http.HttpServlet;
    import javax.servlet.http.HttpServletRequest;
    import javax.servlet.http.HttpServletResponse;
    import java.io.IOException;

    public class StartingServlet extends HttpServlet {
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           resp.getWriter().println("Hello");
       }
    }

### Initializer and Destroyer

When a web container first starts a Servlet, it calls that Servlet’s init method. Later when the web container shuts down the Servlet, it calls the Servlet’s destroy method.

These methods are not the same as the Java constructor and finalizer, and they are not called at the same time as the constructor and finalizer. Normally, these methods do nothing, but you can override them to perform some action


    @Override
    public void init() throws ServletException {
         System.out.println("Servlet " + this.getServletName() + " has started.");
    }

    @Override
    public void destroy() {
        System.out.println("Servlet " + this.getServletName() + " has stopped.");
    }



init is called after the Servlet is constructed but before it can respond to the first request. Unlike when the constructor is called, when init is called all the properties have been set on the Servlet, giving you access to the ServletConfig and `javax.servlet.ServletContext` objects.

The init method is called when the Servlet starts. If the Servlet is configured to start automatically when the web application is deployed and started, that is when it is called. Otherwise, it is not called until the first request for that Servlet is received.
Likewise, destroy is called immediately after the Servlet can no longer accept any requests. This typically happens either when the web application is stopped or un-deployed or when the web container shuts down.


### Adding the Deployment Descriptor(web.xml)


It describes how the web application should be deployed.Its written In XML.
The deployment descriptor is a file which will be used by Application Server/Web Container. It directs a deployment tool to deploy a module or application with the specified security settings and describes other specific configuration requirements and/or container options.
The web application deployment descriptor is named `web.xml`, and when included with a web application, it must reside in a WEB-INF sub directory at the web application root.


    <?xml version="1.0" encoding="UTF-8" ?>
    <web-app
            xmlns="http://xmlns.jcp.org/xml/ns/javaee"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                                http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
            version="3.1">

        <display-name>java-web-app</display-name>

        <servlet>
            <servlet-name>startingServlet</servlet-name>
            <servlet-class>StartingServlet</servlet-class>
        </servlet>

        <servlet-mapping>
            <servlet-name>startingServlet</servlet-name>
            <url-pattern>/hello</url-pattern>
        </servlet-mapping>

    </web-app>


In the above file, we instructed the web container to create an instance of the Servlet we wrote earlier, using the `<servlet>` tag. And we used `<servlet-mapping>` tag to mapped the servlet. All requests to the application-relative URL _/hello_ will be handled by the startingServlet.


### pom.xml File

Final pom.xml file looks like this


    <?xml version="1.0" encoding="UTF-8"?>
    <project xmlns="http://maven.apache.org/POM/4.0.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>

        <groupId>com.rimonmostafiz</groupId>
        <artifactId>java-web-app</artifactId>
        <version>1.0-SNAPSHOT</version>

        <dependencies>
            <dependency>
                <groupId>javax.servlet</groupId>
                <artifactId>javax.servlet-api</artifactId>
                <version>3.1.0</version>
                <scope>provided</scope>
            </dependency>
        </dependencies>

        <build>
            <sourceDirectory>src/main/java</sourceDirectory>
            <resources>
                <resource>
                    <directory>src/main/resources</directory>
                </resource>
            </resources>

            <testSourceDirectory>src/test/java</testSourceDirectory>
            <testResources>
                <testResource>
                    <directory>src/test/resources</directory>
                </testResource>
            </testResources>

            <plugins>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-war-plugin</artifactId>
                    <version>3.0.0</version>
                    <configuration>
                        <warSourceDirectory>web</warSourceDirectory>
                    </configuration>
                </plugin>

                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-compiler-plugin</artifactId>
                    <version>3.6.1</version>
                    <configuration>
                        <source>1.8</source>
                        <target>1.8</target>
                    </configuration>
                </plugin>
            </plugins>
        </build>


    </project>


Now If you want to run this in tomcat then I have made a video how to create this whole project and configure tomcat in IntelliJ-IDEA to run this. Check the video from the top of the post.

I am not an expert, I already told That I'm just documenting my learning. So If you find any anomaly feel free to add a comment. Also, any queries, thoughts, and suggestions will be appreciated.

