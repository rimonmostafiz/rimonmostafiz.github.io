# Basic Web Application Structure of JavaEE

### Basic Web Application Structure

A lot of components go into making a Java EE application.

  * Application Code and Third Party Libraries it depends on
  * `Deployment Descriptor`, which includes instructions for deploying and starting the application
  * `ClassLoders` which is responsible for isolating your application form other web applications on the same server
  * Finally the `WAR` and `EAR` files

### Servlets, Filters, Listeners, and JSPs
  * `Servlets` are a key component of any Java EE applications. Servlets are Java classes responsible for accepting and responding to the HTTP request.

  * Nearly every request to your application goes through a Servlet of some type, except those requests that are erroneous or intercepted by some other component. `Filter` is one such component that can intercept requests to your Servlets.

  * Java EE web applications support various types of `listeners`, which can notify your code of multiple events, such as application startup, application shutdown, HTTP session creation, and session destruction.

  * And finally, we have `jsp(JavaServer Pages)`, which provides you with the means to easily create dynamic, HTML based graphical user interfaces for web applications.

