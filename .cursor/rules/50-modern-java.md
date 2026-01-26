# Modern Java Features (Java 17+)

## Role

You are a Senior Java engineer using modern Java features effectively.

## Streams API

Use Streams for declarative collection processing:

```java
// Good: Streams for filtering and mapping
List<String> filtered = items.stream()
    .filter(item -> item.isActive())
    .map(Item::getName)
    .collect(Collectors.toList());

// Good: Parallel streams for CPU-intensive operations (use carefully)
List<String> processed = items.parallelStream()
    .map(this::expensiveOperation)
    .collect(Collectors.toList());
```

## Optional

Use `Optional` for values that may not exist:

```java
// Good: Optional for nullable returns
public Optional<User> findUser(String id) {
    return Optional.ofNullable(userRepository.get(id));
}

// Good: Avoid null checks
user.ifPresent(u -> logger.info("Found user: {}", u.getName()));
String name = user.map(User::getName).orElse("Unknown");
```

## Records (Java 14+)

Use records for immutable data carriers:

```java
// Good: Record for simple data classes
public record CircuitBreakerState(
    State state,
    int failureCount,
    Instant lastFailureTime
) {
    public CircuitBreakerState {
        if (failureCount < 0) {
            throw new IllegalArgumentException("Failure count cannot be negative");
        }
    }
}
```

## Pattern Matching (Java 17+)

Use pattern matching for cleaner code:

```java
// Good: Pattern matching with instanceof
if (obj instanceof String s && s.length() > 0) {
    return s.toUpperCase();
}

// Good: Pattern matching in switch (Java 17+)
String result = switch (state) {
    case OPEN -> "Circuit breaker is open";
    case CLOSED -> "Circuit breaker is closed";
    case HALF_OPEN -> "Circuit breaker is half-open";
};
```

## Text Blocks (Java 15+)

Use text blocks for multi-line strings:

```java
String json = """
    {
        "name": "%s",
        "status": "%s"
    }
    """.formatted(name, status);
```

## Local Variable Type Inference

Use `var` when the type is obvious:

```java
// Good: var for obvious types
var users = new ArrayList<User>();
var config = loadConfiguration();
var executor = Executors.newFixedThreadPool(10);

// Avoid: var when type is unclear
var result = processData(); // What type is result?
```

## Sealed Classes (Java 17+)

Use sealed classes for controlled inheritance:

```java
public sealed class Result<T> 
    permits Success, Failure {
    
    public static final class Success<T> extends Result<T> {
        private final T value;
        // ...
    }
    
    public static final class Failure<T> extends Result<T> {
        private final Exception error;
        // ...
    }
}
```

## Best Practices

* **Prefer streams over loops** for collection processing
* **Use Optional** instead of returning null
* **Use records** for simple data classes
* **Use pattern matching** to reduce boilerplate
* **Use text blocks** for multi-line strings
* **Use `var` judiciously** - only when type is obvious
* **Leverage modern APIs**: `java.time`, `List.of()`, `Map.of()`
