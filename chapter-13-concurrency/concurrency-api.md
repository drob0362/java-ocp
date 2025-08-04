# Intro

Java has a package `java.util.concurrent`, which is referred to as the concurrency API.
Its purpose being to handle complex threads operations.

## Highlights

- The API has a `ExecutorService` interface, which creates and manages threads
- API has numerous features, including thread pooling and scheduling
- It is recommended to use this API for creation and execution of tasks, even for a single thread
- It is best practice to control threads through this API rather than interact with threads directly

## Single thread executor

A `Executors` interface exists, which can be used to `start` threads.

To achieve this there is the following method: `Executors.newSingleThreadExecutor()`.
This method returns a `ExecutorService`. The service can be used to `execute` multiple threads, via the [Runnable](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/lang/Runnable.html) interface.

When using a single thread executor, it is necessary to use `shutdown` when all the required threads have been submitted to it. This is because this executor creates a non daemon thread.
The state of the executor can be checked using the `isShutdown` and `isTerminated` methods.

### Submit vs Execute

The [executor](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/concurrent/Executor.html) has `submit` and [execute](<https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/concurrent/Executor.html#execute(java.lang.Runnable)> methods. Submit returns a `Future` object, whereas `execute` does not.

Another difference between submit and execute is that submit has two different signatures. Either a `Runnable` or `Callable` type can be passed as a argument. If a `runnable` is passed, there will be a `null` return from a Future.

## Callable

`Callable` is similar to `runnable` except its `call` method returns a value and can throw a checked exception. This call method is in contrast to the `run` method of the Runnable.

Callable is a type of functional interface. When you define such an interface, the return type must be specified. This return type is what is returned when the `submit` function is used with a `Callable`.

## Scheduled Threads

If a task needs to happen at a specific time or interval, functionality exists in the API to cater for this.
And it can be actioned against a single thread or pool of threads.
A delay is provided as a long, coupled with a `TimeUnit`.
Can be used with a Runnable or Callable. An extension of the `Future` type exists, `ScheduledFuture` - which has an additional method to return the remaining delay.
