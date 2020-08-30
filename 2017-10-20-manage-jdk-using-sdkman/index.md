# Manage JDK Using SDKMAN

### What is SDKMAN?

<blockquote>[SDKMAN!](http://sdkman.io/index.html) is a tool for managing parallel versions of multiple Software Development Kits on most Unix based systems. It provides a convenient Command Line Interface (CLI) and API for installing, switching, removing and listing Candidates. Its also open source. You can see the codes form [SDKMAN's github repository](https://github.com/sdkman).</blockquote>


If you are a developer then its very common that you work on multiple projects which use different JDK version. Obviously, you can use `update-alternatives` to manage multiple JDK libraries on the same system to select which one you want to use as the main one.

Did you ever tried the `update-alternatives` and then `java -version` was correct, but the link in `$JAVA_HOME` and `javac -version` was still wrong... and you changed that one manually?

Using SDKMAN you can manage this very easily. SDKMAN will make your life easy.


### How to Install SDKMAN?
Installing SDKMAN is quite easy. Simply open a new terminal and enter:

    $ curl -s "https://get.sdkman.io" | bash


Follow the instructions on-screen to complete the installation. Next enter:


    $ source "$HOME/.sdkman/bin/sdkman-init.sh"


And SDKMAN is installed. :D
Now run the following command to verify that your installation succeeded:

    $ sdk version
    SDKMAN 5.5.9+231

### Usages of SDKMAN

So SDKMAN is installed on your system, now what?
On your terminal run:

    $ sdk list java

Now in your terminal, a list will appear which will show available, local, installed and current versions of the SDK

    ================================================================================
    Available Java Versions
    ================================================================================
       + 9ea157                                                                        
     > * 9.0.1-oracle                                                                  
         9.0.0-zulu                                                                    
         8u151-oracle                                                                  
         8u144-zulu                                                                    
         8u131-zulu                                                                    
       + 7u80                                                                          
         7u141-zulu                                                                    
         6u93-zulu                                                                                                   
    ================================================================================
    + - local version
    * - installed
    > - currently in use
    ================================================================================

As you can see in my system JDK 7, and JDK 9 is installed, among them I installed JDK 7 using local version.

Now I want to install JDK 8 in my system, so first I need to downloaded Java SE Development Kit 8u152(you can choose any other version you like) from [Oracle JDK Download Page](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html). Then extract the folder and then run following command:

    $ sdk install java 8u152 /home/rimonmostafiz/Downloads/jdk1.8.0_152
    > Linking java 8u152 to /home/rimonmostafiz/Downloads/jdk1.8.0_152
    > Done installing!

    # for you, oviously you need to specify your jdk folder loacaion

It will install JDK 8 as a local version on the system. Actually, its linked to your JDK folder, if you delete this folder, then the link will be broken, so you have to keep it there(in my case in my download folder).
**There is another way to do it, which I follow, After extract the folder I copy the folder to**

    ~/.sdkman/candidates/java/

If you don't to want this download and linking hassle, The following command will install a latest stable version of java

    $ sdk install java

If you want to choose the version

    $ sdk install java 8u151-oracle

Make a given version the default:

    $ sdk default java 7u45

    # check java version
    $ java -version
    java version "1.7.0_80"
    Java(TM) SE Runtime Environment (build 1.7.0_80-b15)
    Java HotSpot(TM) 64-Bit Server VM (build 24.80-b11, mixed mode)

    # check javac version
    $ javac -version
    javac 1.7.0_80

    # chack JAVA_HOME
    $JAVA_HOME
    bash: /home/rimonmostafiz/.sdkman/candidates/java/current: Is a directory

To see the current version

    $ sdk current java
    Using java version 7u80

Now your default java version is JDK 7 and you are working on a project which is configured in JDK 8, and you need to compile the project JDK 8.
Go to the project directory and then open a terminal and enter:

    $ sdk use java 8u152
    <span style="color: #339966;">Using java version 8u152 in this shell.</span>

Now in the shell, JDK 8 is activated. You can compile your project in JDK 8 in this shell, your default version is not changed. :D

Check other SDKMAN Usages from [SDKMAN Site.](http://sdkman.io/usage.html)

Using SDKMAN you can manage not only JDK, can manage other SDK too. :D
Want to see which SDK you can also manage using SDKMAN
Run on your terminal

    $ sdk list
    # a list will appear

    ================================================================================
    Available Candidates
    ================================================================================
    q-quit                                  /-search down
    j-down                                  ?-search up
    k-up                                    h-help
    --------------------------------------------------------------------------------
    Groovy (2.4.5)                                       http://www.groovy-lang.org/

    Groovy is a powerful, optionally typed and dynamic language, with static-typing
    and static compilation capabilities, for the Java platform aimed at multiplying
    developers’ productivity thanks to a concise, familiar and easy to learn syntax.
    It integrates smoothly with any Java program, and immediately delivers to your
    application powerful features, including scripting capabilities, Domain-Specific
    Language authoring, runtime and compile-time meta-programming and functional
    programming.

                                                                $ sdk install groovy
    --------------------------------------------------------------------------------
    Scala (2.11.7)                                        http://www.scala-lang.org/
    ...


Visit [this link](http://sdkman.io/sdks.html) to see the SDK Installation Candidates.
Use SDKMAN and Enjoy. :D


#### UPDATE:
Sometimes when you use command `$ sdk version` or any other command you get

    ==== INTERNET NOT REACHABLE! ===================================================

     Some functionality is disabled or only partially available.
     If this persists, please enable the offline mode:

       $ sdk offline

    ================================================================================


Your internet is working fine but SDKMAN is saying INTERNET NOT REACHABLE :/
So how to solve this problem?
Go to your `.sdkman/etc` folder and open config file using any text editor you prefer
now change the following configurations as bellow and save the file


    sdkman_insecure_ssl=true
    sdkman_curl_connect_timeout=7
    sdkman_curl_max_time=10

After saving the file need to re-source the `sdkman-init.sh` or start a new terminal.

    source "$HOME/.sdkman/bin/sdkman-init.sh"

Now SDKMAN should work properly!

