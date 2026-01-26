# Agent Instructions for Distributed Systems in Java

## Project Overview

This repository is a **learning and reference collection** of small, runnable Java examples demonstrating distributed systems concepts and patterns. Each module is designed to be minimal, didactic, and executable.

### Purpose

The repository focuses on educational examples of distributed systems patterns:

* API Gateway patterns
* Circuit Breaker
* Rate Limiting
* Retry/Timeout mechanisms
* Bulkhead pattern
* Messaging patterns
* Saga pattern
* Observability basics

### Core Principles

1. **Simplicity First**: Keep examples minimal and focused on one concept
2. **Real Code**: Always use working, idiomatic Java (no pseudocode)
3. **Clear Documentation**: Each example should have a concise README explaining what it demonstrates
4. **Trade-offs Explained**: Document why certain approaches are chosen
5. **Testable**: Include JUnit 5 tests for core logic where it makes sense
6. **No Over-engineering**: Avoid enterprise complexity unless the pattern requires it

## Technology Stack

* **Java**: 17+ (use modern features when appropriate)
* **Build Tool**: Maven
* **Testing**: JUnit 5
* **Logging**: SLF4J + Logback
* **Dependencies**: Minimal - only what's needed for the pattern

## Build and Test Commands

```bash
# Compile the project
mvn clean compile

# Run all tests
mvn test

# Run a specific module's tests
mvn test -pl <module-name>

# Package the project
mvn clean package

# Run a main class
mvn exec:java -Dexec.mainClass="com.example.Main"
```

## Code Style Guidelines

Follow the Cursor rules located in `.cursor/rules/`:

* **Java Style** (`@10-java-style`): PascalCase for classes, camelCase for methods, UPPER\_SNAKE\_CASE for constants
* **Modern Java** (`@50-modern-java`): Use Streams, Optional, Records, pattern matching (Java 17+)
* **Testing** (`@20-testing`): JUnit 5 with Given-When-Then structure, descriptive test names
* **Exceptions & Logging** (`@30-exceptions-logging`): Specific exceptions, try-with-resources, SLF4J parameterized logging
* **Concurrency** (`@40-concurrency`): Thread-safe collections, atomic operations, ExecutorService

### Key Style Rules

* Use `Objects.requireNonNull()` for null checks in public APIs
* Prefer `Optional<T>` over null returns
* Use `var` for local variables when type is obvious
* Prefer immutable collections: `List.of()`, `Set.of()`, `Map.of()`
* Keep methods short and focused (ideally < 30 lines)
* Use `final` for immutable fields and parameters when appropriate

## Testing Instructions

* Use **JUnit 5** (`org.junit.jupiter.api.*`)
* Follow **Given-When-Then** structure in tests
* Use descriptive test method names or `@DisplayName`
* Test behavior, not implementation details
* Test edge cases: null inputs, empty collections, boundary values
* Test error conditions: verify exceptions are thrown with correct messages

### Example Test Structure

```java
@Test
@DisplayName("should allow request when under limit")
void shouldAllowRequestWhenUnderLimit() {
    // Given
    RateLimiter limiter = new RateLimiter(10);
    
    // When
    boolean result = limiter.allowRequest();
    
    // Then
    assertThat(result).isTrue();
}
```

## Using Cursor Rules

This project uses a minimal set of essential Cursor rules. Reference `CURSOR-RULES-JAVA.md` for complete documentation.

### Quick Reference Prompts

* **Code Style**: `Apply Java style guidelines from @10-java-style to improve this code`
* **Testing**: `Write JUnit 5 tests following @20-testing for this class`
* **Exception Handling**: `Improve exception handling using @30-exceptions-logging`
* **Concurrency**: `Review this concurrent code using @40-concurrency guidelines`
* **Modern Java**: `Refactor this code to use modern Java features from @50-modern-java`
* **Documentation**: `Create a README following @60-documentation for this module`
* **Maven**: `Review this pom.xml using @70-maven-basics`

## Creating a New Example Module

When adding a new distributed systems pattern example:

1. **Setup Maven project structure**:
   * Follow standard Maven directory layout
   * Minimal `pom.xml` with Java 17+ configuration
   * Include JUnit 5 as test dependency

2. **Write the code**:
   * Keep it focused on demonstrating one pattern
   * Use modern Java features (Streams, Optional, Records)
   * Follow naming conventions and code style

3. **Add tests**:
   * Write JUnit 5 tests for core logic
   * Test edge cases and error conditions
   * Use Given-When-Then structure

4. **Add documentation**:
   * Create a README.md explaining what the pattern does
   * Include "How to Run" section
   * Document trade-offs and when to use the pattern
   * Link to related patterns

## Exception Handling

* Use specific exceptions: `IllegalArgumentException`, `IllegalStateException`
* Use `Objects.requireNonNull()` for null checks
* Always use try-with-resources for AutoCloseable resources
* Preserve exception context with exception chaining
* Create custom exceptions for domain-specific errors

