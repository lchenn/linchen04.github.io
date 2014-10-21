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
```

