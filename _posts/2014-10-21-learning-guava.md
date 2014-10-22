---
layout: post
title: "Learning Guava"
categories:
tags: "Java"
---

I have been using Guava for while, mainingly using ```Precondiations``` for agument checking and ```Objects``` for build ```hashCode()``` and ```equals()```. Seems it is a good idea to learn and use more utitlity functions in the wonderful library.

### Strings Classes

#### Charsets

It is used to provide 6 charsets, but in version 18, seems there is only UTF_8 now. 

```Java
bytes = string.getBytes(Charsets.UTF_8);
//Use StandardCharsets in Java 7 and beyond.
bytes = string.getByte(StandardCharsets.UTF_8);
```

#### CharMatcher
- Given a char, it returns true or false
- Implements ```Predicator```

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


### Range
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
