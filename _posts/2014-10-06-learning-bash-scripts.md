---
layout: post
title: "Learning Bash Scripts"
categories:
tags: "Linux"
---

### Ways to execute Bash scripts
- Execute directly, ```chmod +x``` is required, script will run in a sub-shell.

```bash
./alice.sh
```

- Source in script, script will run in current shell.

```bash
source alice.sh
```

- Run in background, script will run in a sub-shell in the background

```bash
./alice.sh &
```

### Functions
Two ways to define a function:

```bash
function function_name {
}
```
Or:

```bash
function_name() {
}
```

To delete the definition of a function:

```bash
unset -f function_name
```

Functions are different from scripts:

- Functions do not run in separate processes.
- If a function has the same name as a script, function takes precedence.


### Order of Precedence When Bash interprets A Command
1. Alias
2. Keywords such ***function***, ***if***, and ***for***
3. Functions
4. Built-ins like ***cd*** and ***type***
5. Scripts and executable programs, for which the shell searches in the directories listed in the ***PATH*** environment variable

```type``` can show how the shell will interpret a command.

### Comment

### Variables


### String Operation
#### String Concatenation
#### String Extraction

### Condition

### Loop


### Testers

### File


