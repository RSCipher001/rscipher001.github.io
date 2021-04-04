+++
categories = ["puppeteer", "node", "chrome"]
date = "2021-04-04"
description = "In this post we will see that how can you use Chrome with puppeteer"
title = "Use Google Chrome With Puppeteer"
+++

Puppeteer is headless Chrome Node API, in short it is an API which allows you to control a headless chromium browser which can be used for anything from testing to scraping websites data, every puppeteer release uses a specific version of chromium which is downloaded when you install puppeteer but in today we will use our existing Google Chrome instead downloading a separate headless chromium browser which is 100+ MB in size.

## Why puppeteer?

There are many tools available to parse JavaScript and web pages like using scrapy, etc but none of those tools are as powerful as using a real browser because a browser executes JavaScript which is not possible with other tools that parses JavaScript, parsing JavaScript is not as powerful as executing it, puppeteer has few extra features like ability to take website screenshots, save webpages to PDF, etc.

## Installtion

Puppeteer Installation is very easy, it just takes one command `npm i puppeteer` in your NodeJS project but when we use this method it will download a headless version of chromium and if we have Google Chrome installed than we can simply try Chrome instead chromium by telling puppeteer about it. Using Chrome instead chromium may be buggy in some cases but who cares. By the way we are going to use NodeJS environment variables to skip chromium download. If you want to know more about NodeJS environment variable (technically npm environment) variables [click here](https://docs.npmjs.com/cli/config)

## Steps

**NOTE: Use lowercase name of every environment variable otherwise it won't work in most cases (In fact it won't work at all and start downloading chromium, I hate that and you would too).**

If not exists create a file named `.npmrc` in your `$HOME` folder or in `/etc`(Bad idea) and add this line
```bash
puppeteer_skip_chromium_download=true
```

or just type `npm config set puppeteer_skip_chromium_download true` in your terminal before installing npm packages (This is my favorite method). By the way you can see all npm environment variables using `npm config ls -l`. Lines starting with `;` are comments.

Now create a new NodeJS project in an empty folder using `npm init` and answer configuration questions. After successful project creation type `npm i puppeteer` and it will install puppeteer without downloading chromium.

Now we need to tell puppeteer to use chrome, let's see how to do that in *Testing* section

## Testing

For tesing and demonstration purpose let's take a screen shot of this(https://rscipher001.github.io) website. To do that create a new file `index.js` in your NodeJS project and add these lines.

```js
const puppeteer = require('puppeteer');

(async () => {
  const browser = await puppeteer.launch({
  	executablePath: '/usr/bin/google-chrome'
  	});
  const page = await browser.newPage();
  await page.goto('https://rscipher001.github.io');
  await page.screenshot({path: 'rscipher001-blog.png'});

  await browser.close();
})();
```

On line 5 you can see `/usr/bin/google-chrome` replace it with your chrome location, you can use `which google-chrome` to find it in Linux. In Windows you can find it somewhere in `C:/Program Files/Google/`.

## References & Related Links
- [Puppeteer Docs](https://github.com/GoogleChrome/puppeteer/blob/v1.9.0/docs/api.md#environment-variables) <br>
- [Puppeteer on GitHub](https://github.com/googlechrome/puppeteer)
