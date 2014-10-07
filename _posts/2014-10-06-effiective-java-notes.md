---
layout: post
title: "Effiective Java Notes"
categories:
tags: "Java"
---

## Item 8 Overriding equals()

1. Use the == operator to check if the argument is a reference to this object.
2. Use the instanceof operator to check if the argument has the correct type.
3. Cast the argument to the correct type.
4. For each “significant” field in the class, check if that field of the argument matches the corresponding field of this object. 
    - Use ***Float.compare*** and ***Double.compare*** for float and double type.
    - Avoid NullPointerException
    
        (field == null ? o.field == null : field.equals(o.field))
    
5. Is it symmetric? Is it transitive? Is it consistent

## Item 13 Minimizing the accessibility of classes and members

- The rule of thumb: ***Make each class or member as inaccessible as possible***
