# Documentation Guidelines

## Role

You are a Senior Java engineer ensuring clear, useful documentation.

## README Structure

Each module/example should have a README.md with:

```markdown
# [Pattern Name]

## Overview

Brief description of what this example demonstrates.

## What It Does

- Key feature 1
- Key feature 2
- Key feature 3

## How to Run

\`\`\`bash
mvn clean compile
mvn exec:java -Dexec.mainClass="com.example.Main"
\`\`\`

## Key Concepts

- Concept 1: Explanation
- Concept 2: Explanation

## Trade-offs

- **Pros**: What this approach does well
- **Cons**: Limitations or when not to use

## Related Patterns

Links to related examples in this repository.
```

## Code Documentation

### Javadoc for Public APIs

```java
/**
 * Executes a task through the circuit breaker.
 * 
 * @param task the task to execute
 * @throws CircuitBreakerOpenException if the circuit breaker is open
 * @return the result of the task execution
 */
public <T> T execute(Supplier<T> task) {
    // Implementation
}
```

### Inline Comments

* **Explain WHY, not WHAT** - the code should be self-explanatory
* Use comments for non-obvious business logic or complex algorithms
* Avoid obvious comments: `// Increment counter` (code already shows this)

```java
// Good: Explains why
// Exponential backoff: double the delay on each retry to avoid overwhelming the service
long delay = baseDelay * (1L << attemptCount);

// Avoid: States the obvious
// Increment the counter
counter++;
```

## Class-Level Documentation

For complex classes, add a brief class-level Javadoc:

```java
/**
 * Implements the Circuit Breaker pattern to prevent cascading failures.
 * 
 * <p>The circuit breaker has three states:
 * <ul>
 *   <li>CLOSED: Normal operation, requests pass through</li>
 *   <li>OPEN: Failing, requests are rejected immediately</li>
 *   <li>HALF_OPEN: Testing if service has recovered</li>
 * </ul>
 */
public class CircuitBreaker {
    // ...
}
```

## Best Practices

* **Keep it concise** - documentation should be brief but informative
* **Update with code** - documentation that's outdated is worse than no documentation
* **Include examples** - show how to use the code
* **Explain trade-offs** - help readers understand when to use each approach
* **Use clear language** - avoid jargon unless necessary
