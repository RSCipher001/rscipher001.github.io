---
title: "Facebook Graph API Cheatsheet"
date: 2019-12-23T03:20:00+05:30
description: "Getting data with Facebook Graph API"
tags: [facebook, graph-api]
category: [Facebook, Graph API]
---

## Steps
- Get app client id
- Get app client credentials
- Get app access token
- Get user authorization code
- Get user access token


## Set variables
```bash
CLIENT_ID=XXXXXXXXXXXXXXXX
CLIENT_SECRET=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
CALLBACK_URL="http://localhost/oauth/facebook/callback"
```

## Get App Access Token
Request
```bash
curl "https://graph.facebook.com/oauth/access_token?client_id=$CLIENT_ID&client_secret=$CLIENT_SECRET&grant_type=client_credentials"
```

Response
```json
{
	"access_token":"XXXXXXXXXXXXXXXX|XXXXXXXXXXXXXXXXX-XXXXXXXXX",
	"token_type":"bearer"
}
```

```bash
APP_ACCESS_TOKEN='XXXXXXXXXXXXXXXX|XXXXXXXXXXXXXXXXX-XXXXXXXXX'
```

## Get User Authorization Code
```bash
firefox https://www.facebook.com/v5.0/dialog/oauth?client_id=$CLIENT_ID&scope=user_likes,user_photos,user_videos,user_posts,email&redirect_uri=$CALLBACK_URL&state=csrf_string
```

Response
```
http://localhost/oauth/facebook/callback?code=AQDY9Yddp5o4aAnzSS2bHMvW6RN_XXXXXXXXX_59wixKl8fshCdw-fn5zYrtlpt6piK-ahfHBmO9CtXVZxHKyPqFyY3wBq5mCSZrTIufPHEp-lqF0neWmc5mT2FIwwbHJmwHm3ntiov2SZyN0tVNomx_XozqIhJUKitAnprMoXfCHsljhqXqTSg1Af9PRVh0XSwAZWcILTEE95FCAzIGEWfA9xQp3SfvAzvRkjtROi8nxuGgk-QF9sOA0ZPjuyLEcLQR1YWITJBBrULh5UPf6361KCca1oOcpaId_b5bpxPJnJdJu51EwsPuLXNDrjgLmUtKCkr6nv63ypg3VfLp4inyljNxZJ1syQ_0PmbZay0uVQ&state=csrf_string#_=_
```

```bash
USER_AUTHORIZATION_CODE="AQDY9Yddp5o4aAnzSS2bHMvW6RN_XXXXXXXXX_59wixKl8fshCdw-fn5zYrtlpt6piK-ahfHBmO9CtXVZxHKyPqFyY3wBq5mCSZrTIufPHEp-lqF0neWmc5mT2FIwwbHJmwHm3ntiov2SZyN0tVNomx_XozqIhJUKitAnprMoXfCHsljhqXqTSg1Af9PRVh0XSwAZWcILTEE95FCAzIGEWfA9xQp3SfvAzvRkjtROi8nxuGgk-QF9sOA0ZPjuyLEcLQR1YWITJBBrULh5UPf6361KCca1oOcpaId_b5bpxPJnJdJu51EwsPuLXNDrjgLmUtKCkr6nv63ypg3VfLp4inyljNxZJ1syQ_0PmbZay0uVQ"
```

## Get user access token
Request
```bash
curl https://graph.facebook.com/v5.0/oauth/access_token?client_id=$CLIENT_ID&redirect_uri=$CALLBACK_URL&client_secret=$CLIENT_SECRET&code=$USER_AUTHORIZATION_CODE
```
Response
```json
{
	"access_token":"EAAjDiYWinYEBADLkmsJ6xcbizwcs8V8Q49EcSdzIVZB0WSIr7oJvIbPhW3QOW4ubZBgAmkNVrIV56uPocs4QgYklQp4oexU9dqoZA0r3bcG8ecDAZCtZCdCe0R3HE5b5KTW4PpKTwyVfHJhh2lrA6n3aUid3B5wXXXXXXXXXXXXXXXX",
	"token_type":"bearer",
	"expires_in":5180061
}
```
```bash
USER_ACCESS_TOKEN="EAAjDiYWinYEBADLkmsJ6xcbizwcs8V8Q49EcSdzIVZB0WSIr7oJvIbPhW3QOW4ubZBgAmkNVrIV56uPocs4QgYklQp4oexU9dqoZA0r3bcG8ecDAZCtZCdCe0R3HE5b5KTW4PpKTwyVfHJhh2lrA6n3aUid3B5wXXXXXXXXXXXXXXXX"
```

## Validating access token

Request
```bash
curl https://graph.facebook.com/debug_token?input_token=$USER_ACCESS_TOKEN&access_token=$APP_ACCESS_TOKEN
```

Response
```json
{
	"data": {
		"app_id": "XXXXXXXXXXXXXXXX",
		"type": "USER",
		"application": "OAuth App",
		"data_access_expires_at": 1584872422,
		"expires_at": 1582276519,
		"is_valid": true,
		"issued_at": 1577092519,
		"scopes": [
			"user_likes",
			"user_photos",
			"user_videos",
			"user_posts",
			"email",
			"public_profile"
		],
		"user_id":"XXXXXXXXXXXXXXXX"
	}
}
```

## Get User profile
Request
```bash
USER_PROFILE_FIELDS=id,address,age_range,birthday,first_name,gender,hometown,interested_in,last_name,location,middle_name,name,picture
curl -s https://graph.facebook.com/me?fields=$USER_PROFILE_FIELDS&access_token=$USER_ACCESS_TOKEN | python -m json.tool
```
Response
```json
{
	"id":"XXXXXXXXXXXXXXXX",
	"first_name":"John",
	"last_name":"Doe",
	"name":"John Doe"
}
```

## Get Likes
```bash
curl https://graph.facebook.com/me?fields=likes.summary(true)&access_token=$USER_ACCESS_TOKEN
```

```json
{
    "id": "XXXXXXXXXXXXXXXX",
    "likes": {
        "data": [
            {
                "created_time": "2019-07-24T15:17:55+0000",
                "id": "XXXXXXXXXXXXXXX",
                "name": "Example Page 1"
            },
            {
                "created_time": "2017-05-15T04:59:08+0000",
                "id": "XXXXXXXXXXXXXXX",
                "name": "Example Page 2"
            }
        ],
        "paging": {
            "cursors": {
                "after": "XXXXXXXXXXXXXXXXXXXX",
                "before": "XXXXXXXXXXXXXXXXXXXX"
            }
        },
        "summary": {
            "total_count": XX
        }
    }
}
```

## Get Picture
```bash
curl https://graph.facebook.com/me/picture?access_token=$USER_ACCESS_TOKEN
```

## Get User Photos
```bash
curl https://graph.facebook.com/me?fields=album,images&access_token=$USER_ACCESS_TOKEN
```