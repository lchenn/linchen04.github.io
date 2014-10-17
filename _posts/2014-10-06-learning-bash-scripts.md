---
layout: post
title: "Learning Bash Scripts"
categories:
tags: "Linux"
---

### Bash terminal shortcuts

```bash
Ctrl + L # clear the terminal
Ctrl + D # log count
Ctrl + A # Move cursor to the start of line
Ctrl + E # Move cursor to the end of line
Ctrl + U # Delete left of the cursor
Ctrl + K # Delete right of the curor
Ctrl + W # Delete word on the left
Ctrl + Y # Past (after Ctrl + U, K or W)
Ctrl + R # Reverse search bash history
!! # Repeat last command
Ctrl + Z # stop current command and put it into background
```

### Ways to execute Bash scripts

```bash
./alice.sh # Execute directly, ```chmod +x``` is required, script will run in a sub-shell.
source alice.sh #Source in script, script will run in current shell
./alice.sh & #Run in background, script will run in a sub-shell in the background
```

### Functions
Two ways to define a function:

```bash
function function_name {
}
#Or
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

```bash
$var
# or
${var}

# It is safe to omit the curly brackets ({}) 
# if the variable is not followed by a character that is not a letter, digit, or underscore.

Example:
echo $UID_ #it shold be ${UID}_, otherwise, the variable name is considered at "UID_"
```

#### Positional parameters
Positional parameters are built-in variables, they hold the command-line arguments to the scripts when they are invoked.

```bash
$#: #the count of parameters
$0: #the name of the script
$1: #the first parameter
$*: #a single string containing all the positional parameters, separated by the 1st character in the ```IFS``` environment variable. It is like "$1 IFS $2 IFS $3 IFS ... $N"
$@: #equals "$1" "$2" "$3" ... "$N"
$?: #returns the exit status of the last command
$$: #returns the processs id of the script
$-: #returns the options given to the shell
```
Example:

```bash
IFS=,
echo "$*"
### run it, it will output "$1,$2,$3,..."
```


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

### Quoting

```bash
\c             #Take character c literally.
`cmd`          #Run cmd and replace it in the line of code with its output.
"whatever"     #Take whatever literally, after first interpreting $, `...`, \
'whatever'     #Take whatever absolutely literally.
```

Example:

```bash
match=`ls *.bak`        #Puts names of .bak files into shell variable match.
echo \*                 #Echos * to screen, not all filename as in:  echo *
echo '$1$2hello'        #Writes literally $1$2hello on screen.
echo "$1$2hello"        #Writes value of parameters 1 and 2 and string hello.
```

### Pattern Matching
```bash
*              #Matches 0 or more characters.
?              #Matches 1 character.
[AaBbCc]       #Example: matches any 1 char from the list.
[^RGB]         #Example: matches any 1 char not in the list.
[a-g]          #Example: matches any 1 char from this range.
```

### Grouping
Parentheses may be used for grouping, but must be preceded by backslashes since parentheses normally have a different meaning to the shell (namely to run a command or commands in a subshell). For example, you might use:

```bash
if test \( -r $file1 -a -r $file2 \) -o \( -r $1 -a -r $2 \)
then
    #do whatever
fi
```


#### String Concatenation
#### String Extraction

### Condition
```bash
if [ -s file ]
then
    #such and such
fi
```

### Loops

```bash
for item in [list]
do
    echo $item
done

for item in [list]; do
    echo $item
done
```

[list] can be supplied multiple ways
```bash
# directly
NUMBERS="1 2 3"
for number in `echo $NUMBERS`
do
    echo $number 
done

for number in $NUMBERS
do
    echo -n $number
done

for number in 1 2 3
do
    echo -n $number
done

## list is supplied as glob pattern 
for file in *.tar.gz
do
    tar -xzf $file
done

## [list] is supplied using a statement
for x in `ls -tr *.log`
do
    cat $x >> biglog
done
```

### Case statement
```bash
case "$1" in
    a) cmd1 ;;
    b) cmd2 ;;
    c) cmd3 ;;
    *) cmd4 ;;
esac
```


### Testers

#### File Testers
```bash
-r file     #Check if file is readable.
-w file     #Check if file is writable.
-x file     #Check if we have execute access to file.
-f file     #Check if file is an ordinary file (not a directory, a device file, etc.)
-s file     #Check if file has size greater than 0.
-d file     #Check if file is a directory.
-e file     #Check if file exists.  Is true even if file is a directory.
```

#### String Testers
```bash
s1 = s2     #Check if s1 equals s2.
s1 != s2    #Check if s1 is not equal to s2.
-z s1       #Check if s1 has size 0.
-n s1       #Check if s2 has nonzero size.
s1          #Check if s1 is not the empty string.
```

#### Numbers Tester
Note that a shell variable could contain a string that represents a number. If you want to check the numerical value use one of the following:

```bash
n1 -eq n2      #Check to see if n1 equals n2.
n1 -ne n2      #Check to see if n1 is not equal to n2.
n1 -lt n2      #Check to see if n1 < n2.
n1 -le n2      #Check to see if n1 <= n2.
n1 -gt n2      #Check to see if n1 > n2.
n1 -ge n2      #Check to see if n1 >= n2.
```

#### Boolean operators

```bash
!     #not
-a    #and
-o    #or
```

Examples:

```bash
if [ $num -lt 10 -o $num -gt 100 ]
then
    echo "Number $num is out of range"
elif [ ! -w $filename ]
then
    echo "Cannot write to $filename"
fi
```


### Shell Arithmetic

```bash
result=`expr $1 + 2`
result2=`expr $2 + $1 / 2`
result=`expr $2 \* 5`               #note the \ on the * symbol
```

With bash, an expression is normally enclosed using [ ] and can use the following operators, in order of precedence:

```bash
* / %       #(times, divide, remainder)
+ -         #(add, subtract)
< > <= >=   #(the obvious comparison operators)
== !=       #(equal to, not equal to)
&&          #(logical and)
||          #(logical or)
=           #(assignment)
```

### Order of Interpretation
The bash shell carries out its various types of interpretation for each line in the following order:

```bash
brace expansion         (see a reference book)
~ expansion             (for login ids)
parameters              (such as $1)
variables               (such as $var)
command substitution    (Example:  match=`grep DNS *` )
arithmetic              (from left to right)
word splitting
pathname expansion      (using *, ?, and [abc] )
```


### Other Shell Features

```bash
$var           #Value of shell variable var.
${var}abc      #Example: value of shell variable var with string abc appended.
var=value      #Assign the string value to shell variable var.
cmd1 && cmd2   #Run cmd1, then if cmd1 successful run cmd2, otherwise skip.
cmd1 || cmd2   #Run cmd1, then if cmd1 not successful run cmd2, otherwise skip.
cmd1; cmd2     #Do cmd1 and then cmd2.
cmd1 & cmd2    #Do cmd1, start cmd2 without waiting for cmd1 to finish.
(cmds)         #Run cmds (commands) in a subshell.
```

###### References
- A lot of content came from [here](http://www.johnstowers.co.nz/blog/pages/bash-cheat-sheet.html)
