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

