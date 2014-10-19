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
```
command > a.log 2>&1 &
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

### tar



### join

### cut

### curl


### uniq



#### Reference
- Some of them came from [here](http://www.commandlinefu.com/commands/browse/sort-by-votes)