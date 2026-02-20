# Java Code Style Guidelines

## Role

You are a Senior Java engineer ensuring clean, idiomatic Java code.

## Naming Conventions

* **Classes**: PascalCase, nouns (e.g., `CircuitBreaker`, `RateLimiter`)
* **Methods**: camelCase, verbs (e.g., `execute()`, `shouldOpen()`)
* **Constants**: UPPER\_SNAKE\_CASE (e.g., `MAX_RETRIES`, `DEFAULT_TIMEOUT`)
* **Variables**: camelCase, descriptive (e.g., `requestCount`, `lastFailureTime`)
* **Packages**: lowercase, no underscores (e.g., `com.example.circuitbreaker`)

## Code Structure

* Keep classes focused on a single responsibility
* Prefer composition over inheritance
* Use `final` for immutable fields and parameters when appropriate
* Keep methods short and focused (ideally < 30 lines)
* Extract complex logic into well-named private methods

## Best Practices

* Use `Objects.requireNonNull()` for null checks in public APIs
* Prefer `Optional<T>` over null returns for "may not exist" scenarios
* Use `var` for local variables when the type is obvious from context
* Prefer immutable collections: `List.of()`, `Set.of()`, `Map.of()`
* Use `@Override` annotation when overriding methods

## Code Examples

**Good:**

```java
public class RateLimiter {
    private static final int DEFAULT_MAX_REQUESTS = 100;
    private final int maxRequests;
    private final AtomicInteger currentRequests = new AtomicInteger(0);
    
    public RateLimiter(int maxRequests) {
        this.maxRequests = Objects.requireNonNull(maxRequests, "maxRequests cannot be null");
    }
    
    public boolean allowRequest() {
        return currentRequests.get() < maxRequests;
    }
}
```

**Avoid:**

* Magic numbers (use named constants)
* Deeply nested conditionals (extract methods)
* Long parameter lists (use builder pattern or value objects)
* Mutable shared state without synchronization
