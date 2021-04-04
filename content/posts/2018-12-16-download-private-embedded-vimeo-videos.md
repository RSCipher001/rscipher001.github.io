+++
categories = ["vimeo", "youtube_dl"]
date = "2021-04-04"
description = "Downloading private embedded vimeo videos with the help of youtube-dl"
title = "How To Download Private Embedded Vimeo Videos"
+++

**NOTE:** Content in this post is available for **educational purpose** and shouldn't be used for any illegal/unauthorized activity.

## Steps

- Download `youtube-dl`
- Find Vimeo video id
- Start download

## Downloading youtube-dl

I assume you've Python installed in your system. If not then I install Python and go for version 3 then install `youtube-dl` using `pip`

```bash
pip install youtube-dl
```

In Many Linux system you may have to type the following command to use Python 3.
```bash
sudo pip3 install youtube-dl
```

## Finding Video ID

It can be tough. Look at the souce code of the page where video is embeded and you will find vimeo video id.

## Downloading

Assuming video was embedded on the following URL
```
https://example.com/here-is-a-private-vimeo-video/
```

and video id is `1234531`.

Now open your Terminal and type
```bash
youtube-dl -v "https://player.vimeo.com/video/1234531" --referer "https://example.com/here-is-a-private-vimeo-video/"
```
replace `1234531` in `https://player.vimeo.com/video/1234531` with your video id.

If you see any error after download don't forget to install `ffmpeg`. In Ubuntu you can type the following command to do that.

```bash
sudo apt install ffmpeg
```

If you still see an error then you may be using an old version of `youtube-dl`, update is using

```bash
sudo pip3 install --upgrade youtube_dl
```