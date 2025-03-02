## What is spring Ioc Container?

The Spring IoC Container is the core of the Spring Framework, responsible for managing the lifecycle and dependencies of objects in a Spring application. It implements the Inversion of Control (IoC) principle, meaning that the container takes control of object creation and dependency injection, instead of the programmer manually managing them.

## What are the key responsibilities of IoC Container?

1. **Object Creation** – Instantiates beans (objects) defined in configuration.
2. **Dependency Injection** – Injects dependencies automatically.
3. **Lifecycle Management** – Initializes, configures, and destroys beans.
4. **Configuration Management** – Reads metadata from XML, annotations, or Java-based configuration.

## What are the different types of Spring IoC Containers?

Spring provides two main types of IoC containers:

1. **BeanFactory (Basic Container)**
   A lightweight and basic IoC container.
   Uses lazy initialization (objects are created only when needed).
   Good for small applications.
   Implemented by org.springframework.beans.factory.BeanFactory.

```java
BeanFactory factory = new ClassPathXmlApplicationContext("beans.xml");
MyBean myBean = (MyBean) factory.getBean("myBean");
```

2. **ApplicationContext (Advanced Container)**
   More powerful than BeanFactory, commonly used in enterprise applications.
   Supports eager initialization (beans are created at startup).
   Provides event handling, internationalization, and AOP support.
   Implemented by org.springframework.context.ApplicationContext.

```java
ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
MyBean myBean = context.getBean(MyBean.class);
```

## What are the ways to configure beans?

Spring IoC Container reads configuration from:

1. __XML Configuration__

```xml
<bean id="myBean" class="com.example.MyBean"/>
```

2. __Java-based Configuration (Annotation-based)__

```java @Configuration
public class AppConfig {
    @Bean
    public MyBean myBean() {
        return new MyBean();
    }
}
```

3. __Annotation-based Configuration (@Component, @Service, @Repository)__

```java
@Component
public class MyBean {
}
```
