---
layout: post
title: "Java 7 New Features"
categories: 
tags: "Java"
---

Java 8 has been released for a while, while Java 7 was released ever longer ago. However, I am still writing code in Java 6. Now my current employer is moving Java 7, so that I can start to enjoy the new features in Java 7.

### Diamond operator
```java
//in Java 6, we need to
Map<String, List<String>> map = new HashMap<String, List<String>>();

//in Java 7, we only need type in the variable type
Map<String, List<String>> map = new HashMap<>();
```


### String in swtich statement
```java
swithc (s) {
   case "AB":
   case "CD":
	return 30;
   case "DE":
        return 20;
   ....
   default:
	return -1;
}
```

### Automatic resource management
```java
try (InputStream in = new FileInputStream(src),
     OutputStream out = new FileOutputStream(dest))
{
    byte[] buffer = new byte[8192];
    int n;
    while ((n = in.read(buff)) > 0) {
	out.write(buff, 0, n);
    }
}
```

### Numeric literals with underscores
```java
int mask = 0b1010_1010_1010;
long big = 9_221_123_333_7838;
float pi = 3.14_15F;
long hexBytes = 0xFF_EC_DE_5E;
```

### Improved exception handling: Multi-Catch
```java
try{
    ...
} catch (ClassCastException e) {
    //Do something
} catch (InstantiationException | InvocationTargetException) {
    //Do some generic actions
}
```
