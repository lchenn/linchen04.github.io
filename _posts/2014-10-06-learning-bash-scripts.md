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

### Shell Variables
- Shell variables are named places to store data, and their values can be obtained by ```$variable_name```
- ***Environment variables***, are conventionally named in ***all capital letters***, and their values are made known to subprocesses using ```export``` command

#### Variable syntax
Shell variables can be in two format:
- $var
- ${var}

It is safe to omit the curly brackets ({}) if the variable is not followed by a character that is not a letter, digit, or underscore.

```bash
### it shold be ${UID}_, otherwise, the variable name is considered at "UID_"
echo $UID_ 
```

#### Positional parameters
Positional parameters are built-in variables, they hold the command-line arguments to the scripts when they are invoked.
- $#: the count of parameters
- $0: the name of the script
- $1: the first parameter
- $*: a single string containing all the positional parameters, separated by the 1st character in the ```IFS``` environment variable. It is like "$1 IFS $2 IFS $3 IFS ... $N"

```bash
IFS=,
echo "$*"
### run it, it will output "$1,$2,$3,..."
```


- $@: equals "$1" "$2" "$3" ... "$N"

Positional parameters are read-only.

#### Positional parameters in functions
- Arguments to the functions are local.
- A function can change the value defined outside of the function.
- ```local``` can be used to define local variables


### String Operators

Substitution operators

- ${varname:-word}: if varname exists and is not null, return its value; otherwise return word 

```bash
${count:-0}
# if count is defined, return its value
# otherwise, return 0
```
- ${varname:=word}: if varname exists and is not null, return its value; otherwise, set varname to word, and return word.

```bash
${count:=0}
# if count is defined, return its value
# otherwise, count will be 0, and return 0
```

- ${varname:?message}: if var exists and is not null, return its value; otherwise, print: varname: followed by message, and abort current command or script. Omitting message produces the default message ***parameter null or not set***

```bash
${count:?"undefined"}
# if count is not defined, prints "count:undefined!"
# otherwise, return the value of count
```

- ${varname:+word}: if varname exists and is not null, return ***word***; otherwise, return ***null***
```bash
${count:+1}
# if count is defined, return 1
# otherwise, return null
```

- ${varname:offset:length}: perform substring expansion. 
```bash
count="frogfottman"
${count:4} ### it returns footman
${count:4:4} ### it returns foot
```

#### String Concatenation
#### String Extraction

### Condition

### Loop


### Testers

### File


