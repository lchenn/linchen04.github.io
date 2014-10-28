---
layout: post
title: "Sed By Examples"
categories:
tags: "Linux"
---


### Basics



#### Use sed to replace line break
An example to replace a line break:

```bash
$ sed ':a;N;$!ba;s/\n/ /g' file
# The explanation is:
# 1. :a create a label 'a'
# 2: N append the next line to the pattern space
# 3: $! if not the last line, ba branch (go to) label 'a'
# 4: s substitute, /\n/ regex for new line, / / by a space, 
#    /g global match (as many times as it can)
```
[reference](http://stackoverflow.com/questions/1251999/sed-how-can-i-replace-a-newline-n)
