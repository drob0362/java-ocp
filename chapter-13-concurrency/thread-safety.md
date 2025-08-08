# Thread safety

##  Volatile

The `volatile` attribute is relevant to the use of threads.
It's purpose is to ensure that *only one thread at a time* can modify a variable.

This does not guarantee thread safety though, so is rarely used.
A likely scenario which could use volatile and still not be thread safe is where two operations
are carried out as two operations, rather than a single operation.

## Atomic classes

The concurrency API contains atomic classes, which are able to retrieve and modify values in a single call. Such classes are: -

- AtomicInteger
- AtomicBoolean

##  Synchronized

The use of `synchronized` can achieve the desired outcome, when using threads.
In order to achieve this, the same object must be used with the `synchronized` statement.

### Sync and static

Static can be used, should you need to enable thread safety across all instances of a class. Rather than an instance of a class.

### Sync methods

Adding the `synchronized` modifier to any instance method automatically provides thread safety to an object. This can be used with any object.

## Lock framework

The lock framework comes into play, if the synchronized functionality is insufficient.
You cannot, for example, check if a lock is available with synchronized.
`Lock` is an interface, which an object must implement in order for it to be possible to lock it.

A class which provides the lock functionality is the `Reentrant` class.
This class only allows to thread to hold a lock at any given time.

The methods available to work with locks are: -

- lock - requests lock and blocks until lock acquired
- unlock - release lock
- tryLock - attempts to lock and returns immediately, with boolean result
- tryLock with timeout - requests lock and blocks for time period or until lock acquired. Returns boolean result

It is recommended to place `lock` method calls in a `try, finally` block.
