---
layout: post
title: "Curl By Examples"
categories:
tags: "Linux"
---



### Send HTTP post request
Options:

```bash
-d, --data ----data-ascii
--data-urlencode
--data-binary
```

Send a http post request

```bash
curl -d "name=Rafael%20Sagula&phone=3320780" http://www.where.com/guest.cgi
```

### Send HTTP get request
When used, this option will make all data specified with -d, --data, --data-binary or --data-urlencode to be used in an HTTP GET request, instead of the POST request that otherwise would be used.

```bash
-G, --get
```

### Emulate filling a form
Options
```bash
-F, --form <name=content>
```

Examples
```bash
# Upload a file
curl -F "web-@index.html" www.example.com
# Upload a file with content type
curl -F "web=@index.html;type=text/html" www.example.com
# Send a file with other field
curl -F "file=@cooltext.txt" -F "yourname=Daniel" \
     -F "filedescription=Cool text file with cool text inside" \
     http://www.post.com/postit.cgi
# Send multiple files in a single "field" with a single field name
curl -F "pictures=@dog.gif,cat.gif" www.example.com
# Send two files with two field names:
curl -F "docpicture=@dog.gif" -F "catpicture=@cat.gif" www.example.com
# Change the uploaded the filename in the post request
curl -F "file=@localfile;filename=nameinpost" www.example.com
#  If filename/path contains ',' or ';', it must be quoted by double-quotes like:
curl -F "file=@\"localfile\";filename=\"nameinpost\"" url.com
```


### Handling cookies
Options

```bash
-b, --cookie <name=data> # Setup the cookie, multiple cookies are in the format of "NAME1=VALUE1; NAME2=VALUE2"
-c, --cookie-jar <file name> # Specify which file to write cookies after a completed http request
```

Examples

```bash
# Send hard coded cookie pairs
curl -b "name=Daniel" www.example.com
# Send cookies stores in a file
curl -b cookies.txt www.examples.com
# Saving the cookie from a http request
curl -c cookies.txt www.example.com
# Save and load cookies from a netscape cookie file
curl -b cookies.txt -c cookies.txt www.example.com
```


### Download files
Options:

```bash
-o, --output <file>
```

Write output to <file> instead of stdout. If you are using {} or [] to fetch multiple documents, you can use '#' followed by a number in the <file> specifier. That variable will be replaced with the current string for the URL being fetched.
Examples:

```bash
# Download one.site.com as file_1.txt, two.site.com as file_2.txt
$ curl http://{one,two}.site.com -o "file_#1.txt"
# Use multiple variables, th
$ curl http://{site,host}.host[1-5].com -o "#1_#2"
```