## Logging

* Use **SLF4J** as logging facade
* Declare logger as: `private static final Logger logger = LoggerFactory.getLogger(ClassName.class);`
* Use parameterized logging: `logger.info("Processing request: {}", requestId)`
* Never log sensitive data (passwords, tokens, PII)
* Log exceptions with context: always include the exception object

## Concurrency

When working with concurrent code:

* Prefer `java.util.concurrent` collections (`ConcurrentHashMap`, `BlockingQueue`)
* Use atomic classes for single-variable operations (`AtomicInteger`, `AtomicLong`)
* Use `ExecutorService` for thread pool management
* Prefer immutable objects for thread safety
* Document thread safety clearly
* Test concurrent code with stress tests

## Documentation Standards

Each module should have a README.md with:

* **Overview**: Brief description of what the example demonstrates
* **What It Does**: Key features of the pattern
* **How to Run**: Maven commands to compile and run
* **Key Concepts**: Explanation of the pattern
* **Trade-offs**: Pros and cons, when to use
* **Related Patterns**: Links to related examples

## What NOT to Include

This project intentionally avoids:

* Enterprise patterns: Heavy DDD, complex layering, enterprise frameworks
* Advanced profiling: JMeter, async profiler (unless specifically demonstrating observability)
* Complex documentation generation: Automated Javadoc, diagram tools
* Advanced Maven plugins: Complex build configurations
* Niche patterns: Data-oriented programming, advanced functional patterns

Keep examples simple and focused on the distributed systems pattern being demonstrated.

## Commit Messages

This project follows the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) specification to create an explicit and structured commit history.

### Format

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### Commit Types

* **`feat`**: A new feature (correlates with MINOR in SemVer)
* **`fix`**: A bug fix (correlates with PATCH in SemVer)
* **`docs`**: Documentation only changes
* **`style`**: Code style changes (formatting, missing semicolons, etc.)
* **`refactor`**: Code refactoring without changing functionality
* **`test`**: Adding or updating tests
* **`chore`**: Maintenance tasks, dependency updates, build config changes

### Scope (Optional)

The scope provides additional contextual information about the area of the codebase:

* Pattern name: `feat(circuit-breaker):`, `fix(rate-limiter):`
* Component: `docs(readme):`, `test(circuit-breaker):`

### Examples

**Feature addition:**

```
feat(circuit-breaker): add half-open state transition

Implement automatic transition from OPEN to HALF_OPEN state
after timeout period to test if service has recovered.
```

**Bug fix:**

```
fix(rate-limiter): correct request count reset logic

The request counter was not resetting properly at the start
of each time window, causing incorrect rate limiting behavior.
```

**Documentation:**

```
docs: add README for retry pattern example

Include usage examples, trade-offs, and when to use
exponential backoff vs fixed delay retry strategies.
```

**Test addition:**

```
test(circuit-breaker): add tests for state transitions

Cover all state transitions: CLOSED -> OPEN, OPEN -> HALF_OPEN,
and HALF_OPEN -> CLOSED/HOPEN scenarios.
```

**Refactoring:**

```
refactor(api-gateway): extract request validation logic

Move validation to separate Validator class to improve
testability and separation of concerns.
```

**Breaking change:**

```
feat(circuit-breaker)!: change failure threshold to percentage

BREAKING CHANGE: Failure threshold now accepts percentage (0-100)
instead of absolute count. Update configuration accordingly.
```

### Best Practices

* Use imperative mood in description: "Add feature" not "Added feature"
* Keep description concise (50-72 characters recommended)
* Capitalize first letter of description
* No period at the end of description
* Use body to explain **what** and **why**, not **how**
* Reference related issues or patterns in footer when relevant
* Use `!` after type/scope or `BREAKING CHANGE:` footer for breaking changes

### Breaking Changes

Breaking changes can be indicated in two ways:

1. **Using `!` in the type/scope:**
   ```
   feat(circuit-breaker)!: change API signature
   ```

2. **Using BREAKING CHANGE footer:**
   ```
   feat: update rate limiter configuration

   BREAKING CHANGE: Rate limiter now requires timeout parameter
   in constructor instead of setter method.
   ```

## Project Structure

```
distributed-systems-in-java/
├── .cursor/
│   ├── rules/          # Essential Cursor rules for Java development
│   └── my-rules/       # Project-specific rules (if any)
├── <pattern-name>/      # Each pattern gets its own module/directory
│   ├── pom.xml
│   ├── src/
│   │   ├── main/java/
│   │   └── test/java/
│   └── README.md
├── CURSOR-RULES-JAVA.md # Guide to using Cursor rules
└── README.md           # Project overview
```

Each pattern example should be self-contained and runnable independently.
