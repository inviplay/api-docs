# Activity

An activity is the sport type in the Inviplay database. This is a list of around 50 sport types and new sports will be added now and then.
## Get list of sport types

```shell
curl 'https://api.inviplay.nl/activity' \
  -H 'Authorization: Bearer ACCESS_TOKEN' \
```

> Returns a list of activities

```json
[
  {
    "id": 1,
    "name": "Voetbal",
    "defaultImageUrl": "/api/attachments/inviplay-219209.appspot.com/download/afad6ead-ef44-4297-943b-317c0648d059.jpg"
  },
  {
    "id": 2,
    "name": "Badminton",
    "defaultImageUrl": "/api/attachments/inviplay-219209.appspot.com/download/2cacbb5d-bf02-4cd6-8bf8-1df6fd924179.jpg"
  },
  {
    "id": 3,
    "name": "Tafeltennis",
    "defaultImageUrl": "/api/attachments/inviplay-219209.appspot.com/download/1860bea4-43fd-4270-ab03-2eb4efb3d633.jpg"
  },
]
```

Endpoint to get a list of possible sport types

### HTTP Request

`POST https://api.inviplay.nl/activity`
