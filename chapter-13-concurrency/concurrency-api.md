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

The [executor](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/concurrent/Executor.html) has `submit` and [execute](<https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/concurrent/Executor.html#execute(java.lang.Runnable>) methods. Submit returns a `Future` object, whereas `execute` does not.

Another difference between submit and execute is that submit has two different signatures. Either a `Runnable` or `Callable` type can be passed as a argument. If a `runnable` is passed, there will be a `null` return from a Future.

## Callable

`Callable` is similar to `runnable` except its `call` method returns a value and can throw a checked exception. This call method is in contrast to the `run` method of the Runnable.

Callable is a type of functional interface. When you define such an interface, the return type must be specified. This return type is what is returned when the `submit` function is used with a `Callable`.

## Scheduled Threads

If a task needs to happen at a specific time or interval, functionality exists in the API to cater for this.
And it can be actioned against a single thread or pool of threads.
A delay is provided as a long, coupled with a `TimeUnit`.
Can be used with a Runnable or Callable. An extension of the `Future` type exists, `ScheduledFuture` - which has an additional method to return the remaining delay.

## Cyclic barrier

A `CyclicBarrier` class exists, which provides the ability to control the order of tasks or units of work. These tasks are akin to methods.

A [Cyclic Barrier](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/concurrent/CyclicBarrier.html) requires a numeric value with its constructor to indicate how many threads to wait for. The use of the `await` method keeps track of how many threads have completed.

Once the specified number of threads have completed, the barrier is released and the follow on code will be reached. The `await` method is the *barrier*.

## Understanding memory consistency errors

Whether it be an application with a single user defined thread, or an application with multiple threads, it is possible to run into issues with data. This occurs when there is an inconsistent *view* of data.

The reason this occurs is because the code is not using thread safe types, which are provided by the concurrency API. For example, using `ConcurrentHashMap` rather than `HashMap`.

## Synchronised collections

If you know you are going to be working with threads, you should use concurrent collections classes e.g. `ConcurrentLinkedQueue`.

However, if you are passed a reference to a non concurrent class and need to peform synchronised operations then make use of the collections synchronised methods e.g. `synchronisedSortedMap`.
