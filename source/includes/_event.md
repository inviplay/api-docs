# Event

## Get all upcoming events

```shell
curl 'https://api.inviplay.nl/event/upcoming?city=arnhem&limit=1' \
  -H 'Authorization: Bearer ACCESS_TOKEN'
```

> The above command returns JSON structured like this:

```json
[
  {
    "eventId": 123,
    "name": "Ga je mee klimmen?",
    "description": "Doe een keer vrijblijvend mee in de grootste klimhal van Arnhem",
    "dates": [
      {
        "startDateTime": "2021-07-16T08:00:00+00:00",
        "endDateTime": "2021-07-16T10:00:00+00:00",
        "numberOfParticipants": 3,
        "dateId": 456
      }
    ],
    "targetGroup": [],
    "maximumParticipants": 4,
    "imageUrl": "/api/attachments/inviplay-219209.appspot.com/download/4a3f86b1-9b6f-40d9-9ec0-48e388f19a43",
    "location": {
      "locationId": 12,
      "name": "Klimhal Mountain Network Arnhem",
      "adress": "Olympus 27",
      "postalCode": "6832 EL",
      "city": "Arnhem",
      "coordinates": {
        "lng": 4.692161717541481,
        "lat": 52.67758735617635
      }
    },
    "activity": {
      "name": "Klimmen",
      "activityId": 39
    }
  }
]
```

This endpoint retrieves all upcoming events.

### HTTP Request

`GET https://api.inviplay.nl/event/upcoming`

### Optional parameters
Parameter | Required | Type
--------- | -------- | ----
limit | optional | `number`
skip | optional | `number`
city | optional | `string`
targetGroup | optional | `number`

## Add new event


```shell
curl -X POST 'https://api.inviplay.nl/event' \
  -H 'Authorization: Bearer ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  --data-raw '{
    "name": "Ga je mee klimmen?",
    "description": "Doe een keer vrijblijvend mee in de grootste klimhal van Arnhem",
    "activityId": 39,
    "locationId": 12,
    "start": "2021-07-16T08:00:00+00:00",
    "end": "2021-07-16T10:00:00+00:00",
    "maximumParticipants": 4
  }'
```
> The above request returns the created event id:

```json
{
  "eventId": 123,
}
```

Add a new event to the Inviplay database. You need to provide an userId 

### HTTP Request

`POST https://api.inviplay.nl/event`

### Request body
Parameter | Required | Type | Default | Description
--------- | -------- | ---- | ------- | -----------
`userId` | **required** | `String` | - | User Id of the organizer of the event
`name` | **required** | `String` | - | Name of the event
`description` | **required** | `String` | - | Description of the event
`activityId` | **required** | `Number` | - | Id of activity
`locationId` | **required** | `Number` | - | Id of location
`start` | **required** | `Date` | - |
`end` | **required** | `Date` | - |
`maximumParticipants` | **required** | `Number` | `null` |
`recurring` | optional | `String` | `null` | Possible values: `sevenDays`, `fourteenDays`, `oneMonth`, `sixMonths`, `oneYear`
`targetGroup` | optional | `Number[]` | `null` | Array of targetGroup Id's

## Get event details

```shell
curl 'https://api.inviplay.nl/event/123' \
  -H 'Authorization: Bearer ACCESS_TOKEN'
```

> The above request returns the following JSON:

```json
{
  "eventId": 123,
  "name": "Ga je mee klimmen?",
  "description": "Doe een keer vrijblijvend mee in de grootste klimhal van Arnhem",
  "dates": [
    {
      "startDateTime": "2021-07-16T08:00:00+00:00",
      "endDateTime": "2021-07-16T10:00:00+00:00",
      "numberOfParticipants": 1,
      "dateId": 456
    }
  ],
  "targetGroup": [],
  "maximumParticipants": 4,
  "imageUrl": "/api/attachments/inviplay-219209.appspot.com/download/4a3f86b1-9b6f-40d9-9ec0-48e388f19a43",
  "location": {
    "locationId": 12,
    "name": "Klimhal Mountain Network Arnhem",
    "adress": "Olympus 27",
    "postalCode": "6832 EL",
    "city": "Arnhem",
    "coordinates": {
      "lng": 4.692161717541481,
      "lat": 52.67758735617635
    }
  },
  "activity": {
    "name": "Klimmen",
    "activityId": 39
  }
}
```

Get the details and dates of a specific event.
### HTTP Request

`GET https://api.inviplay.nl/event/{{eventId}}`

## Add an user to a date of an event


```shell
curl -X POST 'https://api.inviplay.nl/event/123/date/456/addUser/5243a717-7084-4c82-9ea4-7f8f08d63327' \
  -H 'Authorization: Bearer ACCESS_TOKEN'
```

> Returns success if request is successful

```json
{
  "status": "success"
}
```

Endpoint to add an user to a date of an event
### HTTP Request

`POST https://api.inviplay.nl/event/{{eventId}}/date/{{dateId}}/addUser/{{userId}}`

## Remove an user of a date of an event

```shell
curl -X POST 'https://api.inviplay.nl/event/123/date/456/removeUser/5243a717-7084-4c82-9ea4-7f8f08d63327' \
  -H 'Authorization: Bearer ACCESS_TOKEN'
```

> Returns success if request is successful

```json
{
  "status": "success"
}
```

Endpoint to remove a user of a date of an event
### HTTP Request

`POST https://api.inviplay.nl/event/{{eventId}}/date/{{dateId}}/removeUser/{{userId}}`

