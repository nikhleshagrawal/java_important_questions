# Java Important Questions

This page is evolving. 

This page will have some important java questions which are learned by experience.

## In Jav8, why we have default method in Interface?

The reason we have default methods in interfaces is to allow the developers to add new methods to the interfaces without affecting the classes that implements these interfaces.

### Why default method?

For example, if several classes such as A, B, C and D implements an interface XYZInterface then if we add a new method to the XYZInterface, we have to change the code in all the classes(A, B, C and D) that implements this interface. In this example we have only four classes that implements the interface which we want to change but imagine if there are hundreds of classes implementing an interface then it would be almost impossible to change the code in all those classes. This is why in java 8, we have a new concept “default methods”. These methods can be added to any existing interface and we do not need to implement these methods in the implementation classes mandatorily, thus we can add these default methods to existing interfaces without breaking the code.

## Why a variable inside Lambda must be Final or Effective Final?

The above problem arises due to Java 8 Language Specification, §15.27.2 which says :

``` 
Any local variable, formal parameter, or exception parameter used but not declared in a lambda expression
must either be declared final or be effectively final (§4.12.4),
or a compile-time error occurs where the use is attempted.
```

The JLS mentions why in §15.27.2:

```
The restriction to effectively final variables prohibits access to dynamically-changing local variables, whose capture would likely introduce concurrency problems.
```

## Difference between Final and Effective Final:

A variable is final or effectively final when it's initialized once and is never mutated in its owner class; we can't initialize it in loops or inner classes.

Final: final int x;
x = 3;

Effectively Final: A keyword before a variable makes it final and no final keyword before a variable make it effectively final provided we never change its value.
int x;
x = 4; //value is never changed ever, so kind of make=ing it effectively final.

A keyword before a variable makes it final and no final keyword before a variable meke it effectively final provided we never change its value.

# Collections

## Consistency

Fail-fast Iteration - Fails on concurrent modification

Fail-safe - Example ConcurrentSkiptList, it is a snapshot of the collection at the time of calling
Weekly consistent - Never throws concurrent modification, however, doesn’t guarantee if all the elements will be returned if concurrent modification happens.

## Unmodifiable Collections 

read only view

source changes are available

get UnsupportedOperation exception, if modified

## Immutable Collections

Read only copy of the source e.g. List.of 

Source changes are not available

get UnsupportedOperation exception, if modified

Null values are not allowed in List.of, List.copyOf

List.of takes collections of elements where List.copyOf takes Collection

## Synchronized Collections

Returns synchronized collections, basically all the operations are implemented under synchronized block

## CopyOnWriteArrayList

Use to synchronize collection

Create a copy of collection when add or set operation is performed

Iterator is fail safe, gets an immutable collection

Best if used only for read operation

## ConcurrentHashMap

Use to synchronize map

Segment/bucket wise locking, segment is calculated based on the same hashing function which is used to store object.

In Put and remove method, it identifies the segment using hashing function and then put a lock on the segment

In get method, there is no lock

Default segment size is 16

## BlockingQueue

The Java BlockingQueue interface represents a queue which can block 

-	threads inserting elements into the queue if the BlockingQueue is full, 

-	or thread removing elements from the queue if the BlockingQueue is empty.

A BlockingQueue is typically used to have one thread produce objects, which another thread consumes.
The producing thread will keep producing new objects and insert them into the BlockingQueue, until the queue reaches some upper bound on what it can contain. It's limit, in other words. If the blocking queue reaches its upper limit, the producing thread is blocked while trying to insert the new object. It remains blocked until a consuming thread takes an object out of the queue.

The consuming thread keeps taking objects out of the BlockingQueue to processes them. If the consuming thread tries to take an object out of an empty queue, the consuming thread is blocked until a producing thread puts an object into the queue.
http://tutorials.jenkov.com/java-util-concurrent/blockingqueue.html

ArrayBlockingQueue

LinkedListBlockingQueue

## Immutable Class

Make all fields final

No setter methods

Implement cloneable, override clone method and throw CloneNotSupported

Implement serializable, override readResolve method

To protect, reflection use enum

Wrapper classes are immutable

## Optional Classes

The main purpose of Optional, as designed by its creators, is to be a return type of methods that previously would return null. Such methods would require us to write boilerplate code to check the return value, and we could sometimes forget to do a defensive check. In Java 8, an Optional return type explicitly requires us to handle null or non-null wrapped values differently

## Functional Interfaces

A functional interface is an interface with one single abstract method (default methods do not count), no more, no less

Consumer – takes one argument returns nothing

Supplier – takes nothing returns Object of type T

UnaryOperator – takes T returns T

BinaryOperator<T> – Represents an operation upon two operands of the same type, producing a result of the same type as the operands
BinaryOperator<Integer> binaryOpt = (s1, s2) -> s1 + s2;
Example: stream.reduce

Function<T,R> – Represents a function that accepts one argument and produces a result.

Type parameters: <T> – the type of the input to the function <R> – the type of the result of the function
  
Function<String, String> func = (s1) -> s1 + "-" + s1;
  
Example: stream.map

Predicate – takes T return Boolean
