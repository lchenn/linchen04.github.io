---
layout: post
title: "Curl By Examples"
categories:
tags: "Linux"
---

### Send HTTP post request
Options
```bash
-d, --data ----data-ascii.
```

Send a http post request
```bash
curl -d "name=Rafael%20Sagula&phone=3320780" \
                http://www.where.com/guest.cgi
```

### Emulate filling a form
Options
```bash
-F, --form <name=content>
```

Examples
```bash
# Send a file with other field
curl -F "file=@cooltext.txt" -F "yourname=Daniel" \
     -F "filedescription=Cool text file with cool text inside" \
     http://www.post.com/postit.cgi
# Send multiple files in a single "field" with a single field name
curl -F "pictures=@dog.gif,cat.gif"
# Send two files with two field names:
curl -F "docpicture=@dog.gif" -F "catpicture=@cat.gif"
```


### Handling cookies

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
