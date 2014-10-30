---
layout: post
title: "Curl By Examples"
categories:
tags: "Linux"
---



### Send HTTP post request
Options:

```bash
# Use application/x-www-form-urlencoded mime-type to send the request
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
Options:

```bash
-F, --form <name=content>
```

***-F*** use ***multipart/form-data*** mime type to send post request.



Examples:

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
Options:

```bash
# Setup the cookie, multiple cookies are in the format of "NAME1=VALUE1; NAME2=VALUE2"
-b, --cookie <name=data>
# Specify which file to write cookies after a completed http request
-c, --cookie-jar <file name>
```

Examples:

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

### Upload files
Options:

```bash
-T
```

Examples of uploading to FTP/FTPS/SFTP/SCP:

```bash
# Upload all data on stdin to a specified server:
$ curl -T - ftp://ftp.upload.com/myfile
#Upload data from a specified file, login with user and password:
$ curl -T uploadfile -u user:passwd ftp://ftp.upload.com/myfile
# Upload a local file to the remote site, and use the local file name at the remote site too:
$ curl -T uploadfile -u user:passwd ftp://ftp.upload.com/
# Upload a local file to get appended to the remote file:
curl -T localfile -a ftp://ftp.upload.com/remotefile
```

Example of uploading to HTTP put.

```bash
# Upload all data on stdin to a specified HTTP site which can accept put request
$ curl -T - http://www.upload.com/myfile
```

#### Reference
[Curl manual](http://curl.haxx.se/docs/manual.html)