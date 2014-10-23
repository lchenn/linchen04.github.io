---
layout: post
title: "Learning Guava"
categories:
tags: "Java"
---

I have been using Guava for while, mainingly using ```Precondiations``` for agument checking and ```Objects``` for build ```hashCode()``` and ```equals()```. Seems it is a good idea to learn and use more utitlity functions in the wonderful library.

### Basic Utilities

#### Objects

```java
// Objects.equal()
Objects.equal("a", "a"); // returns true
Objects.equal(null, "a"); // returns false
Objects.equal("a", null); // returns false
Objects.equal(null, null); // returns true

// Objects.toStringHelper
// Returns "ClassName{x=1}"
Objects.toStringHelper(this)
    .add("x", 1)
    .toString();

// Returns "MyObject{x=1}"
Objects.toStringHelper("MyObject")
    .add("x", 1)
    .toString();

// Returns the first of two given parameters that is not null,
// if either is, or otherwise throws a NullPointerException.
Objects.firstNonNull(string1, string2)

// Implement Objects.hashCode
Objects.hashCode(field1, field2, ..., fieldn)

// Implement Comparable
ComparisonChain.start()
    .compare(this.aString, that.aString)
    .compare(this.anInt, that.anInt)
    .compare(this.anEnum, that.anEnum, Ordering.natural().nullsLast())
    .result();
```


#### Preconditions

Preconditions are used to check some conditions before executing some commands. If the conditions are not met, an Exception will be thrown.

```java
- checkArgument(boolean) // throws IllegalArgumentException
- checkNotNull(T) // NullPointerException, if T is not null, return the value.
- checkState(boolean) // throws IllegalStateException
- checkElementIndex(int index, int size) // IndexOutOfBoundsException; returns index.
- checkPositionIndex(int index, int size) // IndexOutOfBoundsException; returns index.
```

Most of the methods has three signatures. "%" is used to specify a parameter in the template for the error message.

```java
- checkXxx(T)
- checkXxx(T, String message)
- checkXxx(T, String messageTemplate, Object...parameters)
```

### Strings Classes

#### Strings
Strings has been simplified, now it contains a few String null/empty check and operate method, and a few padding method.

```java
- nullToEmpty(String) // if it's null, return empty;
- emptyToNull(String) // if it's empty return null
- isNullOrEmpty(String) // test if empty or null
//
- paddingStart(String, int minLength, char padChar)
- padEnd(String, int minLength, padChar)
- repeat(String, int count)
```

#### Charsets

It is used to provide 6 charsets, but in version 18, seems there is only UTF_8 now. 

```Java
bytes = string.getBytes(Charsets.UTF_8);
//Use StandardCharsets in Java 7 and beyond.
bytes = string.getByte(StandardCharsets.UTF_8);
```

#### CharMatcher
- Given a char, it returns true or false
- Implements ```Predicate```

```java
// remove control characters from the input string
String noControlString = CharMatcher.JAVA_ISO_CONTROL.removeFrom(string);
// only retain digits
String theDigits = CharMatcher.DIGIT.retainFrom(string)
// trim whitespace at ends, and replace/collapse whitespace into single spaces
String spaced = CharMatcher.WHITESPACE.trimAndCollapseFrom(string, ' ');
// replace all the digit with star
String stared = CharMatcher.JAVA_DIGIT.replaceFrom(string, "*");
// only keep digit and lowercased
String lowerAndDigit = 
	CharMatcher.JAVA_DIGIT.or(CharMatcher.JAVA_LOWER_CASE).retainFrom(string);
```

Ways to construct a CharMatcher:

```java
- anyOf(CharSequence)
- is(char)
- inRange(char, char)
- negate()
- and(CharMatcher)
- or(CharMatcher)
```

Ways to use CharMatchers:

```java
- collapseFrom(CharSequence, char) //replace each group of matching chars with the char.
- matchesAllOf(CharSequence) // Test if this matcher matches all chars in the sequence.
- removeFrom(CharSequence) // Removes matching chars from the sequence.
- retainFrom(CharSequence) // Retains matching chars from the sequence.
- trimFrom(CharSequence)   // Remove leading/trailing matching chars.
- replaceFrom(CharSequence, CharSequence) // Replace matching chars with a given sequence.
```

#### Joiner
Join a collection of objects into a string.

