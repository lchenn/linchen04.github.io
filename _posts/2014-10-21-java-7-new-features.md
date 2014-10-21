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

### Improved exception handling

Multi-Catch

```java
try {
    ...
} catch (ClassCastException e) {
    //Do something
} catch (InstantiationException | InvocationTargetException) {
    //Do some generic actions
}
```

More precise rethrow

```java
public void foo(String bar) throws FirstException, SecondExcepiton {
    try {    
	//code that may throw both FirstException and SecondException
    } catch (Exception e) {
	throw e;
	//this doesn't work prior to Java 7
    }
}
```

### Java NIO 2
#### Files, Paths, Path, FileSystem
- Class java.nio.file.Paths
- Interface  java.nio.file.Path
- Class java.nio.file.Files
- Class java.nio.file.FileSystem

Use ```Paths``` to get a ```Path```. Use ```Files``` to do stuff.

```java
Path src = Paths.get(“/home/fred/readme.txt”);
Path dst = Paths.get(“/home/fred/copy_readme.txt”);
Files.copy(src, dst, 
	StandardCopyOption.COPY_ATTRIBUTES,
	StandardCopyOption.REPLACE_EXISTING);
```

Use ```DirectoryStream``` to support directory operations:
- Implements Iterable and Closeable interfaces
- Built-in supoort for glob, regex and custom filters

```java
Path srcPath = Path.get("/home/user/src");
try (DirectoryStream<Path> dir = srcPath.newDirectoryStream("*.java")) {
    for (Path file: dir) {
	//do something to the file
    }
}
```

Use ```FileVisitor``` to walk through a File tree.

```java
    Path startingDir = Paths.get("/home/user/src");
    PrintFiles printFileVisitor = new PrintFiles();
    Files.walFileTree(stringDir, printFileVisitor);
```

### JDBC 4.1
Try-with-resources statement to automatically close resource of type Connection, ResultSet, and Statement

```java
try (Statement statement = conn.createStatement()) {
    // ...
}
```


##### Reference
- Examples came from [here](http://www.slideshare.net/boulderjug/55-things-in-java-7)
