# Stream types

*Serial* streams have the behaviour that results are *ordered* and *only one entry* can be processed at a time.

*Parallel* streams are capable of processing results *concurrently*, achieved by using multiple threads.

## Parallel streams

Parallel streams can be made from another stream or from a collections class.

###  Unordered streams

For parallel streams, *unordered* streams are more performant. It is merely a method call on an existing stream, to obtain an *unordered* stream.

### Avoiding parallel stream problems

If a `reduce` method is to be used with parallel streams, the 3 argument version (accumulator, reducer and identity) must be present.
Similiarly, the same goes for the `collect` method. The 3 argument method must be called.
