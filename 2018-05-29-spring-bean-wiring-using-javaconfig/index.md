# Spring Bean Wiring Using Javaconfig

In the [previous post](https://rimonmostafiz.com/post/auto-bean-wiring-of-spring/), I wrote about how can we implicitly wire beans automatically in Spring container. In my previous post I created a new maven project and started writing code so that we can understand the topics more clearly. In this post, I am documenting my learning of how we can wire bean using Explicit Java Configuration. I will work on the same project I have created earlier.

### Explicit wiring using Java

When an automatic configuration isn’t an option then we must configure Spring explicitly. Let’s say that we want to wire components from some third-party library into our application. Because we don’t have the source code for that library, there’s no opportunity to annotate its classes with `@Component` and `@Autowired` annotations. Therefore, automatic configuration isn’t an option.

We have two choices for explicit configuration:
* Java
* XML

JavaConfig is the preferred option for explicit configuration because it’s more powerful, type-safe, and refactor-friendly.

### Create a configuration class

To wire bean in JavaConfig, we need to create a Configuration Class and mark that with `@Configuration` annotation.

This annotation identifies this class as a configuration class, and it’s expected to contain details of beans that are to be created in the Spring application context.

    package com.rimonmostafiz;

    import org.springframework.context.annotation.Bean;
    import org.springframework.context.annotation.Configuration;

    @Configuration
    public class StoreConfig { }

### Declare A Bean
To declare a bean in JavaConfig, we should create a method in our configuration class and creates an instance of the desired class and annotate the method with `@Bean`

    package com.rimonmostafiz;

    import org.springframework.context.annotation.Bean;
    import org.springframework.context.annotation.Configuration;

    @Configuration
    public class StoreConfig {
        @Bean
        Item foodItem() {
            return new FoodItem();
        }
    }

Here the `@Bean` annotation tells spring that this method will return an object and that should be registered as a bean in the Spring application context.

By default, the bean will be given an Id same as the method name annotated with `@Bean`. If we want to give the bean a different name then we can supply a name attribute in `@Bean` annotation like the example below

    package com.rimonmostafiz;

    import org.springframework.context.annotation.Bean;
    import org.springframework.context.annotation.Configuration;

    @Configuration
    public class StoreConfig {
        @Bean(name = "myFoodItemBean")
        Item foodItem() {
            return new FoodItem();
        }
    }

### Inject Bean in JavaConfig

So we Created a simple Item bean. It was simple and easy as It wasn't dependent on any other bean.  
But now we are going to declare a Store bean which is dependent on Item bean. How to do it in JavaConfig?

    package com.rimonmostafiz;

    import org.springframework.context.annotation.Bean;
    import org.springframework.context.annotation.Configuration;

    @Configuration
    public class StoreConfig {
        @Bean(name = "myFoodItemBean")
        Item foodItem() {
            return new FoodItem();
        }

        @Bean
        Store store() {
            return new Store(foodItem());
        }
    }

Here our `store()`method is similarly annotated with `@Bean` to indicate that it will produce an instance of a bean to be registered in the Spring application context.
As no name attribute is present in `@Bean` so by default the bean name will be store, the same as the method's name.

The body of the method is different from the `foodItem()` method. The store instance is created by calling its constructor that takes a Item. It appears that the Item is provided by calling `foodItem` , but that’s not exactly true. Because the `foodItem()` method is annotated with `@Bean` , Spring will intercept any calls to it and ensure that the bean produced by that method is returned rather than allowing it to be invoked again.
For example, we want to introduce another Store bean that is just like the first one.

    @Bean
    Store store() {
        return new Store(foodItem());
    }

    @Bean
    Store anotherStore() {
        return new Store(foodItem());
    }

Now here things get little tricky. If the call to `foodItem()` was treated like any other call to a Java method, then each store would be given its own instance of `FoodItem`.
If you have two Store, there’s no physical way for a single item to simultaneously be present in two stores. Right?
In software, however, there’s no reason you couldn’t inject the same instance into as many other beans as you want. By default, all beans in Spring are singletons, and there’s no reason you need to create a duplicate instance for the second Store bean. So Spring intercepts the call to `foodItem()` and makes sure that what is returned is the Spring bean that was created when Spring itself called `foodItem()` to create the Store bean. Therefore, both our Store beans will be given the same instance of `FoodItem`.

Referring to a bean by calling its method can be confusing. There’s another way that might be easier to digest:

    @Bean
    Store store(Item foodItem) {
        return new Store(foodItem);
    }


Here, the `store()` method asks for an Item as a parameter. When spring calls `sotre()` to create a Store bean, it autowire an Item into the configuration method. This approach is to refer to other beans is usually the best choice because it doesn't depend on the Item bean being declared in the same configuration class. In fact, you can even declare Item bean in XML configuration or automatically scanned and wired beans. No matter how its created spring will hand it to this configuration method to create the Store bean.

### Run Application

Let's test all this java configuration by creating an `App` class.

**App.class Code**

    package com.rimonmostafiz;

    import org.springframework.context.ApplicationContext;
    import org.springframework.context.annotation.AnnotationConfigApplicationContext;

    public class App {
        public static void main(String[] args) {
            ApplicationContext context = new AnnotationConfigApplicationContext(StoreConfig.class);
            Store store = (Store) context.getBean("store");
            store.showNotice();
        }
    }

