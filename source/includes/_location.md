# Location

## Add location

```shell
curl -X POST 'https://api.inviplay.nl/location' \
  -H 'Authorization: Bearer ACCESS_TOKEN' \
  -H 'Content-type: application/json' \
  --data-raw '{
    "name": "Klimhal Mountain Network Arnhem",
    "description": "De grootste klimhal van Arnhem"
    "address": "Olympus 27",
    "city": "Arnhem",
    "postalCode": "6832EL",
  }'
```

> Returns the id of the created location

```json
{
  "locationId": 12
}
```

Endpoint to add a location

### HTTP Request

`POST https://api.inviplay.nl/location`


### Request body
Parameter | Required | Type | Default | Description
--------- | -------- | ---- | ------- | -----------
`name` | **required** | `String` | - | 
`address` | **required** | `String` | - | 
`city` | **required** | `Number` | - | 
`postalCode` | **required** | `Date` | - | 
`description` | optional | `String` | - | 
