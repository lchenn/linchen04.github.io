---
layout: post
title: "Effiective Java Notes"
categories:
tags: "Java"
---

### Item 8 Overriding equals()

1. Use the == operator to check if the argument is a reference to this object.
2. Use the instanceof operator to check if the argument has the correct type.
3. Cast the argument to the correct type.
4. For each “significant” field in the class, check if that field of the argument matches the corresponding field of this object. 
    - Use ***Float.compare*** and ***Double.compare*** for float and double type.
    - Avoid NullPointerException
    
        (field == null ? o.field == null : field.equals(o.field))
    
5. Is it symmetric? Is it transitive? Is it consistent

### Item 13 Minimizing the accessibility of classes and members

- The rule of thumb: ***Make each class or member as inaccessible as possible***
- Instance fields should never be public
- Classes with public mutable fields are not thread-safe
- Nonzero-length array is always mutable, a class should not have a public static final array field, or an accessor that returns such a field

### Item 15 Minimize mutability

- Immutable objects are inherently thread-safe; they require no synchronization.
- The disadvantage of immutable classes is that they require a separate object for each distinct value. 
- To make a class immutable, we can 1) Make the class final 2) Make constructor private or package-private, and provide public factory method where the original constructor is.




## Section 8

### Item 45 Minimize the scope of local variables
- Prefer ```for``` loop to ```while``` loop. ```for``` loop provides a place to initialize ```loop variable```

    ```java
    //this is not that good
    Iterator<Element> i = c.iterator();
    while (i.hasNext()) {
        doSomething(i.next());
    }

    //this is better
    for (Iterator i = c.iterator(); i.hasNext(); ) {
        doSomething(i.next());
    }
    ```

### Item 46 Prefer for-each loop to traditional ```for``` loop
- for-each loop is better in general
- Implement the ```Iterable``` interface will enable the support of for-each loop

    ```java
    public interface Iterable<E> {
        Iterator<E> iterator();
    }
    ```

### Item 47 Know and use the libraries
- Libraries is written and tested
- Standard libraries to lear
  * java.lang
  * java.util
  * java.io
  * java.util.concurrent


### Item 48 Regarding float and double
- Use ```BigDecimal```, ```int``` or ```long``` for currency calculation


### Item 51 String concatenation
- Use StringBuilder when a lot of String need to be concatenated


## Section 9: Exceptions

### Item 60: Favor the use of standard exceptions
- IllegalArgumentException
- IllegalStateException
- NullPointerException
- IndexOutOfBoundsException
- ConcurrentModificationException
- UnsupportedOperationException
- ArithmeticException
- NumberFormatException

### Item 62: Document all exceptions thrown by each method
### Item 63: Include failure-capture information in detail messages
### Item 65: Don’t ignore exceptions
Don't do this:

```java
//empty catch, it is like turning of the alarm
try {
} catch (SomeException e) {
}
```
