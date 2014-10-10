---
layout: post
title: "Awk By Examples"
categories:
tags: "Linux"
---

### Built-in variables


| Variable | Description   |
|----------|---------------|
| $0	| Current Line |
| $1~$n | The nth field, separated by FS |
| FS    | Field separator, the default is white space or tab |
| OFS   | Output field separator, the default is white space |
| NF    | Number of fields in current line |
| NR    | Number of rows read out, starting with 1, accumulated if there are multiple files |
| FNR   | Number of rows per file |
| RS    | Input record separator, the default is line break |
| ORS   | Output Record Separator |
| FILENAME | Current file's name |



### Examples

#### Concatenate every two lines


```awk
BEGIN{ORS=""} 
{
    if (NF > 0) {
        print $0; 
        if (NR%2 == 1) {
            print "\t"
        } else {
            print "\n"
        }
    }
}
```

- Input

	    1
	    2
	    3
	    4
	    5
	    6


- Output


	    1	2
	    3	4
	    5	6

#### Extract lines between two patterns
Purpose: there are two patterns, extract the lines between these two pattern
- Code:

```awk
awk '/pattern1/ {p=1}; p; /patten2/ {p=0}' log
```

- Explaination:
  + ```p``` serves as the condidtion for the default action (print $0).
  + When ```pattern1``` is matched, p is 1; then the default action will be executed.
  + When ```pattern2``` is matched, p is 0, it means a group has ended.

#### Break a file by a field

```awk
awk 'NR!=1{print > $6}' netstat.txt
```

#### Pass variable into awk script from shell
```awk
awk -v val=$x '{print $1, $2, $3, $4+val, $5+ENVIRON["y"]}' OFS="\t" score.txt
```

#### Specify Input Field Separator
```
awk -F: '{print $2}'
awk 'BEGIN{FS=":"} {print $2}'
```


### Randomly sample lines
```awk
awk 'BEGIN {srand()} !/^$/ { if (rand() <= .10) print $0}'
```

### Match a certain field and print
```awk
awk '$6 ~ /FIN/ || NR==1 {print NR,$4,$5,$6}' OFS="\t" netstat.txt
```
