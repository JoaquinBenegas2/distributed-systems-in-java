# Exception Handling and Logging

## Role

You are a Senior Java engineer ensuring robust error handling and useful logging.

## Exception Handling

### Use Specific Exceptions

* Use `IllegalArgumentException` for invalid method parameters
* Use `IllegalStateException` for invalid object state
* Use `NullPointerException` (or `Objects.requireNonNull()`) for null checks
* Create custom exceptions when domain-specific errors need clear semantics

### Exception Best Practices

```java
// Good: Specific exception with descriptive message
public void processRequest(Request request) {
    Objects.requireNonNull(request, "Request cannot be null");
    
    if (request.getTimeout() <= 0) {
        throw new IllegalArgumentException("Timeout must be positive, got: " + request.getTimeout());
    }
    
    // Process request...
}

// Good: Custom exception for domain errors
public class CircuitBreakerOpenException extends RuntimeException {
    public CircuitBreakerOpenException(String message) {
        super(message);
    }
}
```

### Resource Management

Always use **try-with-resources** for AutoCloseable resources:

```java
try (BufferedReader reader = Files.newBufferedReader(path)) {
    return reader.lines().collect(Collectors.toList());
} // Automatically closed
```

### Exception Chaining

Preserve original exception context:

```java
try {
    externalService.call();
} catch (IOException e) {
    throw new ServiceException("Failed to call external service", e);
}
```

## Logging

### Framework

* Use **SLF4J** as the logging facade
* Use **Logback** or **Log4j2** as implementation
* Declare logger as: `private static final Logger logger = LoggerFactory.getLogger(ClassName.class);`

### Log Levels

* **ERROR**: System errors, exceptions that need attention
* **WARN**: Unexpected situations that don't break functionality
* **INFO**: Important business events, state changes
* **DEBUG**: Detailed information for debugging
* **TRACE**: Very detailed diagnostic information

### Logging Best Practices

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class CircuitBreaker {
    private static final Logger logger = LoggerFactory.getLogger(CircuitBreaker.class);
    
    public void execute(Runnable task) {
        try {
            logger.debug("Executing task via circuit breaker");
            task.run();
            logger.info("Task executed successfully");
        } catch (Exception e) {
            logger.error("Task execution failed", e);
            throw e;
        }
    }
}
```

### Key Rules

* **Use parameterized logging**: `logger.info("Processing request: {}", requestId)` not `logger.info("Processing request: " + requestId)`
* **Never log sensitive data**: passwords, tokens, PII
* **Log exceptions with context**: always include the exception object
* **Keep log messages concise** but informative
