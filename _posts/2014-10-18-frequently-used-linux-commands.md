---
layout: post
title: "Frequently Used Linux Commands"
categories:
tags: "Linux"
---

### Frequently Used

#### Execute a command without saving it in the history
```bash
<space>command
``` 
#### Execute the last command with sudo  
```bash
sudo !!
```
#### Last argument of the last command
```bash
!$
# Example
mkdir /tmp/abcd
cd !$
echo $(pwd) # will print "/tmp/abcd"   
```

#### Put a command into history without execute it
```bash  
# alt + # (alt + shift + #) 
```

#### Runs previous command but replacing
```bash
^foo^bar # replace "foo" with "bar" in previous command
```

#### Execute a command at a given time
```bash
echo "ls -l" | at midnight
# OR
at midnight<<<'ls -l'
```

#### Get the external IP address 
```bash
curl ifconfig.me
```

#### Mount folder/filesystem through SSH
```bash
sshfs name@server:/path/to/folder /path/to/mount/point
```

#### Mount a temporary ram partition
```bash
mount -t tmpfs tmpfs /mnt -o size=1024m
```

#### Create a SSH tunnel
```bash
ssh -N -L2001:localhost:80 somemachine
# start a tunnel from some machine's port 80 to your local post 2001
```

#### Run a command and  redirect stderr and stdout to a file
```bash
command > a.log 2>&1 &
```

#### Use () to create subshell
```bash
# do something in current dir
(cd /some/other/dir; other-command)
# continue in original dir
```

#### here document
```bash
tr a-z A-Z <<END_TEXT
> one two three
> uno dos tres
> END_TEXT

# output
ONE TWO THREE
UNO DOS TRES
```

### sort

```bash
-b, --ignore-leading-blanks # Ignore leading blanks
-f, --ignore-case # Fold lowercase to upper case to sort
-i, --ignore-nonprinting # Consider only printable characters
-h, --human-numeric-sort # compare human readable numbers (e.g., 2K 1G)
-r, --reverse # Reverse the result of comparisons
-n, --numeric-sort # Compare according to string numerical value
-R, --random-sort # Sort by random hash of keys
-o, --output=FILE # Write result to FILE instead of standard output
```

Sort by field options:

```bash
-t, --field-separator=SEP #Use SEP instead of non-blank to blank transition
-k, --key=KEYDEF # Sort via a key; KEYDEF gives location and type
    # KEYDEF  is F[.C][OPTS][,F[.C][OPTS]] for start and stop position, 
    # where F is a field number and C a character position in the field; 
    # both are ori‐ gin 1, and the stop position defaults to the line's end.  
```

Examples:

Input, cat.txt
```
Solaris,10
Linux,20
AIX,25
Linux,25
Unix,30
HPUX,100
```

```bash
cat cat.txt | sort -n  # Sort cat.txt using numeric-sort
cat cat.txt | sort -t"," -k2,2nr 
        # Sort cat.txt by the second field, 
        # numeric-sort and in reversed order, fields are separated by ","
```


### tar
Stores and extracts files from a tape or disk archive. 

Syntax: ```tar Options [pathname ...]```

Options:

```bash
-c, --create # Create a new archive
-t, --list # List the contents of an archive
-r, --append # Append files to the end of an archive  
-x, --extract, --get # Extract files from an archive

-f, --file ARCHIVE # Use archive file or device ARCHIVE
-v, --verbose # Verbosely list files processed

-j, --bzip2 # Process bzip2 file
z, --gzip, --gunzip --ungzip # Process gz file
```

Examples:

```bash
# Create an archive file "temp.tar.gz" from directory "/home/user/temp"
tar -cvzf temp.tar.gz /home/user/temp/ 

# Create an archive file files.tar.gz from files file1 and file2
tar -cvzf files.tar.gz file1 file2

# Extract files from the file "temp.tar.gz"
tar -xvzf temp.tar.gz

# Extract a bzip2 file
tar -xvjf temp.tar.bz2
```


### find
Search for files in a directory hierarchy

Synax: ```find [-H] [-L] [-P] [path...] [expression]```

Options below path:

```bash
-P # Never follow symbolic links. This is the defualt behavious
-L # Follow symbolic links.
-H # Do not follow symbolic links, except while processing the command line argument.
```

Expresion options:

```bash
-maxdepth levels
-mindepth levels
```

Find tests options
```bash
-name pattern # Match the file by name
-iname pattern # Match the file by name, ignore the case
-size [+-]n[cwbkMG] # File used n units of space. + means >, - means <
-type # Match by type. d: directory. f: file
```

Examples:

```bash
#Find Files Using Name and Ignoring Case under /home/temp/
find /home/temp/ -iname "TestFile"

#Dispay files with 040 permission. i.e files with group read only permisison.
find . -perm 040 -type f -exec ls -l {} \;

#Find files bigger than 100M bytes
find / -size +100M

#Find all directories
find / -type d

#Find all the hidden files
find . type f -name ".*"

#Substitute space with underscore in the file name.
find . -type f -iname “*.mp3″ -exec mv “s/ /_/g” {} \;
```


### cut
Print selected parts of lines from each FILE to standard output. Options:

```bash
-d, --delimiter=DELIM # Use DELIM instead of TAB for field delimiter
-f, --fields=LIST # Select only these fields; 
                  # also print any line that contains no delimiter character, 
                  # unless the -s option is specified
-s, --only-delimited # Do not print lines not containing delimiters

# Examples:

cut -f1,3 cat.txt ## Extact the 1st and the 3rd columns
cut -d"," -f1,2 cat.txt ## Extract the 1st and the 3rd fields, fields are separated by ","
```

### join
Join lines of two files on a common field. For each pair of input lines  with identical join fields, write a line to standard output.  The default join field is the first, delimited by whitespace.  When FILE1 or FILE2 (not both) is -, read standard input. Options:

```bash
-a FILENUM # Also print unpairable lines from file FILENUM, 
           # where FILENUM is 1 or 2, corresponding to FILE1 or FILE2
-i, --ignore-case # Ignore differences in case when comparing fields
-1 FIELD # Join on this FIELD of file 1
-2 FIELD # Join on this FIELD of file 2
-j FIELD # Equivalent to '-1 FIELD -2 FIELD'
-t CHAR # Use CHAR as input and output field separator

--check-order 
  # Check that the input is correctly sorted, even if all input lines are pairable

# Example

join file1 file2 # inner join file1 and file2
join -a 1 file1 file2 # left join file1 and file2
join -a 2 file1 file2 # right join file1 and file2
join -1 1 -2 3 file1 file2 
# join file1 and file2 using the 1st field in file1, and the 3rd field in file2
join file1 file2 | join - file3 # join file1, file2, and file3
```

### uniq
Filter adjacent matching lines from INPUT (or standard input), writing to OUTPUT (or standard output). Options:

```bash
# With no options,  matching lines are merged to the first occurrence
-c, --count # Prefix lines by the number of occurrences
-d, --repeated # Only print duplicate lines
-i, --ignore-case # ignore differences in case when comparing
-u, --unique # Only print unique lines

# Examples

cat a b | sort | uniq > c # c is the union of a and b: a | b
cat a b | sort | uniq -b > c # c is the intersection of b: a & b
cat a b b | sort | uniq -u > c # c is the difference of a and b: (a -b)
cat a | sort | uniq -c # create a histogram
```

### Linux control characters


### curl


#### Reference
- Some of them came from [here](http://www.commandlinefu.com/commands/browse/sort-by-votes)
