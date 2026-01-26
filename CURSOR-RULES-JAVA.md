# Cursor Rules for Java - Essential Guide

This is a concise, project-specific guide to Cursor rules for the **distributed-systems-in-java** repository. These rules are optimized for creating small, runnable examples of distributed systems patterns.

## Overview

This repository uses a minimal set of essential Cursor rules located in `.cursor/my-rules/`. These rules focus on:

* Clean, idiomatic Java code
* Meaningful tests with JUnit 5
* Clear, concise documentation
* Modern Java features (Java 17+)
* Thread-safe concurrent code

## Rule Files

| Rule File | Description | When to Use |
|-----------|-------------|-------------|
| [00-project-context](.cursor/my-rules/00-project-context.md) | Project-specific context and principles | Always applied - defines project goals |
| [10-java-style](.cursor/my-rules/10-java-style.md) | Java code style and naming conventions | Apply when writing or reviewing code |
| [20-testing](.cursor/my-rules/20-testing.md) | JUnit 5 testing guidelines | Apply when writing or improving tests |
| [30-exceptions-logging](.cursor/my-rules/30-exceptions-logging.md) | Exception handling and logging practices | Apply when handling errors or adding logging |
| [40-concurrency](.cursor/my-rules/40-concurrency.md) | Thread safety and concurrent programming | Apply when working with multi-threaded code |
| [50-modern-java](.cursor/my-rules/50-modern-java.md) | Modern Java features (Streams, Optional, Records, etc.) | Apply when refactoring or writing new code |
| [60-documentation](.cursor/my-rules/60-documentation.md) | README and code documentation guidelines | Apply when creating or updating documentation |
| [70-maven-basics](.cursor/my-rules/70-maven-basics.md) | Maven project structure and best practices | Apply when setting up or modifying `pom.xml` |

## Quick Reference

### Code Style

**Prompt:** `Apply Java style guidelines from @10-java-style to improve this code`

### Testing

**Prompt:** `Write JUnit 5 tests following @20-testing for this class`

### Exception Handling

**Prompt:** `Improve exception handling using @30-exceptions-logging`

### Concurrency

**Prompt:** `Review this concurrent code using @40-concurrency guidelines`

### Modern Java

**Prompt:** `Refactor this code to use modern Java features from @50-modern-java`

### Documentation

**Prompt:** `Create a README following @60-documentation for this module`

### Maven Setup

**Prompt:** `Review this pom.xml using @70-maven-basics`

## Common Workflows

### Creating a New Example Module

1. **Setup Maven project:**
   ```
   Apply Maven structure from @70-maven-basics
   ```

2. **Write the code:**
   ```
   Implement following @10-java-style and @50-modern-java
   ```

3. **Add tests:**
   ```
   Write tests using @20-testing
   ```

4. **Add documentation:**
   ```
   Create README using @60-documentation
   ```

### Improving Existing Code

1. **Code quality:**
   ```
   Improve code style using @10-java-style
   ```

2. **Error handling:**
   ```
   Review exception handling with @30-exceptions-logging
   ```

3. **Modernize:**
   ```
   Refactor to modern Java using @50-modern-java
   ```

### Working with Concurrency

```
Review concurrent code using @40-concurrency
```

## What's NOT Included

This minimal ruleset intentionally excludes:

* **Enterprise patterns**: Heavy DDD, complex layering, enterprise frameworks
* **Advanced profiling**: JMeter, async profiler, detailed performance analysis
* **Complex documentation generation**: Automated Javadoc generation, diagram tools
* **Advanced Maven plugins**: Complex build configurations, enforcer plugins
* **Niche patterns**: Data-oriented programming, advanced functional patterns
* **Security deep-dives**: Comprehensive secure coding (basic practices included)

These can be added on-demand using the full ruleset in `.cursor/rules/` if needed for specific examples.

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

**Note**: This is a focused ruleset for educational examples. For production applications, consider the comprehensive ruleset in `.cursor/rules/`.
