# Payment

## Get status of specific payment for specific user

```shell
curl 'https://api.inviplay.nl/payment/{{paymentId}}/status/user/{{userId}}' \
  -H 'Authorization: Bearer ACCESS_TOKEN' \
```

> Returns the status of a payment if exists

```json
"paid"
```
> Possible values that can be returned:

```
open | failed | paid | canceled | expired | processing | refunded
```

Endpoint to get the status of a payment.

### HTTP Request

`GET https://api.inviplay.nl/payment/{{paymentId}}/status/user/{{userId}}`
