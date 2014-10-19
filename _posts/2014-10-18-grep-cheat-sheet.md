---
layout: post
title: "Grep Cheat Sheet"
categories:
tags: "Linux" 
---

### Basic Usage

```bash
grep -E PATTERN FILE
#or 
egrep PATTERN FILE
```


### Grep Options

Matcher selection options:

```bash
-E, --extended-regexp # Interpret PATTERN as an extended regular expression
```

Matching control options:

```bash
-i, --ignore-case # Ignore case (ie uppercase, lowercase letters).
-v, --invert-match # Invert the match sense, print the non-match lines
-w, --word-regexp # Select only matches that form whole words.
-o, --only-matching # Print only the matched (non-empty) part
```

File search control options:
```bash
-r, --recursive # Search the file recursively, to include subdirectories and to follow symbol links.
```

Output control options:

```bash
-c, --count # Only print the number of matches
-l, --files-with-matches # Only print the file names of matches 
```

Output prefix control options:

```bash
-H, --with-filename # Print the file names as the prefix out of the output
-n, --line-number # Print the line number before each line that matches.
````

Context line control options:

```bash
-A NUM, --after-context=NUM # Print  NUM  lines  of  trailing context after matching lines. 
-B NUM, --before-context=NUM # Print NUM lines of leading context before matching lines.
-C NUM, -NUM, --context=NUM # Print  NUM  lines of output context.
```