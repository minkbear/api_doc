
# Introduction Shipyous API v1

Shipyours API enable you to manage data on server through REST API.

Please reach out directly to itmanager@outsourcingfactory.co.th for URI, Token.

# Authentication

Shipyours uses Bearer Token in which you can acquire the token by sending an inquiry email to itmanager@outsourcingfactory.co.th (please also specify your customer code within the email).

Shipyours will reply back with Bearer Token, in which it can be used in the next topic.

Note: Bearer Token can only be used on a single project.

# Headers

Please ensure to use below header format for every request.

`Accept: application/json`

`Content-Type: application/json`

`Authorization: Bearer API_KEY_HERE`

# Errors

Shipyous API uses conventional HTTP response codes to indicate the success or failure of an API request. The table below contains a summary of the typical response codes:

Code | Description
-------------- | --------------
200 | Normal
401 | Permission denied because of no Token
404 | The request resource could not be found.
422 | Incorrect or Insufficient Parameters.
500 | Internal error in Shipyours API (please notify us)
503 | Shipyous API is offline for maintenance.

## 401: Response Sample

```json
{
    "message": "401 Unauthorized",
    "status_code": 401
}
```

## 404: Response Sample

```json
{
    "message": "404 Not Found",
    "status_code": 404
}
```

## 422: Response Sample

```json
{
    "message": "422 Unprocessable Entity",
    "errors": {
        "schedule_deliver_date": [
            "The schedule deliver date does not match the format Y-m-d."
        ]
    },
    "status_code": 422
}
```

## 500: Response Sample

```json
{
    "message": "...",
    "status_code": 500
}
```

# Orders

## Create an order

### HTTP Request

`POST /api/v1/order`

### Parameters

Key | Description
-------------- | --------------
schedule_deliver_date | Shipping date in yyyy-mm-dd format (2018-07-20)
schedule_deliver_time | Desired shipping time in hh:mm (24H) format (17:20)
rc_name | Reciever's name
rc_address1 | Reciever's address 1 (line 1)
rc_address2 | Reciever's address (sub district)
rc_address3 | Reciever's address 3 (district)
rc_country | Destination country (see valid list in Reference > Country )
rc_postcode | Zip code
rc_phone | Telephone number
rc_email | Email
cod_amount | Cash on delivery amount to be collected
remark | Remark
ref1 | Reference 1
ref2 | Reference 2
carrier_method_code | Shipping method 
(see detail in Reference > Carrier Method Code)
items | See more detail in Reference > Item Object

### Sample Request

```json
{
	"schedule_deliver_date": "2018-05-31",
	"schedule_deliver_time": "",
	"rc_name": "ทดสอบ",
	"rc_address1": "ทดสอบ",
	"rc_address2": "ทดสอบ",
	"rc_address3": "ทดสอบ",
	"rc_country": "Thailand",
	"rc_postcode": "10600",
	"rc_phone": "0851234567",
	"rc_email": "",
	"cod_amount": "",
	"remark": "",
	"ref1": "",
	"ref2": "",
	"carrier_method_code": "TP1",
	"items": {"sku-01":"2","sku-01":"1"}
}
```

### Sample Response

```json
{
    "success": true,
    "data": {
        "code": "E0-1807-1172",
        "status": "WAIT_FOR_PROCESSING",
        "schedule_deliver_date": "2018-05-31",
        "schedule_deliver_time": "00:00:00",
        "weight_g": 0,
        "tracking_number": "",
        "carrier_method_code": "TP1",
        "cod_amount": 0,
        "rc_name": "ทดสอบ",
        "rc_address1": "ทดสอบ",
        "rc_address2": "ทดสอบ",
        "rc_address3": "ทดสอบ",
        "rc_postcode": "10600",
        "rc_country": "Thailand",
        "rc_phone": "0851234567",
        "rc_email": "",
        "remark": "",
        "ref1": "",
        "ref2": "",
        "items": [
            {
                "sku_code": "sku-01",
                "qty": 2
            },
            {
                "sku_code": "sku-02",
                "qty": 1
            }
        ]
    },
    "message": "Orders saved successfully"
}
```

## Get an order

### HTTP Request

`GET /api/v1/order/ORDER_CODE_HERE`

ex. `GET /api/v1/order/E0-1801-0001`

### Sample Response

```json
{
    "success": true,
    "data": {
        "code": "E0-1806-4951",
        "status": "DONE",
        "schedule_deliver_date": "2018-06-29",
        "schedule_deliver_time": "",
        "weight_g": 109,
        "tracking_number": "TEST123456",
        "carrier_method_code": "SY1",
        "cod_amount": 1190,
        "rc_name": "test",
        "rc_address1": "test test",
        "rc_address2": "",
        "rc_address3": "",
        "rc_postcode": "84130",
        "rc_country": "Thailand",
        "rc_phone": "02123456789",
        "rc_email": "",
        "remark": "รับสินค้า 29/6/18",
        "ref1": "123456",
        "ref2": "",
        "items": [
            {
                "sku_code": "sku-01",
                "qty": 1
            }
        ]
    },
    "message": "Orders retrieved successfully"
}
```

# Reference

## Item Object

Item object is JSON object that that identify an SKU and shipping quantity.
"Key" is an SKU code while "Value" is desired quantity.

ex.

```json
{
	"sku_01":"1",
	"sku_02":"1",
	"sku_03":"1"
}
```

## Order Status Code

Key | Description
-------------- | --------------
WAIT_FOR_PROCESSING | Processing
WAIT_FOR_PICK | Waiting for pick
WAIT_FOR_CAL_SHIPPING_COST | Waiting for shipping cost to be calculated
WAIT_FOR_DELIVER | Waiting to dispatch
WAIT_FOR_RESULT | Waiting for shipping confirmation
DONE | Sent
CANCEL | Cancelled
POSTPONE | Postpone

## Carrier Method Code

Key | Description
-------------- | --------------
TP1 | EMS
TP2 | Registered
TP3 | Int’l Small Packet-Air
TP4 | Parcel
TP5 | Registered Int’l Small Packet-Air
TP6 | International EMS
DH1 | DHL Express
SY1 | Warehouse Pickup
AL1 | Alpha
KR1 | KERRY
OF1 | MESSENGER
SP1 | Shoppee (pickup)
LZ1 | LAZADA (pickup)
ES1 | 11street (pickup)
SS1 | Season (pickup)
DHC | DHL TH

## Country

Please go to https://gist.github.com/kalinchernev/486393efcca01623b18d

<!--stackedit_data:
eyJoaXN0b3J5IjpbNjA2OTk3Mjc4XX0=
-->