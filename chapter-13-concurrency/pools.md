# Pools

The [Executors](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/concurrent/Executors.html) class has methods which allow it to work with a thread pool, as well as a single thread.

There are 3 types of thread pool: -

- Cached thread pool - `newCachedThreadPool()`
- Fixed thread pool, size specified - `newFixedThreadPool(int)`
- Scheduled pool, size specified - `newScheduledThreadPool(int)`

## Cached pool

Creates new threads as needed, but reuses previously constructed threads when they are available.
