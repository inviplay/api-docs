---
title: Inviplay API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:

includes:
  - user
  - event
  - activity
  - location
  - targetgroup

search: true

code_clipboard: true
---

# Introduction

Welcome to the Inviplay API Reference! You can use our API to access Inviplay API endpoints, which can get upcoming events in the Inviplay network, add new users and new events.

# Authentication

## Get token
> First, get an access token:

```shell
curl POST 'https://authentication.inviplay.nl/connect/token' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=CLIENT_ID' \
--data-urlencode 'client_secret=CLIENT_SECRET'
```

> This returns the following JSON:

```json
{
  "access_token": "ACCESS_TOKEN",
  "expires_in": 3600,
  "token_type": "Bearer",
  "scope": "CreateEvent RegisterUser"
}
```

> To authorize every api request, use the above ACCESS_TOKEN:

```shell
curl 'api_endpoint_here' \
  -H 'Authorization: Bearer ACCESS_TOKEN'
```

> Make sure to replace `ACCESS_TOKEN` with the token that you will get from the /token endpoint.

Inviplay uses an access token to allow access to the API. To request a token you need a client_id and a client_secret and use that in the following request:

### HTTP Request

`POST https://authentication.inviplay.nl/connect/token`

### Body

Key | Value
--- | -----
grant_type | client_credentials
client_id | CLIENT_ID
client_secret | CLIENT_SECRET

<aside class="notice">
Use x-www-form-urlendcoded as body type and replace CLIENT_ID and CLIENT_SECRET with your own client_id and client_secret
</aside>
