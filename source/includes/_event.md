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
    "eventId": 123,
    "name": "Ga je mee klimmen?",
    "description": "Doe een keer vrijblijvend mee in de grootste klimhal van Arnhem",
    "cost": "5.00",
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

## Get only events in specific city

Get a list of upcoming events only in a specific city.

### HTTP Request

`GET https://api.inviplay.nl/event/upcoming/city/arnhem`

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
    "name": "Ga je mee klimmen?",
    "description": "Doe een keer vrijblijvend mee in de grootste klimhal van Arnhem",
    "activityId": 39,
    "locationId": 12,
    "start": "2021-07-16T08:00:00+00:00",
    "end": "2021-07-16T10:00:00+00:00",
    "maximumParticipants": 4,
    "cost": "5.00"
  }'
```
> The above request returns the created event id:

```json
{
  "eventId": 123,
}
```

Add a new event to the Inviplay database. Some remarks:

- You need to provide an id of a location. This can only be a location that is created by the user that is creating the event.
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
`start` | **required** | `Date` | - |
`end` | **required** | `Date` | - |
`maximumParticipants` | **required** | `Number` | `null` |
`recurring` | optional | `String` | `null` | Possible values: `sevenDays`, `fourteenDays`, `oneMonth`, `sixMonths`, `oneYear`
`targetGroup` | optional | `Number[]` | `null` | Array of targetGroup Id's
`cost` | optional | `String` | `null` | Format "5.00"

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
  "cost": "5.00",
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
curl -X POST 'https://api.inviplay.nl/event/subscribe/user' \
  -H 'Authorization: Bearer ACCESS_TOKEN'
  -H 'Content-Type: application/json' \
  --data-raw '{
    "userId": "5243a717-7084-4c82-9ea4-7f8f08d63327",
    "dates": [
      {
        "id": 456,
        "attendance": "yes"
      },
      {
        "id": 567,
        "attendance": "no"
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

> If there is a payment needed then a payment url will be provided

```json
{
  "status": "pending",
  "message": "payment needed, follow redirect url to complete request",
  "redirectUrl": "https://mollie.com/payment_link/tr_123ae3f"
}
```

Endpoint to sign up or signout an user to one or more dates of one event
### HTTP Request

`POST https://api.inviplay.nl/event/{{eventId}}/user`

### Request body
Parameter | Required | Type | Default | Description
--------- | -------- | ---- | ------- | -----------
`userId` | **required** | `String` | - |
`dates` | **required** | `Array` | - | Array of object per date that needs to be updated: `{ id: [Number], attendance: ['yes | no'] }`
`confirmationUrl` | **required** | `String` | - | Url where the user needs to land after a successful payment is made
