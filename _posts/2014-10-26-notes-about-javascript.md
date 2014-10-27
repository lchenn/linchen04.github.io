---
layout: post
title: "Notes about JavaScript"
categories:
tags: "FrontEnd"
---

I have been using JavaScript for quite some time. Recently I feel like I need to re-learn it more carefully. I found [this tutorial](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide) from Mozilla Development Netowrk is very useful. I would like to take some notes while reading it.

### Javascript Object

- Any JavaScript function can be used as a constructor. You use the new operator with a constructor function to create a new object.

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