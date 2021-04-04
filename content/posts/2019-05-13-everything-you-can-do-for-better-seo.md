+++
categories = ["SEO"]
date = "2021-04-04"
description = "A comprehensive list of all the available tweaks and options to improve your website ranking in search results."
title = "Everything you can do for a better SEO"
+++

# Everything You Can Do For Better SEO

SEO is more than keyword research and meta tags, it is an entire world in itself, After investing months in this field I have compiled a list of everything I found about SEO, let's take a look at all available options to measure your website ranking and how to improve it.

## Test SEO Score

Testing website SEO is easy, we have many options, you can use any available but I will suggest you to use Lighthouse, let's explore all available options 

### Test with PageSpeed Insights

Go to https://developers.google.com/speed/pagespeed/insights and enter your website URL, it will scan your website and print score for mobile and desktop, It's UI is really simple and easy to understand

![PageSpeed Insight Screenshot](/assets/images/in-post/everything-you-can-do-for-a-better-seo/pagespeed-insights.webp)

### Test with Google Chrome

**Note:** Disable all Chrome extensions to get neutral result.

Google Chrome comes with an audit tab in developer options, Open website in Chrome and launch developer options, now click on audit button and it will run same test as PageSpeed Insight and print result

![Chrome DevTools Screenshot](/assets/images/in-post/everything-you-can-do-for-a-better-seo/chrome-devtools.webp)

### Test with Lighthouse

Lighthouse is my favorite tool for testing website, It is a complete package with a lot of options, it also gives you more accurate results than anything else.

**Installation:** Run `sudo npm install -g lighthouse` to install it.
**Testing:** Run `lighthouse https://infosecravindra.github.io --view` to run a test on https://infosecravindra.github.io and launch report when finished, If you're planning a future in SEO and digital marketing then you must learn everything about Lighthouse.

![Lighthouse Screenshot](/assets/images/in-post/everything-you-can-do-for-a-better-seo/chrome-devtools.webp)

- Structure Data Testing: https://search.google.com/structured-data/testing-tool/
- Test Mobile Friendliness: https://search.google.com/test/mobile-friendly
- Think with Google Test: https://testmysite.thinkwithgoogle.com/


### Solutions
- Try using webp format fore images

## Improve SEO Score

Improving website SEO is a time consuming process, let's explore all the available options

### Optimize Images

I prefer using WEBP format images over JPEG/PNG because 400 KB PNG can be easily compressed in 20 KB WEBP image, smaller size images means faster loading and better SEO, If you don't want to use WEBP then you should properly resize and optimize all images, I am using a Ubuntu system

#### Optimizing JPEG

JPEG is the most used image format ever so optimizing JPEG is really important, I use a program named `jpegoptim` to do that, you can also use `imagemagick` or anything else if you want, To optimize all images in current folder run the following command

```bash
sudo apt install jpegoptim			# Installation

for i in *.jp*g 					# Select all jpg/jpeg
do
	jpegoptim -s $i;				# WARNING: It will remove ICC profiles
done
```

To convert jpg/png images to webp, install webp converter, for Ubuntu type
```bash
sudo apt install webp
```

To convert all the jpg images in current folder use

```bash
for i in *.jpg                                                                           
do
cwebp $i -o "${i%.jpg}.webp"
done
```
then replace all the references in html.

- Optimize all jpeg/jpg images

```bash
sudo apt install jpegoptim			# Translate according to your system

for i in *.jp*g 					# Be careful about wild card
do
	jpegoptim -s $i;				# WARNING: It will remove ICC profiles
done
```

- Avoid PNG if possible
- Optimize PNG images

```bash
sudo apt install optipng			# Translate according to your system

for i in *.png
do
	optipng -o7 $i;					# Be carefull it is 100 times slower than jpeg compression
done
```

- If Server == Apache ? Use modspeed plug-in : do nothing
- Use compression when supported by browser.
- Use proper meta description
- Use slugs instead id.
- Use right keyword in images.
- Use Google Keyword planner.
- Use defer/async tag in scripts.
- Avoid redundancy in content.
- Use rich snippet.
- Use DNS prefetching and pre connecting.
- Set priority if number of images is large. [Hint: Search priority tag on Search engine]
- Use caching (Service worker) [WARNING: Service workers may be confusing, always hire experienced people or you would end up breaking site for majority of people]
- If possible reduce JS & CSS by compiling only essentials portions from framework code,
- Make sure NPM scripts are using production environments.
- Use CDN for serving vendor libraries.
- Thumbnails should be thumbnails size images not large and heavy images.
- Create Google business account.
- Use localization for international content.
- Ask people to write reviews on Google.
- Avoid fake back-linking.
- Avoid spelling mistakes.
- Do not overkill with black SEO (To avoid blacklisting).
- Keep your website upto date
- Make sure your website is accessible to everyone .
- Should be responsive (Use `bootstrap`, `bulma`, `semantic-ui`, media tags, whatever).
- Use sitemap if possible.
- Use HTTPS.
- Add Jump to section by utilizing ids