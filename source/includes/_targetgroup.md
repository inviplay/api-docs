# Targetgroup

A targetgroup is used to specify for which people an event is organized. This is a fixed list in the Inviplay database

## Get list of target groups

```shell
curl 'https://api.inviplay.nl/targetgroup' \
  -H 'Authorization: Bearer ACCESS_TOKEN' \
```

> Returns a list of targetgroups

```json
[
  {
    "id": 1,
    "name": "adults",
  },
  {
    "id": 2,
    "name": "children",
  },
  {
    "id": 3,
    "name": "65+",
  },
]
```

Endpoint to get a list of possible targetgroups

### HTTP Request

`GET https://api.inviplay.nl/targetgroup`
