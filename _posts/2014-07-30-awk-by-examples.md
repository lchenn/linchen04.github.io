---
layout: post
title: "awk by examples"
categories:
tags: "Linux"
---

### Built-in variables

- NR: Number of Rows
- NF: Number of Fields, $(NF - 1): the second to the last field
- ORS: Output Record Separator


### Examples

#### Concatenate every two lines
{% highlight awk %}

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
{% endhighlight  %}

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

