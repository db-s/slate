---
title: xDForce API Reference

language_tabs:
  - shell
  - ruby
  - python

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the xDForce API! You can use our API to access xDForce API endpoints, which can get information on your monitors which are being tracked for analytics in our database.

We have language bindings in Shell, Ruby, and Python! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace `meowmeowmeow` with your personal API key.
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

`POST /api2/signup`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
email | | User email address which will also be used as the username
firstName | | User's first name
lastName | | User's last name
phone | | User's phone number
password | | User's login password

<aside class="success">
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

`POST /api2/login`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
username | | User email address which was used in signup
password | | User's login password

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

`DELETE /api2/logout`
