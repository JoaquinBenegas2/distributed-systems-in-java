# Concurrency Guidelines

## Role

You are a Senior Java engineer ensuring thread-safe, correct concurrent code.

## Thread Safety Fundamentals

### Use Thread-Safe Collections

Prefer `java.util.concurrent` collections:

```java
// Good: Thread-safe collections
private final Map<String, Integer> counters = new ConcurrentHashMap<>();
private final Queue<Task> taskQueue = new ConcurrentLinkedQueue<>();
private final BlockingQueue<Event> eventQueue = new LinkedBlockingQueue<>();
```

### Atomic Operations

Use atomic classes for single-variable operations:

```java
private final AtomicInteger requestCount = new AtomicInteger(0);
private final AtomicLong lastFailureTime = new AtomicLong(0);

public void increment() {
    requestCount.incrementAndGet();
}
```

### Synchronization

* Use `synchronized` for simple critical sections
* Use `ReentrantLock` for more complex locking needs
* Keep critical sections **small** - minimize lock duration

```java
private final Object lock = new Object();
private int count = 0;

public void increment() {
    synchronized (lock) {
        count++;
    }
}
```

## ExecutorService

Use `ExecutorService` for managing thread pools:

```java
ExecutorService executor = Executors.newFixedThreadPool(10);

try {
    executor.submit(() -> processRequest(request));
} finally {
    executor.shutdown();
    executor.awaitTermination(5, TimeUnit.SECONDS);
}
```

## CompletableFuture

Use `CompletableFuture` for asynchronous operations:

```java
CompletableFuture<String> future = CompletableFuture
    .supplyAsync(() -> fetchData(), executor)
    .thenApply(data -> processData(data))
    .exceptionally(ex -> handleError(ex));
```

## Immutability

Prefer immutable objects for thread safety:

```java
// Good: Immutable configuration
public final class CircuitBreakerConfig {
    private final int failureThreshold;
    private final Duration timeout;
    
    public CircuitBreakerConfig(int failureThreshold, Duration timeout) {
        this.failureThreshold = failureThreshold;
        this.timeout = timeout;
    }
    
    // Only getters, no setters
}
```

## Common Patterns

### Producer-Consumer

```java
BlockingQueue<Task> queue = new LinkedBlockingQueue<>(100);

// Producer
queue.put(task);

// Consumer
Task task = queue.take();
```

### Thread-Safe Singleton

```java
public class RateLimiter {
    private static final RateLimiter INSTANCE = new RateLimiter();
    
    private RateLimiter() {}
    
    public static RateLimiter getInstance() {
        return INSTANCE;
    }
}
```

## Best Practices

* **Minimize shared mutable state** - prefer immutable objects
* **Use appropriate concurrency primitives** - don't over-synchronize
* **Document thread safety** - clearly state if a class is thread-safe
* **Test concurrent code** - use stress tests to find race conditions
* **Handle InterruptedException** - restore interrupt status: `Thread.currentThread().interrupt()`
