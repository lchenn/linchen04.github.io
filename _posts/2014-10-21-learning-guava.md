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

``java
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


