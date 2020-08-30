# Inversion of Control and Dependency Injection


### Inversion of control (IoC)

In software engineering, inversion of control (IoC) is a design principle. It is used to invert different kinds of controls. More Specifically invert the control of your custom written program or objects of a program is transferred to a container or framework.

In traditional programming, our custom code that expresses the purpose of the program calls reusable libraries to take care of generic tasks, but with inversion of control, it is the framework that calls into the custom, or task-specific, code.

IoC is sometimes referred to as the **Hollywood Principle** (_"Don't call us, we'll call you"_). Simply the flow of control of an application is not controlled by the application itself, but rather by the underlying framework.

#### Example of IoC
Suppose you drive a car to your workplace, it means you control the car. IoC principle suggests to invert the control, meaning instead of driving the car yourself, you hire a cab where another person will drive the car. Thus it is called inversion of the control from you to the cab driver. You don't have to drive a car yourself and let the driver do the driving so that you can focus on your main work.

Inversion of Control can be achieved through various mechanisms such as: Strategy design pattern, Service Locator pattern, Factory pattern, and Dependency Injection (DI).

### Dependency Injection(DI)
In software engineering, dependency injection is a technique whereby one object supplies the dependencies of another object.

Dependency Injection was originally called Inversion of Control (IoC). The normal control sequence would be the object finds the objects it depends on by itself and then calls them. Here, this is reversed: The dependencies are handed to the object when it's created. This also illustrates the **Hollywood Principle** at work: Don't call around for your dependencies, we'll give them to you when we need you.

The Inversion of Control (IoC) and Dependency Injection (DI) patterns are all about removing dependencies from your code.

One of the purposes of Dependency Injection is to reduce coupling in your application to make it more flexible and easier to test.


#### Example Of DI
Say you have A **_Repository_** class which responsible for handing over data to you from a **_Datasource_**. We need to instantiate an implementation of the **_Datasource_** Interface within the **_Repository_**.

    public class Repository {
        private Datasource dataSource;

        public Repository () {
            this.dataSource = new Datasource();
        }
    }

The **_Repository_** could establish a connection to the _**Datasource**_ by itself. But what if it allowed you to pass in a connection to the _**Datasource**_ through the _**Repository's**_ constructor?

    public class Repository {

        private Datasource dataSource;

        public Repository (Datasource dataSource) {
            this.dataSource = dataSource;
        }
    }


In the first code example, we are instantiating **Datasource**

    this.dataSource = new Datasource();

which means the _**Repository**_ class directly depends on the _**Datasource**_ class.

In the second code example, we are creating an abstraction by having the **Datasource** dependency class in **Repository** constructor signature (not initializing dependency in class).
This allows us to call the dependency then pass it to the **Repository** class like below

    Datasource dc = new MySqlDataSource(); // dependency
    Repository rep = new Repository(dc);   // caller is injecting dependency

Now the client creating the _**Repository**_ class has the control over which _**DataSource**_ implementation to use because we're injecting the dependency to the _**Repository**_.

You have just _inverted control_ by handing the responsibility of creating the connection from the _**Repository**_ class to the caller.

**Martin Fowler** suggests using the term "_Dependency Injection_" to describe this type of Inversion of Control since Inversion of Control as a concept can be applied more broadly than just injecting dependencies in a constructor method.
I don't think anyone can explain it better than Martin Fowler does, further down [the article you linked to.](http://www.martinfowler.com/articles/injection.html)

