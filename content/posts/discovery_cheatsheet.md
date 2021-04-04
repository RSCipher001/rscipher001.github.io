+++
categories = ["infosec", "discovery"]
date = "2021-04-04"
description = "Recon cheatsheet to discovert new hosts, endpoint, etc"
title = "Recon cheatsheet"
+++

## Finding Subdomains

### Using Sublist3r
```bash
sublister -d example.com -o example
```

- `example.com` is target domain
- `example` is output filename

### Using Virus Total API
```bash
curl -s 'https://www.virustotal.com/ui/domains/example.com/subdomains?limit=40' | jq .data[].id
```

### Using cert.sh

```bash
curl "https://crt.sh?q=%.example.com&output=json" -sS | jq .name_value | uniq | tee output
```


```bash
DOMAIN=example.com
curl -s "https://crt.sh/?q=%.$DOMAIN&output=json" | grep -oE \"[a-zA-Z0-9.]+$DOMAIN\" | sed s/\"//g | sort -u
```

## Fuzzing

**NOTE:** Edit ~/.wfuzz/wfuzz.ini to overwrite default user agent.

```
user-agent = Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36
```

```bash
wfuzz -c --filter "c=200" -t 50 -w ~/Projects/GitHub/dictionaries/starter.txt https://www.target-domain.com/FUZZ
```
- `--filter "c=200":` Filter non 200 result
- `-c:` Color output
- `-t :` Number of threads
- `-w:` Wordlist
- `-H:` Header
- `-X HEAD:` For head requests


## Javascript retrieve all a links from a page using console.
```js
var x = document.links;
for(var i = 0; i < x.length; i++){
  console.log(x[i].href);
}

/*
function copyToClipboard(text){
    var dummy = document.createElement("input");
    document.body.appendChild(dummy);
    dummy.setAttribute('value', x);
    dummy.select();
    document.execCommand("copy");
    document.body.removeChild(dummy);
}
copyToClipboard('Hello, World!')
*/
```

## Cleaning result in bash

Manual copy for now



```bash
cat haha | sort | uniq > url 
cat url | cut -d'/' -f3 | sort | uniq > Processed_URLs.txt
```

### Retrieve name colums from cities json array of objects
```json
[
    {
        "id": "1",
        "name": "Mumbai",
        "state": "Maharashtra"
    },
    {
        "id": "2",
        "name": "Delhi",
        "state": "Delhi"
    },
]
```


```jq
cat cities.json |  jq '.[] | .name' > Cities.txt
```