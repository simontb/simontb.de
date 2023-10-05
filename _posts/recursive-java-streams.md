---
layout: post
title: Streaming recursive data
subtitle: Using the Java Streams API for recursive data
tags: [programming, java]
---
The Java Streams API is great for working with data of all kinds, because its declarative nature lets us focus on the business logic. I recently had to write error handling for a JPA exception based on the database error code. Unfortunately, this code is not in the exception itself, but deeper in the stack of causes:

![Debug view of a PersistenceException with expanded cause fields until JDBCDriverException with vendorErrorCode](/assets/img/post-recursive-java-streams/persistence-exception-cause-stack.png)

As you can see, the error code I was looking for is in the 4th Exception of the cause stack. This `JDBCDriverException` has a field called `vendorErrorCode`. It's a subclass of `SQLException` that is also the parent exception in the cause stack. So we have to look at the causes until we find an instance of `SQLException` with a `vendorErrorCode`.

I'm known as a Streams advocate within my team, so I asked myself if it'd be possible to stream over the causes and use the stream operations to get the error code. I already had the Stream pipeline in my mind, but needed a way to stream over the cause stack.

Streams are most famous for their usage with the Java Collections API. Simply call the `stream`-method on the Collection instance to get a stream on the Collection's elements.

However, not everything you want to stream over is in a Collection. And you don't have to create one just for streaming purposes, because there are other ways to create a Stream.

First there a static methods in the JDK like `IntStream.range(0, 10)` or `Stream.of(firstElement, secondElement)`. These are useful and quite self-explanatory (in a sense that an experienced Java developer probably won't have to read the Javadoc to get a sense of what these methods are doing).

## Write your own Spliterator
An advanced approach to generate a Stream is to implement the `Spliterator` interface. This is common if you want to add streaming capabilities to your own data structure. Then you can pass that Spliterator to `StreamSupport.stream(spliterator, false)` to create a Stream. The second parameter indicates whether the Stream shall be parallel or not.

This is exactly what the `stream`-method of the Collection interface does. It passes the Spliterator of the Collection to the `StreamSupport.stream` method:
```java
default Stream<E> stream() {
    return StreamSupport.stream(spliterator(), false);
}
```

While `Collection` has a default implementation for `spliterator()`, most Collections override this method with a Spliterator that is tailored to that data structure.

To implement your own Spliterator, you have to implement all abstract methods:
```java
public interface Spliterator<T> {
    boolean tryAdvance(Consumer<? super T> action);
    Spliterator<T> trySplit();
    long estimateSize();
    int characteristics();
}
```
The `tryAdvance`-method performs the given action on the next remaining element and returns whether such a remaining element existed.

With the `trySplit`-method, the Stream pipeline tries to split the Stream. This is typically done for parallel processing of the Stream pipeline. E.g., when the Stream contains 10 elements, the Spliterator can return a new instance that contains the last 5 elements and keep the first 5 to himself. A Stream that cannot be split returns `null`.

The `estimateSize`-method returns the estimated size of the Stream. When the size is unknown, `Long.MAX_VALUE` should be returned.

Lastly, the `characteristics`-method is used to describe the characteristics of the Stream. E.g., whether the data is ordered or if the size of the Stream is known.

Our recursive Spliterator might look like this:

```java

```
