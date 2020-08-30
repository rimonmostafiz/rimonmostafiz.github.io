# Web Application Directory Structure and WAR Files

Standard Java EE web applications are deployed as **WAR** files or **exploded (unarchived)** web application directories. All Java EE web application servers support WAR file application archives. Whether archived or exploded, the directory structure convention, as shown in Figure is the same.

![Directory Structure](/images/directory-structure.jpg)

  * This structure contains classes and other application resources, the class files live in **_/WEB-INF/classes_**. The **WEB-INF** directory stores informational and instructional files that Java EE web application servers use to determine how to deploy and run the application. Its classes directory acts as the package root. All compiled application class files and other resources live within this directory.

  * WAR files can contain bundled JAR files, which live in _**/WEB-INF/lib.**_ All the classes in the JAR files in this directory are also available to the application on the application’s classpath.

  * The _**/WEB-INF/tags**_ and **_/WEB-INF/tld_** directories are reserved for holding JSP tag files and tag library descriptors, respectively.

  * The _**i18n**_ directory is not actually part of the Java EE specifications, but it is a convention that most application developers follow for storing internationalization (_**i18n**_) and localization (_**L10n**_) files.

  * There are two different _**META-INF**_ directories.

    * The root-level _**/META-INF**_ directory contains the application manifest file. This directory is not on the application classpath. You cannot use the ClassLoader to obtain resources in this directory.
    It contains resources for specific web containers or application servers.<br>
    For example, Apache Tomcat looks for and uses a _context.xml_ file in this directory to help customize how the application is deployed in Tomcat. None of these files are part of the Java EE specification, and the supported files can vary from one application server or web container to the next.

    * _**WEB-INF/classes/META-INF**_ is on the classpath. Any application resources you desire in this directory, and they become accessible through the ClassLoader.<br>
    Some Java EE components specify files that belong in this directory.<br>
    For example, the Java Persistence API specifies two files, _persistence.xml_, and _orm.xml_ — that live in _**/WEB-INF/classes/META-INF**_.

Most files contained within a **WAR** file or **exploded** web application directory are resources directly accessible through a URL.
For example, the file _/bar.html_ relative to the root of an application deployed to _http://example.org/foo_ is accessible from _http://example.org/foo/bar.html_.

In the absence of any filter or security rules to the contrary, this holds true for all resources in your application except those resources under the _**/WEB-INF**_ and _**/META-INF**_ directories. The files in these directories are protected resources that are not accessible via URL.

