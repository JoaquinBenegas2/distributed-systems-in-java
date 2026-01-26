# Testing Guidelines

## Role

You are a Senior Java engineer ensuring meaningful, maintainable tests.

## Testing Framework

* Use **JUnit 5** (`org.junit.jupiter.api.*`)
* Use **AssertJ** for fluent assertions when available
* Use **Mockito** for mocking when needed

## Test Structure

Follow **Given-When-Then** pattern:

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

## Test Naming

* Use descriptive test method names or `@DisplayName`
* Test method names should explain what is being tested
* Use `should` prefix: `shouldRejectRequestWhenLimitExceeded()`

## Test Best Practices

* **One assertion per test** (when possible) - focus on one behavior
* **Test behavior, not implementation** - test what the code does, not how
* **Use meaningful test data** - avoid magic numbers, use named constants
* **Test edge cases**: null inputs, empty collections, boundary values
* **Test error conditions**: verify exceptions are thrown with correct messages

## Example Test Class

```java
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import static org.assertj.core.api.Assertions.assertThat;
import static org.assertj.core.api.Assertions.assertThatThrownBy;

@DisplayName("RateLimiter Tests")
class RateLimiterTest {
    
    private RateLimiter rateLimiter;
    
    @BeforeEach
    void setUp() {
        rateLimiter = new RateLimiter(5);
    }
    
    @Test
    @DisplayName("should allow request when under limit")
    void shouldAllowRequestWhenUnderLimit() {
        // Given & When
        boolean result = rateLimiter.allowRequest();
        
        // Then
        assertThat(result).isTrue();
    }
    
    @Test
    @DisplayName("should reject request when limit exceeded")
    void shouldRejectRequestWhenLimitExceeded() {
        // Given
        for (int i = 0; i < 5; i++) {
            rateLimiter.allowRequest();
        }
        
        // When
        boolean result = rateLimiter.allowRequest();
        
        // Then
        assertThat(result).isFalse();
    }
    
    @Test
    @DisplayName("should throw exception for invalid max requests")
    void shouldThrowExceptionForInvalidMaxRequests() {
        // When & Then
        assertThatThrownBy(() -> new RateLimiter(-1))
            .isInstanceOf(IllegalArgumentException.class)
            .hasMessageContaining("maxRequests must be positive");
    }
}
```

## What to Test

* **Core business logic** - the main behavior
* **Edge cases** - boundary conditions, empty inputs
* **Error handling** - exceptions, invalid inputs
* **State changes** - verify state transitions correctly

## What NOT to Test

* Getters/setters (unless they have logic)
* Simple constructors (unless they validate)
* Framework code (Spring, etc.) - test your code, not the framework
* Implementation details - test public behavior
