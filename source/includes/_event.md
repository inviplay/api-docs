# Event

An event is the main object in the Inviplay ecosystem. It holds al the characteristics of an event, but not the start date and end date. These are stored sepperately in a `dates` table. This way an event can have multiple dates to make it possible to create recurring dates that belong to the same event.

## Get all upcoming events

```shell
curl 'https://api.inviplay.nl/event/upcoming?limit=1' \
  -H 'Authorization: Bearer ACCESS_TOKEN'
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 123,
    "name": "Ga je mee klimmen?",
    "description": "Doe een keer vrijblijvend mee in de grootste klimhal van Arnhem",
    "cost": "5.00",
    "dates": [
      {
        "startDateTime": "2021-07-16T08:00:00+00:00",
        "endDateTime": "2021-07-16T10:00:00+00:00",
        "numberOfParticipants": 3,
        "id": 456
      }
    ],
    "targetGroup": [],
    "maximumParticipants": 4,
    "imageUrl": "/api/attachments/inviplay-219209.appspot.com/download/4a3f86b1-9b6f-40d9-9ec0-48e388f19a43",
    "location": {
      "id": 12,
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

## Get all upcoming events with every date as single object

```shell
curl 'https://api.inviplay.nl/event/upcoming_by_date' \
  -H 'Authorization: Bearer ACCESS_TOKEN'
```

> The above command returns JSON structured like this:

```json
[
  {
    "dateId": 3001,
    "numberOfParticipants": 3,
    "startDateTime": "2022-05-21T20:00:00+00:00",
    "endDateTime": "2022-05-21T21:00:00+00:00",
    "eventId": 600,
    "cost": 500,
    "name": "Potje voetballen?",
    "description": "Doe je mee met een potje voetbal in de stad?",
    "maximumParticipants": 4,
    "location": {
        "id": 1,
        "name": "Kooi in de stad",
        "address": "Oudegracht 143",
        "postalCode": "3511 AJ",
        "city": "Utrecht",
        "coordinates": {
            "lng": 5.117693,
            "lat": 52.0913
        }
    },
    "activity": {
        "id": 1,
        "name": "Voetbal"
    },
    "imageUrl": "",
    "targetGroup": [2]
  }
]
```

This endpoint retrieves all upcoming events with every date as single object.

### HTTP Request

`GET https://api.inviplay.nl/event/upcoming_by_date`

### Optional parameters
Parameter | Required | Type
--------- | -------- | ----
limit | optional | `number`
skip | optional | `number`

## Get all upcoming events with every date as single object

```shell
curl 'https://api.inviplay.nl/event/upcoming_by_date' \
  -H 'Authorization: Bearer ACCESS_TOKEN'
```

> The above command returns JSON structured like this:

```json
[
  {
    "dateId": 2776,
    "numberOfParticipants": 0,
    "startDateTime": "2022-02-21T09:18:00+00:00",
    "endDateTime": "2022-02-21T09:19:00+00:00",
    "eventId": 824,
    "cost": 0,
    "name": "Padel recurring",
    "description": "",
    "maximumParticipants": 4,
    "location": {
        "id": 1,
        "name": "23",
        "address": "Oudegracht 143",
        "postalCode": "3511 AJ",
        "city": "Utrecht",
        "coordinates": {
            "lng": 5.117693,
            "lat": 52.0913
        }
    },
    "activity": {
        "id": 1,
        "name": "Voetbal"
    },
    "imageUrl": "",
    "targetGroup": []
  }
]
```

This endpoint retrieves all upcoming events with every date as single object.

### HTTP Request

`GET https://api.inviplay.nl/event/upcoming_by_date`

### Optional parameters
Parameter | Required | Type
--------- | -------- | ----
limit | optional | `number`
skip | optional | `number`

## Get only events in specific city

Get a list of upcoming events only in a specific city.

### HTTP Request

`GET https://api.inviplay.nl/event/upcoming/{city}`

## Get only events of specific sport type

Get a list of upcoming events that has a specific sport type. You can retrieve the list of Id's with the `GET /activity` endpoint.
### HTTP Request

`GET https://api.inviplay.nl/event/upcoming/activity/1`

## Get only events for specific target group

Get a list of upcoming events that are for a specific target group. You can retrieve the list of Id's with the `GET /targetgroup` endpoint.

### HTTP Request

`GET https://api.inviplay.nl/event/upcoming/target_group/2`

## Add new event

```shell
curl -X POST 'https://api.inviplay.nl/event' \
  -H 'Authorization: Bearer ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  --data-raw '{
    "userId" 123,
    "name": "Ga je mee klimmen?",
    "description": "Doe een keer vrijblijvend mee in de grootste klimhal van Arnhem",
    "activityId": 39,
    "locationId": 12,
    "start": "2021-07-16T08:00:00+00:00",
    "end": "2021-07-16T10:00:00+00:00",
    "maximumParticipants": 4,
    "cost": 500
  }'
```
> The above request returns the created event id:

