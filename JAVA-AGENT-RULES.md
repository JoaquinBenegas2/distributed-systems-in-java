# Agent Rules for Java - Essential Guide

This is a concise, project-specific guide to agent rules for the **distributed-systems-in-java** repository. These rules are optimized for creating small, runnable examples of distributed systems patterns.

## Overview

This repository uses a minimal set of essential agent rules located in `.agents/rules/java/`. These rules focus on:

* Clean, idiomatic Java code
* Meaningful tests with JUnit 5
* Clear, concise documentation
* Modern Java features (Java 17+)
* Thread-safe concurrent code

## Rule Files

| Rule File | Description | When to Use |
|-----------|-------------|-------------|
| [java-project-context](.agents/rules/java/java-project-context.md) | Project-specific context and principles | Always applied - defines project goals |
| [java-style](.agents/rules/java/java-style.md) | Java code style and naming conventions | Apply when writing or reviewing code |
| [java-testing](.agents/rules/java/java-testing.md) | JUnit 5 testing guidelines | Apply when writing or improving tests |
| [java-exceptions-logging](.agents/rules/java/java-exceptions-logging.md) | Exception handling and logging practices | Apply when handling errors or adding logging |
| [java-concurrency](.agents/rules/java/java-concurrency.md) | Thread safety and concurrent programming | Apply when working with multi-threaded code |
| [java-modern-java](.agents/rules/java/java-modern-java.md) | Modern Java features (Streams, Optional, Records, etc.) | Apply when refactoring or writing new code |
| [java-documentation](.agents/rules/java/java-documentation.md) | README and code documentation guidelines | Apply when creating or updating documentation |
| [java-maven-basics](.agents/rules/java/java-maven-basics.md) | Maven project structure and best practices | Apply when setting up or modifying `pom.xml` |

## Quick Reference

### Code Style

**Prompt:** `Apply Java style guidelines from @java-style to improve this code`

### Testing

**Prompt:** `Write JUnit 5 tests following @java-testing for this class`

### Exception Handling

**Prompt:** `Improve exception handling using @java-exceptions-logging`

### Concurrency

**Prompt:** `Review this concurrent code using @java-concurrency guidelines`

### Modern Java

**Prompt:** `Refactor this code to use modern Java features from @java-modern-java`

### Documentation

**Prompt:** `Create a README following @java-documentation for this module`

### Maven Setup

**Prompt:** `Review this pom.xml using @java-maven-basics`

## Common Workflows

### Creating a New Example Module

1. **Setup Maven project:**
   ```
   Apply Maven structure from @java-maven-basics
   ```

2. **Write the code:**
   ```
   Implement following @java-style and @java-modern-java
   ```

3. **Add tests:**
   ```
   Write tests using @java-testing
   ```

4. **Add documentation:**
   ```
   Create README using @java-documentation
   ```

### Improving Existing Code

1. **Code quality:**
   ```
   Improve code style using @java-style
   ```

2. **Error handling:**
   ```
   Review exception handling with @java-exceptions-logging
   ```

3. **Modernize:**
   ```
   Refactor to modern Java using @java-modern-java
   ```

### Working with Concurrency

```
Review concurrent code using @java-concurrency
```

## What's NOT Included

This minimal ruleset intentionally excludes:

* **Enterprise patterns**: Heavy DDD, complex layering, enterprise frameworks
* **Advanced profiling**: JMeter, async profiler, detailed performance analysis
* **Complex documentation generation**: Automated Javadoc generation, diagram tools
* **Advanced Maven plugins**: Complex build configurations, enforcer plugins
* **Niche patterns**: Data-oriented programming, advanced functional patterns
* **Security deep-dives**: Comprehensive secure coding (basic practices included)

These can be added on-demand using the full ruleset in `.agents/rules/java/` if needed for specific examples.

## Project Principles

1. **Simplicity First**: Keep examples minimal and focused
2. **Real Code**: Always use working, idiomatic Java (no pseudocode)
3. **Clear Documentation**: Each example should explain what it demonstrates
4. **Trade-offs Explained**: Document why approaches are chosen
5. **Testable**: Include tests for core logic where it makes sense
6. **No Over-engineering**: Avoid complexity unless the pattern requires it

## Target Stack

* **Java**: 17+ (use modern features)
* **Testing**: JUnit 5
* **Build**: Maven
* **Logging**: SLF4J + Logback
* **Dependencies**: Minimal - only what's needed

***

**Note**: This is a focused ruleset for educational examples.