```java
//will return "Harry; Ron; Herminoe"
Joiner.on("; ").skipNulls().join("Harry", null, "Non", "Herminone");
```

#### Splitter
Split a String using some chars.

```java
//will return "foo", "bar", and "qux", in Iterable<String> format
Splitter.on(',').trimResults.omitEmptyStrings().split("foo,bar,,    qux");
```
A Splitter can be created using a Pattern, char, String, or CharMatcher

Options to modify a Splitter.

```java
- omitEmptyStrings()  //omit empty strings
- trimResults()	    // trim whitespaces from each splitted field
- trimResults(CharMatcher) //trim the chars matching the specified CharMatcher
- limit(int)  //stop splitting after the specified number of strings
```

#### CaseFormat
Utility class to convert ASCII cases.

```java
// Will return "constantName"
CaseFormat.UPPER_UNDERSCORE.TO(CaseFormat.LOWER_CAMEL, "CONSTANT_NAME");
```

The predefined CaseFormats are:

```java
- LOWER_CAMEL // lowserCamel
- LOWER_HYPHEN // lower-hygen
- LOWER_UNDERSCORE // lower-underscore
- UPPER_CAMEL //UpperCamel
- UPPER_UNDERSCORE //UPPER_UNDERSCORE
```

### Collections

#### Range
Defines boundaries around a continuous span values of of some ```Comparable``` types.

Static methods to create Ranges.

```java
- open(C,C) // (a..b)
- closed(C, C) //  [a..b]
- closedOpen(C, C) // [a..b)
- openClosed(C, C) // (a..b]
- greaterThan(C) // (a..+∞)
- atLeast(C) // [a..++∞)
- lessThan(C) // (-∞..b)
- atMost(C) // (-∞..b]
- all() // (-∞..+∞)
```

The fundamental operation of a Range is its contains(C)

```java
Range.closed(1, 3).contains(2); // returns true
Range.closed(1, 4).containsAll(Ints.asList(1, 2, 3)); // returns true
```

Other operations:

```java
// Query operations
- isEmpty() // test if the range is empty, such as [a, a)
- hasLowerBound()
- hasUpperBound()
- lowerBoundType()
- upperBoundType()
- LowerEndpoint()
// Examples
Range.open(4, 4).isEmpty(); // Range.open throws IllegalArgumentException
Range.closed(3, 10).lowerEndpoint(); // returns 3
Range.open(3, 10).lowerEndpoint(); // returns 3
Range.closed(3, 10).lowerBoundType(); // returns CLOSED
Range.open(3, 10).upperBoundType(); // returns OPEN
```

Interval operations:


enclose(Range):  If the bounds of the inner range do not extend outside the bounds of the outer range. 
isConnected(Range):  Tests if these ranges are connected.

```java
Range.closed(3, 5).isConnected(Range.open(5, 10)); // returns true????
Range.closed(0, 9).isConnected(Range.closed(3, 4)); // returns true
Range.closed(0, 5).isConnected(Range.closed(3, 9)); // returns true
Range.open(3, 5).isConnected(Range.open(5, 10)); // returns false
Range.closed(1, 5).isConnected(Range.closed(6, 10)); // returns false
```

intersection(Range): Returns the maximal range enclosed by both this range and other. if it doesn't exist,  throws an IllegalArgumentException.

```java
Range.closed(3, 5).intersection(Range.open(5, 10)); // returns (5, 5]
Range.closed(0, 9).intersection(Range.closed(3, 4)); // returns [3, 4]
Range.closed(0, 5).intersection(Range.closed(3, 9)); // returns [3, 5]
Range.open(3, 5).intersection(Range.open(5, 10)); // throws IAE
Range.closed(1, 5).intersection(Range.closed(6, 10)); // throws IAE
```
                    
span(Range): Returns the minimal range that encloses both this range and other.  If the ranges are both connected, this is their union.

```java
Range.closed(3, 5).span(Range.open(5, 10)); // returns [3, 10)
Range.closed(0, 9).span(Range.closed(3, 4)); // returns [0, 9]
Range.closed(0, 5).span(Range.closed(3, 9)); // returns [0, 9]
Range.open(3, 5).span(Range.open(5, 10)); // returns (3, 10)
Range.closed(1, 5).span(Range.closed(6, 10)); // returns [1, 10]
```

