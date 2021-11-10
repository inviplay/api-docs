# User
## Add new user

```shell
curl -X POST 'http://api.inviplay.nl/user' \
  -H 'Authorization: Bearer ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  --data-raw '{
  "username": "theo_janssen_79",
  "email": "theo@inviplay.nl",
  "firstName": "Theo",
  "lastName": "Janssen",
  "newsletterActivities": true,
  "postalCode": "6821AA",
  "rangeChoice": 5,
  "activities": [1, 4, 11],
  "newsletterGeneral": false,
}'
```

> This returns the userId of the created user:

```json
{
  "userId": "5243a717-7084-4c82-9ea4-7f8f08d63327"
}

```

This endpoint creates a new user in the Inviplay database

### HTTP Request

`POST http://api.inviplay.nl/user`

### Request body
Parameter | Required | Type | Default | Description
--------- | -------- | ---- | ------- | -----------
`username` | **required** | `String` | - | Needs to be unique
`email` | **required** | `String` | - | Email address can be used multiple times
`firstName` | **required** | `String` | - |
`lastName` | **required** | `String` | - |
`newsletterActivities` | optional | `Boolean` | `false` | If a user wants to receive invites for events in his neighbourhood this needs to be `true`.
`postalCode` | optional | `String` | `null` | If a user wants to receive invites for events this needs to be provided
`rangeChoice` | optional | `Number` | `null` | If a user wants to receive invites for events this is the range in kilometers from his own postalCode in which he will receive invites.
`activities` | optional | `Array` | `null` | If a user wants to receive invites for events these are the `activityId`'s he wants to receive invites for
`newsletterGeneral` | optional | `Boolean` | `false` | If a user wants to receive occasional updates about about Inviplay this needs to be `true`.

## Get user

```shell
curl 'http://api.inviplay.nl/user/5243a717-7084-4c82-9ea4-7f8f08d63327' \
  -H 'Authorization: Bearer ACCESS_TOKEN'
}'
```

> This returns the details of the user

```json
{
  "username": "theo_janssen_79",
  "email": "theo@inviplay.nl",
  "firstName": "Theo",
  "lastName": "Janssen",
  "newsletterActivities": true,
  "postalCode": "6821AA",
  "rangeChoice": 5,
  "activities": [1, 4, 11],
  "newsletterGeneral": false,
}
```

### HTTP Request

`GET http://api.inviplay.nl/user/{{userID}}`

## Get events a user has signed up for

```shell
curl 'http://api.inviplay.nl/user/5243a717-7084-4c82-9ea4-7f8f08d63327/events/joined' \
  -H 'Authorization: Bearer ACCESS_TOKEN'
}'
```

> This returns a list of dates of events the user has signed up for

```json
[
  {
    "eventId": 123,
    "name": "Ga je mee klimmen?",
    "description": "Doe een keer vrijblijvend mee in de grootste klimhal van Arnhem",
    "cost": "5.00",
    "dateId": 456,
    "startDateTime": "2021-07-16T08:00:00+00:00",
    "endDateTime": "2021-07-16T10:00:00+00:00",
  }
]
```
This request returns all the dates a user has signed up for. 
### HTTP Request

`GET http://api.inviplay.nl/user/{{userID}}/events_joined`

## Get events a user has created

```shell
curl 'http://api.inviplay.nl/user/5243a717-7084-4c82-9ea4-7f8f08d63327/events/created' \
  -H 'Authorization: Bearer ACCESS_TOKEN'
}'
```

> This returns a list of events the user has created

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
This request returns all the dates a user has created. 
### HTTP Request

`GET http://api.inviplay.nl/user/{{userID}}/events/created`

## Get locations that a user has created

```shell
curl 'http://api.inviplay.nl/user/5243a717-7084-4c82-9ea4-7f8f08d63327/locations' \
  -H 'Authorization: Bearer ACCESS_TOKEN'
}'
```

> This returns a list of events the user has created

```json
[
  {
    "adress": "Oudegracht 143",
    "city": "Utrecht",
    "coordinates": {
      "lat": 52.09129938255362,
      "lng": 5.117693057604256
    },
    "country": "Nederland",
    "description": null,
    "id": 1,
    "image": null,
    "imageUrl": null,
    "name": "Utrecht centrum",
    "postalCode": "3511 AJ"
    },
  }
]
```
This request returns all the locations a user has created. 
### HTTP Request

`GET http://api.inviplay.nl/user/{{userID}}/locations`
