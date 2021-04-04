---
title: "SEO Cheatsheet"
date: 2019-11-10T23:30:00+05:30
description: "SEO Cheatsheet"
tags: [seo]
category: [SEO]
---

### Test website score.
- Test with **PageSpeed Insights**: https://developers.google.com/speed/pagespeed/insights.
- Structure Data Testing: https://search.google.com/structured-data/testing-tool/
- Test Mobile Friendliness: https://search.google.com/test/mobile-friendly
- Think with Google Test: https://testmysite.thinkwithgoogle.com/
- Test Using Lighthouse: Chrome DevTools > Audits


### Solutions
- Try using webp format fore images

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