#### Multiset

#### Multimap

#### Bimap

#### Table

#### Immutables


### Functional Programming

#### Predicate
#### Function

### Cache

LoadingCache
CacheBuilder
CacheLoader

### Working with Files



### EventBus

EventBus allows publish-subscribe-style communication between components without requiring the components to explicitly register with one another (and thus be aware of each other). It is designed exclusively to replace traditional Java in-process event distribution using explicit registration. It is not a general-purpose publish-subscribe system, nor is it intended for interprocess communication.

Glossary, came from the (wiki)[https://code.google.com/p/guava-libraries/wiki/EventBusExplained]

| Name  | Description |
|-------|-------------|
| Event | Any object that may be posted to a bus. |
| Subscribing | The act of registering a listener with an EventBus, so that its handler methods will receive events. |
| Listener | An object that wishes to receive events, by exposing handler methods. |
| Handler method | A public method that the EventBus should use to deliver posted events. Handler methods are marked by the Subscribe annotation. |
| Posting an event | Making the event available to any listeners through the EventBus. |


An example is below.

```java
public class EventBusExample {

    /**
     * An Event, can be any class
     */
    public static class EventA {
        public String toString() {
            return "Event A";
        }
    }

    /**
     * Another Event, can be any class
     */
    public static class EventB {
        public String toString() {
            return "Event B";
        }
    }

    /**
     * A different event for multi-thread
     */
    public static class EventC {
        public String toString() {
            return "Event C";
        }
    }


    public static class EventD {
        public String toString() {
            return "Event D";
        }
    }

    /**
     * The event which are not handled in this example.
     */
    public static class EventE {
        public String toString() {
            return "Event E";
        }
    }

    /**
     * Listener in the Glossary
     */
    public static class EventListener {

        /**
         * Subscribing in the Glossary, this is also a Handler method
         */
        @Subscribe
        public void onEvent(EventA e) {
            System.out.println("I subscribed EventA, I received: :" + e);
        }

        @Subscribe
        public void onEvent(EventB e) {
            System.out.println("I subscribed EventB, I received: :" + e);
        }

        /**
         * AllowConcurrentEvents marks an event handling method as being thread-safe.
         * It indicates that EventBus may invoke the event
         * handler simultaneously from multiple threads.
         */
        @Subscribe
        @AllowConcurrentEvents
        public void onEvent(EventC e) throws InterruptedException {
            String name = Thread.currentThread().getName();
            System.out.format("%s sleep for 1000 ms%n", name);
            Thread.sleep(1000);
            System.out.println(name + "I subscribed EventC, I received: :" + e);
            System.out.format("%s sleep done%n", name);
            System.out.println(e.toString());
        }

        @Subscribe
        public void onEvent(EventD e) throws InterruptedException {
            String name = Thread.currentThread().getName();
            System.out.format("%s sleep for 1000 ms%n", name);
            Thread.sleep(1000);
            System.out.println(name + "I subscribed EventD, I received: :" + e);
            System.out.format("%s sleep done%n", name);
        }

        /**
         * DeadEvent is used to hand all the Events
         * which are posted to this EventListener,
         * but they are handled by other Subscribe methods.
         */
        @Subscribe
        public void onEvent(DeadEvent de) {
            System.out.println("Got a DeadEvent" + de.getEvent());
        }

    }

    public static void main(String[] args) throws InterruptedException {
        EventBus eb = new EventBus();
        eb.register(new EventListener());

        // Posting an event
        System.out.println("----------Trigger EventA---------");
        eb.post(new EventA());
        // Posting a different event
        System.out.println("----------Trigger EventB---------");
        eb.post(new EventB());
        // Posting a DeadEvent
        System.out.println("----------Trigger EventE---------");
        eb.post(new EventE());
        // Multi-thread event
        System.out.println("----------Trigger EventC---------");
        ExecutorService threadPool = Executors.newCachedThreadPool();
        eb = new AsyncEventBus(threadPool);
        eb.register(new EventListener());
        for (int i = 0; i < 20; i++) {
            eb.post(new EventC());
        }
        System.out.println("----------Trigger EventD---------");
        for (int i = 0; i < 20; i++) {
            eb.post(new EventD());
        }
        Thread.sleep(2000);
        threadPool.shutdown();
    }
}
```


