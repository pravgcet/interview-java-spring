# Spring basics

## What is Spring?

Spring Framework is a Java-based framework that provides a comprehensive programming and configuration model for modern Java applications. It is widely used for building enterprise-level applications and supports dependency injection, aspect-oriented programming, and transaction management.

## Key Features of Spring Framework

1. **Dependency Injection (DI)** – Manages object dependencies automatically, making code more modular and testable.

2. **Aspect-Oriented Programming (AOP)** – Enables separation of cross-cutting concerns like logging and security.
3. **Spring MVC** – A framework for building web applications.
4. **Spring Boot** – A sub-project that simplifies application setup with auto-configuration.
5. **Spring Data** – Simplifies database access with repositories.
6. **Spring Security** – Provides authentication and authorization mechanisms.
7. **Spring Cloud** – Helps in building microservices-based applications.
8. **Transaction Management** – Ensures data consistency in database operations.

<p>Spring follows a loosely coupled architecture, making it easier to develop, test, and maintain applications. It is widely used in enterprise applications, microservices, and cloud-native development.</p>

## What is IoC Container?

The `org.springframework.beans` and `org.springframework.context` packages are the basis for Spring Framework’s IoC container.

In Spring, the **IoC (Inversion of Control) Container** is a **core concept** responsible for managing the lifecycle and configuration of application objects, known as *beans*.

## Key Functions of the IoC Container

1. **Bean Creation** 
   - Instantiates objects defined in the configuration (via annotations or XML).

2. **Dependency Injection** 
   - Injects dependencies into beans (constructor, setter, or field injection) automatically.

3. **Lifecycle Management** 
   - Manages bean lifecycles from instantiation to destruction using callbacks like `@PostConstruct`, `@PreDestroy`, etc.

4. **Configuration Management** 
   - Reads configuration metadata (`@Component`, `@Configuration`, `@Bean`, or XML) to understand how to wire beans.

5. **Scope Management** 
   - Manages different bean scopes (singleton, prototype, request, session, etc.).

---

## Types of IoC Containers in Spring

- **BeanFactory** 
  Basic container with fundamental IoC features.

- **ApplicationContext** 
  More advanced container built on top of `BeanFactory`, adds features like:
  - Internationalization
  - Event propagation
  - AOP integration

---

## What are Beans?

## What is Dependency Injection?

Dependency injection (DI) is a specialized form of IoC, whereby objects define their dependencies only through constructor arguments, arguments to a factory method, or properties that are set on the object instance after it is constructed or returned from a factory method. The IoC container then injects those dependencies when it creates the bean. This process is fundamentally the inverse (hence the name, Inversion of Control) of the bean itself controlling the instantiation or location of its dependencies by using direct construction of classes or a mechanism such as the Service Locator pattern.
