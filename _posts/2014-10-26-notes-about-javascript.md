---
layout: post
title: "Notes about JavaScript"
categories:
tags: "FrontEnd"
---

I have been using JavaScript for quite some time. Recently I feel like I need to re-learn it more carefully. I found [this tutorial](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide) from Mozilla Development Netowrk is very useful. I would like to take some notes while reading it.

### Javascript Object

- Any JavaScript function can be used as a constructor. You use the new operator with a constructor function to create a new object.


### [Regular Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)
```javascript
// literal way to create a regular expression
var re = /ab+c/;
// Using RegExp object to create a regular expression
var re = new RegExp("ab+c");

//with flag
var re = /\w+\s/g;
var re = new RegExp("\\w+\\s", "g");
```

Examples of using regular expressions in Javascript.

```javascript
// Escapes regular expression in a string.
function escapeRegExp(string) {
  return string.replace(/([.*+?^${}()|\[\]\/\\])/g, "\\$1");
}

// Replace the 1st and 2nd parenthesized match
var re = /(\w+)\s(\w+)/;
var str = "John Smith";
var newstr = str.replace(re, "$2, $1"); //newstr is "Smith, John");
```


### Closures

Closures are functions that refer to independent (free) variables. In other words, the function defined in the closure 'remembers' the environment in which it was created.

### Module pattern (Anonymous Closures)

```javascript
var MODULE = (function () {
	var my = {};
    var privateVariable = 1;

	function privateMethod() {
		// ...
	}

	my.moduleProperty = 1;
	my.moduleMethod = function () {
		// ...
	};

	return my;
}());
```


##### Reference
- [Module pattern](http://www.adequatelygood.com/JavaScript-Module-Pattern-In-Depth.html)