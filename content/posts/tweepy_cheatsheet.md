+++
categories = ["tweepy", "python"]
date = "2021-04-04"
description = "Tweepy twitter library cheatsheet"
title = "Tweepy Cheatsheet"
+++

I am assuming at this point you have a Twitter developer account and already completed basic Tweepy tutorial where you've access to api object to access Twitter api. If not here is the code

**Note: Please run authenticate function before performing any task**

## Login and get api object
File: credentials.json
```json
{
  "consumer_key": "",
  "consumer_secret": "",
  "access_token": "",
  "access_token_secret": ""
}
```

```python
def authenticate():
    # Create Global variable to access Twitter API.
    global api

    # Read credentials.json
    credentials = json.loads(open('credentials.json').read())

    # Set API related variables
    consumer_key = credentials['consumer_key']
    consumer_secret = credentials['consumer_secret']
    access_token = credentials['access_token']
    access_token_secret = credentials['access_token_secret']

    # Create tweepy auth variable
    auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
    auth.set_access_token(access_token, access_token_secret)

    # authorize
    api = tweepy.API(auth)

    return
```

## Post a text Tweet
```python
api.update_status('Hello Tweepy')
```

## Post a Tweet with media
```python
# Deprecated method
api.update_with_media('filename.jpg', 'Tweet message')

# Standard method, can upload upto 4 images
image = api.media_upload('filename.jpg')
image_2 = api.media_upload('filename_2.jpg')

# A list of media ids
media_ids = [image.media_id, image_2.media_id]

api.update_status('Tweet content', media_ids = media_ids )
```
