# Event

## Get all upcoming events

```shell
curl 'http://api.inviplay.nl/event/upcoming' \
  -H 'Authorization: Bearer ACCESS_TOKEN'
```

> The above command returns JSON structured like this:

```json
[
  {
    "name": "klimmen",
    "description": "",
    "start": "0001-01-01T00:00:00+00:00",
    "end": "0001-01-01T00:00:00+00:00",
    "recurring": "sevenDays",
    "maximumParticipants": 4
  },
  {
    "name": "eindelijk weer partijen",
    "description": "",
    "start": "0001-01-01T00:00:00+00:00",
    "end": "0001-01-01T00:00:00+00:00",
    "recurring": "sevenDays",
    "maximumParticipants": 4
  },
]
```

This endpoint retrieves all upcoming events.

### HTTP Request

`GET http://api.inviplay.nl/event/upcoming`

