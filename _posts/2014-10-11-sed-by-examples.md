---
layout: post
title: "Sed By Examples"
categories:
tags: "Linux"
---

### Basics
#### Synopsis
```bash
$ sed [options] '[[address1,[address2]][!]{cmd}' file
```

#### Options
```bash
-n, --quiet, --silent # Suppress automatic printing of pattern space
-e script, --expression=script # Add the script to the commands to be executed
```

#### Addresses
An address can be either a regular expression enclosed by forward slashes /regex/, or a line number. The ***$*** symbol can be used in place of a line number to denote the last line.

If one address is given, then the command is applied to lines containing that address. If two addresses are given separated by a comma, then the command is applied to all lines between the two lines that match the pattern.

Examples:

```bash
# Replace "my" with "yours" from line 1 to 5
$ sed '1,5s/my/yours/g' file.txt
# Add a "# " to the 3 lines after the 1st appearance of "dog"
$ sed '/dog/,+3s/^/# /g' file.txt
# Delete the 2nd line
$ sed '2d' file.txt
# Delete from the 2nd line to the end of the file
$ sed '2,$d' file.txt
```


#### Pattern Space
```c
# Pseudo code
foreach line in file {
    // Put a line into Pattern_Space
    Pattern_Space <= line;
    // For each pattern space, execute sed command
    Pattern_Space <= EXEC(sed_cmd, Pattern_Space);
    // If no "-n", print the pattern space
    if (sed option hasn't "-n")  {
       print Pattern_Space
    }
}
````

#### Commands
```
a text # Append text, which has each embedded newline preceded by a backslash.
c text # Replace the selected lines with text, which has each embedded newline preceded by a backslash.
d # Delete pattern space.  Start next cycle.
p # Print the current pattern space
```


#### Regular expression in Sed
```bash
(character)\{n\} # Match exactly n repetitions of (character)
\(expression\) # Group operator.
\n # Backreference - matches nth group
```

### Example input: pets.txt
```text
This is my cat, my cat's name is betty
This is my dog, my dog's name is frank
This is my fish, my fish's name is george
This is my goat, my goat's name is adam
```

### Sed as a substitution tool
#### Basic command synopsis

```bash
$ sed '[address1[ ,address2]]s/pattern/replacement/[flags]' <file>
```

#### Flags
If no flags are specified the first match on the line is replaced. The flags can be any of the following:

```bash
n # Replace nth instance of pattern with replacement
g # Replace all instances of pattern with replacement
p # Write pattern space to STDOUT if a successful substitution takes place
w file # Write the pattern space to file if a successful substitution takes place
```

#### Use Sed to substitute examples
Only replace the 3rd to the 6th line:

```bash
$ sed '1,2s/my/yours/g' pets.txt
# This is yours cat, yours cat's name is betty
# This is yours dog, yours dog's name is frank
# This is my fish, my fish's name is george
# This is my goat, my goat's name is adam
```

Only replace the 1st "my" for each line:

```bash
$ sed 's/my/yours/1' file.txt
# This is yours cat, my cat's name is betty
# This is yours dog, my dog's name is frank
# This is yours fish, my fish's name is george
# This is yours goat, my goat's name is adam
```


Only replace the "my" from the 2nd match in each line

```bash
$ sed 's/my/yours/2g' file.txt
# This is my cat, yours cat's name is betty
# This is my dog, yours dog's name is frank
# This is my fish, yours fish's name is george
# This is my goat, yours goat's name is adam
```

Put a [] around "my", ***&*** refers to the matched part.

```bash
$ sed 's/my/[&]/g' file.txt
# This is [my] cat, [my] cat's name is betty
# This is [my] dog, [my] dog's name is frank
# This is [my] fish, [my] fish's name is george
# This is [my] goat, [my] goat's name is adam
```

Extract pets' types and names, \1, \2 can refer to match groups, denoted by ()

```
$ sed 's/This is my \([^,]*\),.*is \(.*\)/\1:\2/g' my.txt
# cat:betty
# dog:frank
# fish:george
# goat:adam
```

#### Use ***c*** to replace full line
```bash
sed '[address1[,address2]]c text <file.txt>
```

Examples

Replace the 2nd line

```bash
$ sed "2 c This is my monkey, my monkey's name is wukong" my.txt
# This is my cat, my cat's name is betty
# This is my monkey, my monkey's name is wukong
# This is my fish, my fish's name is george
# This is my goat, my goat's name is adam
```

Replace the lines having fish.

```bash
$ sed "/fish/c This is my monkey, my monkey's name is wukong" my.txt
# This is my cat, my cat's name is betty
# This is my dog, my dog's name is frank
# This is my monkey, my monkey's name is wukong
# This is my goat, my goat's name is adam
```


#### Use ***d*** to delete lines
```bash
sed '[address1[,address2]]d <file.txt>
```

Examples

```bash
# Delete lines containing fish
$ sed '/fish/d' my.txt
# Delete the 2nd line
$ sed '2d' my.txt
# Delete from the 2nd line
$ sed '2,$d' my.txt
```

#### Use ***p*** to print lines
Use -n to only print the matched lines.

Examples:

```bash
# Print the lines containing fish
$ sed -n '/fish/p' my.txt
# Print from the 1st line having "dog" to the 1st line having "fish"
$ sed -n '/dog/,/fish/p' my.txt
# Print the 2nd line to the first match of "fish"
$ sed -n '1,/fish/p' my.txt
```


#### Use ***i*** and ***a*** to insert and append lines
```bash
# Insert text in the 1st line, inserted will be the 1st
$ sed "1 i This is my monkey, my monkey's name is wukong" my.txt
# Append text after the 1st line, inserted will be the 2nd
$ sed "1 a This is my monkey, my monkey's name is wukong" my.txt
# Insert a line after every line matching fish
$ sed "/fish/a This is my monkey, my monkey's name is wukong" my.txt
```


#### Use multiple commands

Examples
```bash
# From line 3 to 6, matching "This", then match "fish", then d
$ sed '3,6 {/This/{/fish/d}}' pets.txt
# If a line having "This", delete it. If there is a space, trim it
$ sed '1,${/This/d;s/^ *//g}' pets.txt
```


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
[coolshell](http://coolshell.cn/articles/9104.html)
[panix](http://www.panix.com/~elflord/unix/sed.html)