```json
{
  "eventId": 123,
}
```

Add a new event to the Inviplay database. Some remarks:

- You need to provide an id of a location. This can only be a location that is created by the user who is creating the event.
- You need to provide an id of an activity (sports type).
- You can provide a list of target group id's.
- You can make a recurring event by specifing the `recurring` option. The API will create dates between the start date and end date looking at the value you provided in the `recurring` option. If you leave `recurring` empty, it will create one date with the provided start date and end date.

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
`start` | **required** | `Date` | - | The start date as local date
`end` | **required** | `Date` | - | The end date as local date
`maximumParticipants` | **required** | `Number` | `null` |
`recurring` | optional | `String` | `None` | Possible values: `None`,`SevenDays`, `FourteenDays`, `OneMonth`, `SixMonth`,`OneYear`. 
`targetGroup` | optional | `Number[]` | `null` | Array of targetGroup Id's
`cost` | optional | int | `null` | The costs are handled in cents

## Get event details

```shell
curl 'https://api.inviplay.nl/event/123' \
  -H 'Authorization: Bearer ACCESS_TOKEN'
```

> The above request returns the following JSON:

```json
{
  "id": 123,
  "name": "Ga je mee klimmen?",
  "description": "Doe een keer vrijblijvend mee in de grootste klimhal van Arnhem",
  "cost": "5.00",
  "dates": [
    {
      "startDateTime": "2021-07-16T08:00:00+00:00",
      "endDateTime": "2021-07-16T10:00:00+00:00",
      "numberOfParticipants": 1,
      "id": 456
    }
  ],
  "targetGroup": [],
  "maximumParticipants": 4,
  "imageUrl": "/api/attachments/inviplay-219209.appspot.com/download/4a3f86b1-9b6f-40d9-9ec0-48e388f19a43",
  "location": {
    "id": 12,
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
    "id": 39
  }
}
```

Get the details and dates of a specific event.
### HTTP Request

`GET https://api.inviplay.nl/event/{{eventId}}`

## Update event
```shell
curl -X PUT 'http://api.inviplay.nl/event/123' \
  -H 'Authorization: Bearer ACCESS_TOKEN'
  -H 'Content-Type: application/json' \
  --data-raw '{
  "name": "We gaan toch bowlen"
}'
```

> This returns the updated event

```json
{
  "id": 123,
  "name": "We gaan toch bowlen",
  "description": "Doe een keer vrijblijvend mee in de grootste klimhal van Arnhem",
  "cost": "5.00",
  "dates": [
    {
      "startDateTime": "2021-07-16T08:00:00+00:00",
      "endDateTime": "2021-07-16T10:00:00+00:00",
      "numberOfParticipants": 1,
      "id": 456
    }
  ],
  "targetGroup": [],
  "maximumParticipants": 4,
  "imageUrl": "/api/attachments/inviplay-219209.appspot.com/download/4a3f86b1-9b6f-40d9-9ec0-48e388f19a43",
  "location": {
    "id": 12,
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
    "id": 39
  }
}
```
This request returns the updated event. 
### HTTP Request

`PUT http://api.inviplay.nl/event/{{eventId}}`

## Subscribe or unsubscribe a user to an event


```shell
curl -X PUT 'https://api.inviplay.nl/event/{{eventId}}/attendance' \
  -H 'Authorization: Bearer ACCESS_TOKEN'
  -H 'Content-Type: application/json' \
  --data-raw '{
    "userId": "5243a717-7084-4c82-9ea4-7f8f08d63327",
    "dates": [
      {
        "id": 456,
        "attendance": true
      },
      {
        "id": 567,
        "attendance": false
      }
    ],
    "confirmationUrl": "https://yourwebsite.com/thanks"
  }'
```

> Returns success if request is successful

```json
{
  "status": "success",
  "message": "participant successfully signed up to date 456 and signed out of date 567 of event 123",
  "redirectUrl": null
}
```

> If there is a payment needed then a payment url and payment ID will be provided

```json
{
  "status": "pending",
  "message": "payment needed, follow redirect url to complete request",
  "redirectUrl": "https://mollie.com/payment_link/tr_123ae3f",
  "paymentId": 101
}
```

Endpoint to sign up or signout a user to one or more dates of one event
### HTTP Request

`PUT https://api.inviplay.nl/event/{{eventId}}/attendance`

### Request body
Parameter | Required | Type | Default | Description
--------- | -------- | ---- | ------- | -----------
`userId` | **required** | `String` | - |
`dates` | **required** | `Array` | - | Array of object per date that needs to be updated: `{ id: [Number], attendance: true / false }`
`confirmationUrl` | **required** | `String` | - | Url where the user needs to land after a successful payment is made
