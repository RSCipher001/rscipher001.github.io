+++
categories = ["curl"]
date = "2021-04-04"
description = "Curl cheatsheet"
title = "Curl cheatsheet"
+++

### Change system wide user agent

Create `.curlrc` in $HOME directory and add this line
```
user-agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36"
```

to suppress this file use
```bash
curl -q example.com
```

### Include the header response in output
```bash
curl -i
```

### Head request
```bash
curl -I
```

### get request and header in the response
```bash
curl -D
```

### Verbose
```bash
curl -v
```

### Follow redirects
```bash
curl -L
```

### Save cookies to a file
```bash
curl -b cookiesfile <url>
```

**NOTE: cookiesfile is a file in which cookeis are saved**
### User saved cookies
```bash
curl -c cookiesfile <url>
```

### Make POST request
```bash
curl -XPOST <url>
```
**Note: change POST to PUT, PATCH or whatever you need except HEAD, use `-I` for HEAD**

### Make POST request with data
```bash
curl --data "param1=value1&param2=value2" <url>
```

### List Input Field
```bash
curl website | gunzip | sed -n '/<form/,/<\/form/p' | grep '<input'
```

### List Input Field Uncompressed
```bash
curl website | sed -n '/<form/,/<\/form/p' | grep '<input'
```