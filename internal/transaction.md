## How Spring Configures @Transactional at Startup?

When we use the `@Transactional` annotation in a Spring application, the Spring IoC container processes it at startup and applies transaction management. This is done through Spring AOP (Aspect-Oriented Programming) or Spring proxy-based mechanisms.

## Step-by-step process of how Spring configures transactions at startup.

__1. Scanning for @Transactional Annotations__

Spring looks for `@Transactional` annotations in the application code. These can be applied at:

+ __Class level__ → All methods inherit the transaction configuration.
+ __Method level__ → Only the annotated methods are transactional.

```java
    @Service
    @Transactional
    public class PaymentService {
        public void processPayment() {
            // Transactional logic
        }
    }
```
Or at method level

```java
    @Service
    public class PaymentService {
        @Transactional
        public void processPayment() {
            // Transactional logic
        }
    }
```

__2. Enabling Transaction Management__

To activate transaction management, you must enable it using:
```java
    @Configuration
    @EnableTransactionManagement
    public class AppConfig {
        @Bean
        public PlatformTransactionManager transactionManager(DataSource dataSource) {
            return new DataSourceTransactionManager(dataSource);
        }
    }
```
__3. Creating a Proxy Around Transactional Beans__

Spring creates a proxy object for each bean with a @Transactional method:

+ If the method is called, the proxy intercepts the call and starts a transaction.
+ After execution, the proxy commits or rolls back the transaction based on the method outcome.
+ Proxy Mechanisms in Spring

__Spring creates proxies using:__

JDK Dynamic Proxy – Used if the class implements an interface.
CGLIB Proxy – Used if the class does not implement an interface.
Example: If you call processPayment(), instead of calling the original method directly, Spring calls a proxy method that:

+ Starts a transaction.
+ Calls the actual method.
+ Commits or rolls back the transaction.

__4. Transaction Manager Initialization__
Spring initializes a transaction manager, which is responsible for handling database transactions. Examples:

JPA → JpaTransactionManager
JDBC → DataSourceTransactionManager
Hibernate → HibernateTransactionManager
Spring injects the appropriate transaction manager based on the configuration.

__5. Transaction Lifecycle Execution__

When a transactional method is called:

+ The proxy intercepts the method call.
+ The transaction manager:
Starts a transaction before execution.
+ Executes the method.
+ Commits the transaction if no exception occurs.
+ Rolls back the transaction if an exception occurs.

__6. Handling Rollbacks and Propagation__
By default:

+ Unchecked exceptions (RuntimeException) trigger a rollback.
+ Checked exceptions do NOT trigger a rollback unless explicitly configured.
```java
@Transactional(rollbackFor = Exception.class) // Rollback for all exceptions
public void processOrder() {
    // Business logic
}
```
__Transaction Propagation__

Defines how transactions behave when nested calls occur. Example:

```java
@Transactional(propagation = Propagation.REQUIRES_NEW)
public void updateInventory() {
    // Runs in a new transaction, independent of the caller
}
```




