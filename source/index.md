---
title: xDForce API Reference

[comment]: <> (language_tabs:)
[comment]: <> (  - shell)
[comment]: <> (  - ruby)
[comment]: <> (  - python)

[comment]: <> (toc_footers:)
[comment]: <> ( - <a href='#'>Sign Up for a Developer Key</a>)
[comment]: <> ( - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>)

includes:
  - errors

search: true
---

# Introduction

Welcome to the xDForce API! You can use our API to access xDForce API endpoints, which can get information on your monitors which are being tracked for analytics in our database.

We have language bindings in Shell, Ruby, and Python! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: XDFORCE_API_KEY"
```

> Make sure to replace `XDFORCE_API_KEY` with your API key.

xDForce uses API keys to allow access to the API. You can register a new xDForce API key at our [developer portal](http://example.com/developers).

xDForce expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: XDFORCE_API_KEY`

<aside class="notice">
You must replace `XDFORCE_API_KEY` with your personal API key.
</aside>

# Users

## Signup / Create Users

> The above command returns JSON structured like this:

```json
{
    "ok": true,
    "message": "Account created successfully",
    "target": "REDIRECTION URL"
}
```

This endpoint creates a user.

### HTTP Request

`POST /api/v1/signup`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
email | String | User email address which will also be used as the username
firstName | String | User's first name
lastName | String | User's last name
phone | String | User's phone number
password | String | User's login password

<aside class="notice">
By signing up, user will automatically accept the terms and conditions of xDForce and Bizzblizz
</aside>

## Login

> The above command returns JSON structured like this:

```json
{
    "ok": true,
    "message": "Login successful",
    "target": "REDIRECTION_URL"
}
```

Users can login through this endpoint.

### HTTP Request

`POST /api/v1/login`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
username | String | User's email address which was used in sign up
password | String | User's login password

## Logout

> The above command returns JSON structured like this:

```json
{
    "ok": true,
    "message": "You have successfully logged out"
}
```

Users can logout through this endpoint.

### HTTP Request

`DELETE /api/v1/logout`

# Monitors

## Create Monitors (Basic Settings)

Users can create new monitors through this endpoint.

### HTTP Request

`POST /api/v1/monitors/new`

> The above command returns JSON structured like this on SUCCESS:

```json
{
    "ok": true,
    "id": "MONITOR_ID",
    "rev": "DOCUMENT_REVISION_HASH"
}
```

> The above command returns JSON structured like this in case of any ERROR:

```json
{
  "ok": false,
  "message": "ERROR_MESSAGE"
}
```

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
name | String | Name or Address of the website to be monitored
category | String | Category of the Monitor
wantsDesktop | Boolean | Accept desktop traffic as good traffic
wantsPhone | Boolean | Accept mobile traffic as good traffic
wantsTablet | Boolean | Accept tablet/device traffic as good traffic
mismatchRedirectUrl | String | Redirect URL for unwanted impressions
dangerRedirectUrl | String | Redirect URL for dangerous impressions



## Set Monitor Geo Locations

Users Geo Locations to the respective Monitor

`POST /api/v1/monitors/<ID>/setgeographicarea`

> The above command returns JSON structured like this on SUCCESS:

```json
{
    "ok": true,
    "id": "MONITOR_ID",
    "rev": "DOCUMENT_REVISION_HASH"
}
```

> The above command returns JSON structured like this in case of any ERROR:

```json
{
  "ok": false,
  "message": "ERROR_MESSAGE"
}
```

### Query Parameters

Parameter | Type | Options | Default | Description
--------- | ---- | ------- | ------- | -----------
geoStrategy | String | coordinates, regions | coordinates | Set geographic strategy
addresses | Array of String | | | List of addresses (if selected `coordinates`)
country | Array of String | | | List of countries as regions (if selected `regions`)

<aside class="notice">
When selecting coordinates, try to provide an address as specific as possible for a better result. Location of the address consisting latitude and longitude will be updated automatically when updating the monitors geographic location.
</aside>

## List All Monitors

This endpoint will list all the active monitors of a user.

`GET /api/v1/monitors`

> The above command returns JSON structured like this on SUCCESS:


```json
{
  "ok": true,
  "message": {
    "monitors": [
    {
      "_id": "13OG0C57B101",
      "_rev": "60-c96ab2a1547ce4c26c1c11407af8324c",
      "type": "Monitor",
      "accountId": "16VM0C2cuD02",
      "name": "Sample Monitor 1",
      "domain": "",
      "category": "",
      "wantsDesktop": false,
      "wantsPhone": false,
      "wantsTablet": false,
      "geoStrategy": "coordinates",
      "dangerRedirectUrl": "",
      "mismatchRedirectUrl": "",
      "archived": false,
      "blacklist": [],
      "coordinates":
        [
          {
            "address": "Kolkata",
            "latitude": 22.572646,
            "longitude": 88.36389500000001,
            "radius": 25
          },
          {
            "address": "Delhi",
            "latitude": 28.6139391,
            "longitude": 77.2090212,
            "radius": 25
          }
        ]
      },
      {
        "_id": "12zu0CELWG01",
        "_rev": "1-6466ba5e64216c44db51553ff05e8fb7",
        "type": "Monitor",
        "accountId": "16VM0C2cuD02",
        "name": "Sample Monitor 2",
        "domain": "",
        "category": "Blog - Cultural",
        "wantsDesktop": true,
        "wantsPhone": true,
        "wantsTablet": true,
        "geoStrategy": "regions",
        "regions":
          [
            {
              "country": "*",
              "region": "*"
            }
          ],
        "dangerRedirectUrl": "",
        "mismatchRedirectUrl": "",
        "archived": false,
        "coordinates": [],
        "blacklist": []
      }
    ]
  }
}
```

> The above command returns JSON structured like this in case of any ERROR:

```json
{
  "ok": false,
  "message": "ERROR_MESSAGE"
}
```
