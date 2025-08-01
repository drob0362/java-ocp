# Intro

A *thread* is the smallest unit of execution which can be scheduled by a Operating System.
A *process* is a group of associated threads that execute in the same environment.
A *task* is a single unit of work performed by a thread.

A thread can complete multiple independent tasks, but only one at a time.

## Creating a thread

A common way to define a *task* for a thread is by using the *Runnable* interface,
which is a functional interface.

Note that a thread cannot be started with the *run* method, only the *start* method.
The run method is typically used to define a thread in a class which extends *Thread*.

It is more common and easier to create a thread using Lambdas.

## Daemon threads

Daemon threads have specific behaviour in Java, which is that they do not prevent
an application from terminating.
The java *psvm* method is a user defined thread. User defined threads are not daemon threads.

## States

Possible states are NEW, RUNNABLE, TERMINATED, BLOCKED, WAITING and TIMED_WAITING.

## Thread lifecycle

A thread is initialised with a *NEW* state. As soon is start() is called, the thread
moved to the *RUNNABLE* state. This state means that the thread is able to run.

Whilst in a *RUNNABLE* state, a thread may transition to states where it pauses it work:
BLOCKED, WAITING or TIMED_WAITING.

Once a thread completes its work or throws an exception, its state becomes *TERMINATED*.

##  Best practices

Code in any thread, including a main(user) thread, which is in a loop and is dependent on some outside factor e.g. a variable
being modified by another thread, should aleways have a sleep added to avoid hogging CPU.
