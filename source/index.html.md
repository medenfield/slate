---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  #- ruby
  #- python
  #- javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Open Angler API. You can use our API to access API endpoints, which can get information on various listings, trips, requests, guides, and other database resources.

Right now, all language bindings are demonstrated in Shell. We will add more language examples as time permits.

# Authentication

> To authorize, use this code:

```shell

curl -u "username:password" https://openangler.com/api/login-token

# With shell, you just pass the correct header with each request
curl "api_endpoint_here"
  -H "Content-Type: application/json"
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"
```

Open Angler uses an API access token to interface with the API. Please contact us to obtain permission.

Open Angler expects for the API key to be included in all API requests to the server in a header that looks like the following:

`access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs`

<aside class="notice">
You must replace <code>YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs</code> with your personal API key.
</aside>

### HTTP Request

`curl -u "username:password" https://openangler.com/api/login-token`


# Users  

## Register a new user

```shell
curl https://openangler.com/api/user-registration
  -X POST
  -H "Content-Type: application/json"
  -d "{\"name\":\"testuser@example.com\",\"pass\":\"password\",\"mail\":\"testuser@example.com\",\"first_name\":\"Test\",\"last_name\":\"User\"}"
```

> The above command returns JSON structured like this:

```json
{
  "data":{
    "uid":"23748"
  },
  "self":{
    "title":"Self",
    "href":"http:\/\/openangler.test.dd:8083\/api\/user-registration"
  }
}
```

### HTTP Request

`POST https://openangler.com/api/user-registration`


### URL Paramaters

Parameter | Type | Description
--------- | ---- | -----------
name | string | The unique username of the user account
mail | string | The unique email address of the user getAccount
pass | string | The password of the user account
first_name | string | The first name of of the user
last_name | string | The last name of the user
role | string | "guide" if user a guide.


## Get All Users

```shell
curl "https://openangler.com/api/users"
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"   
```

> The above command returns JSON structured like this:

```json

{
  "data":[
    {
      "label":null,
      "self":"http:\/\/openangler.test.dd:8083\/api\/v1.0\/users\/0"
    },
    {
      "id":1,
      "label":"Open Angler",
      "self":"http:\/\/openangler.test.dd:8083\/api\/v1.0\/users\/1",
      "mail":"user+1@localhost.localdomain"
    },
    {
      "id":96,
      "label":"test test",
      "self":"http:\/\/openangler.test.dd:8083\/api\/v1.0\/users\/96",
      "mail":"user+96@localhost.localdomain"
    },
  ]
}
```

### HTTP Request

`GET https://openangler.com/api/users/`


## Get a Specific User  

```
curl "https://openangler.com/api/users/<id>"
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"   
```

> The above command returns JSON structured like this:

```json
{
  "data":
  [
    {
      "id":"1",
      "label":"Open Angler",
      "self":"http:\/\/openangler.test.dd:8083\/api\/v1.0\/users\/1",
      "mail":"user+1@localhost.localdomain"
    }
  ],
  "self":{
    "title":"Self",
    "href":"http:\/\/openangler.test.dd:8083\/api\/v1.0\/users\/1"
  }
}
```

### HTTP Request

`GET https://openangler.com/api/users/<id>`


### URL Paramaters

Parameter | Description
--------- | -----------
ID | The ID of the user to retrieve


## Create a User

```shell
curl "https://openangler.com/api/users"
  -X POST
  -I
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"
  -d "{\"label\":\"test api user\", \"mail\":\"test@example.com\"}"   
```

> The above command returns JSON structured like this:

```json
{
  "data":
  [
    {
      "id":"1",
      "label":"Open Angler",
      "self":"http:\/\/openangler.test.dd:8083\/api\/v1.0\/users\/1",
      "mail":"user+1@localhost.localdomain"
    }
  ],
  "self":{
    "title":"Self",
    "href":"http:\/\/openangler.test.dd:8083\/api\/v1.0\/users\/1"
  }
}
```

## Delete a User  

```shell
curl "https://openangler.com/api/users/<id>"
  -X DELETE
  -I
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"   
```

### HTTP Request

`DELETE https://openangler.com/api/users/<ID>`

Response Code | Meaning
---------- | -------
200 | The user has been deleted
422 | The user does not exist


### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user to delete


# Listings

## Get All Listings

```shell
curl "https://openangler.com/api/listings"
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 37,
    "self": "http://openangler.com/api/v1.0/listings/37",
    "name": "Test Listing",
    "user": 1,
    "description": "<p>Test description of a listing</p>",
    "what_to_bring": "Be sure to wear comfortable clothing.",
    "charter_type": "Inshore Trip",
    "travel_type": "Power Boat",
    "boat_type": "Flats Boat",
    "fishing_types": [
      "Fly",
      "Light Tackle/Spin"
    ],
    "reel_types": [
      "Fly",
      "Baitcast",
      "Conventional",
      "Spinning"
    ],
    "included_items": [
      "Fishing License",
      "Fuel",
      "Ice",
    ],
    "boat_amenities": [
      "Poling Platform",
      "Radio",
    ],
    "other_amenities": [
      "Pick-up/Drop-off",
      "Tackle Shop"
    ],
    "terms": [
      "Catch and Release",
      "Great for Children"
    ],
    "experience": null,
    "image": {
      "self": "https://openangler.com/sites/default/files/Jimmy2.JPG",
      "filemime": "image/jpeg",
      "filesize": "1734493",
      "width": "3050",
      "height": "2033",
      "styles": {
        "thumbnail": "https://openangler.com/sites/default/files/styles/thumbnail/public/Jimmy2.JPG?itok=MdE5JIas",
        "medium": "https://openangler.com/sites/default/files/styles/medium/public/Jimmy2.JPG?itok=3BV5wpBe",
        "large": "https://openangler.com/sites/default/files/styles/large/public/Jimmy2.JPG?itok=RO_6FIYc"
      }
    },
    "lat": "32.776474900000",
    "lon": "-79.931051200000",
    "address": {
      "city": "Charleston",
      "state": "SC",
      "postal_code": "",
      "country": "US"
    },
    "payment_option": null,
    "length_half_day": "4",
    "pricing_half_day": "400",
    "length_3/4_day": "6",
    "pricing_3/4_day": "600",
    "length_full_day": "8",
    "pricing_full_day": "750",
    "pricing_lowest": "400",
    "deposit_percentage": null,
    "passengers_base": "2",
    "passengers_extra": {
      "count": "2",
      "price": "50"
    },
    "passengers_total": "4",
    "hours_extra": {
      "count": "2",
      "price": "100"
    },
    "other_fees": null,
    "cancellation_policy": "2",
    "status": "1",
    "metatags": {
      "title": "Metatag title",
      "description": "Metatag description."
    }
  }
]
```

This endpoint retrieves all listings.

### HTTP Request

`GET https://openangler.com/api/listings`

### Attributes

Name | Type | Description
--------- | ------- | -----------
id | integer | Unique ID.
name | string | The name of the listing.
user | integer | ID of the listing author.
description | string | The listing description, usually formatted HTML.
what_to_bring | string | What anglers will need to bring.
charter_type | string | The type of charter.
travel_type | string | The type of travel.
boat_type | string | The type of boat used on this listing.
fishing_types | array | Types of fishing offered on this listing.
reel_types | array | Types of reels suitable for this listing.
included_items | array | Items included with this listing.
boat_amenities | array | Boat amenities included with this listing.
other_amenities | array | Additional amenities.
terms | array | Terms and conditions, e.g., catch and release.
image | object | The featured image for this listing.
* self | string | The path to the file.
* filemime | string | The mimetype of this file.
* filesize | string | The filesize in bytes.
* width | string | The width of the original image.
* height | string | The height of the original image.
* styles | object | The generated styles
*** thumbnail | string | The path to the thumbnail.
*** medium | string | The path to the medium size image.
*** large | string | The path to the large size image.
lat | string | The latitude coordinate for this listing.
lon | string | The longitude coordinate for this listing.
address | object | The street address for this listing. (USA only)
payment_option | integer | Deposit or Full Payment
length_half_day | string | The number of hours for a half day trip.
pricing_half_day | string | The price of a half day trip.
length_3/4_day | string | The number of hours of a 3/4 day trip.
pricing_3/4_day | string | The price of a 3/4 day trip.
length_full_day | string | The number of hours of a full day trip.
pricing_full_day | string | The price of a full day trip.
pricing_lowest | string | The lowest available trip price.
deposit_percentage | string | The percentage amount needed when making a deposit.
passengers_base | string | The number of passengers that can travel without additional cost.
passengers_extra | object | Info about taking extra passengers.
* count | string | the number of extra passengers that can be accommodated.
* price | string | the price for each extra passenger.
passengers_total | string | the number of total passengers this listing can accommodate.
hours_extra | object | Info about adding extra hours.
* count | string | The number of total extra hours that can be added on.
* price | string | The price per extra hour.
other_fees | object |  (todo: build out this object)
cancellation_policy | string | The cancellation policy applied to this listing. (todo)
status | string | whether or not the listing is active. (todo: change to bool).
metatags | object | The metadata included with this listing. (todo: extend)
* title | string | The page title.
* description | string | The page description.


## Get a Specific Listing

```shell
curl "https://openangler.com/api/listings/2"
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"
```

> The above command returns JSON structured for a single listing as per 'Get All Listings'

This endpoint retrieves a specific listing.

### HTTP Request

`GET https://openangler.com/api/listings/<ID>`

### Attributes

This endpoint utilizes the same attributes as 'Get all Listings.'

## Create a Listing

```shell
curl "https://openangler.com/api/listings"
  -X "POST"
  -H "Content-Type: application/json"
  -H "access-token: UxotI49THODxc4Gbz0c_lggFww3Q1q7k9dd-IhUVGeg"
  -d "{\"name\":\"test listing\"}"
```

> The above command returns JSON structured like this:

```JSON
{
  "data":[
    {             
      "id":"157642",
      "self":"https:\/\/openangler.com\/api\/v1.0\/listings\/157642",
      "name":"test listing",
      "user":1,
      "description":null,
      "what_to_bring":null,
      "charter_type":"",
      "travel_type":"",
      "boat_type":"",
      "fishing_types":null,
      "reel_types":null,
      "included_items":null,
      "boat_amenities":null,
      "other_amenities":null,
      "terms":null,
      "experience":null,
      "image":null,
      "lat":null,
      "lon":null,
      "address":null,
      "payment_option":"0",
      "length_half_day":"4",
      "pricing_half_day":null,
      "length_3\/4_day":"6",
      "pricing_3\/4_day":null,
      "length_full_day":"8",
      "pricing_full_day":null,
      "pricing_lowest":null,
      "deposit_percentage":null,
      "passengers_base":"1",
      "passengers_extra":null,
      "passengers_total":null,
      "hours_extra":null,
      "other_fees":null,
      "cancellation_policy":null,
      "status":"1",
      "metatags":{
        "title":"- test listing | OpenAngler.com",
        "description":null
      }
    }
  ],
  "count":1682,
  "self": {
    "title":"Self",
    "href":"https:\/\/openangler.com\/api\/v1.0\/listings"
  },
  "next": {
    "title":"Next",
    "href":"https:\/\/openangler.com\/api\/v1.0\/listings?page%5Bnumber%5D=2"
  }
}
```


### HTTP Request

`POST https://openangler.com/api/listings/`


### Parameters

Name | Type | Description
--------- | ------- | -----------
name | string | The name of the listing.
description | string | The listing description, usually formatted HTML.
what_to_bring | string | What anglers will need to bring.
charter_type | integer | The charter type ID of the trip.
travel_type | integer | The travel type ID of the trip.
boat_type | integer | The boat type ID of the trip.
fishing_types | array | The fishing types of the trip.
reel_types | array | The reel types of the trip.
included_items |  |
boat_amenities |  |
other_amenities |  |
terms |  |
experience |  |


## Delete a Listing

```shell
curl "https://openangler.com/api/listings/"
  -X DELETE
  -I
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"
```


This endpoint deletes a specific listing.

### HTTP Request

`DELETE http://openngler.com/api/listings/<ID>`

Response Code | Meaning
---------- | -------
200 | The listing has been deleted.
422 | The listing does not exist. (Unprocessable Entity)


### Parameters

Parameter | Description
--------- | -----------
ID | The ID of the listing to delete

# Requests

Requests from a customer to book a listing on Open Angler


## Get a specific request

```
curl "https://openangler.com/api/requests/157851"
  -H "access-token: LoehxXU1OexRXmW7jl2XfjYMbRNbkAZo86wuXqKLUqw"
```

> The above command returns JSON structured like this:

```json
{
  "data":[
    {
      "id":"157852",
      "self":"http:\/\/openangler.test.dd:8083\/api\/v1.0\/requests\/157852",
      "name":"Lake Fishing Trip",
      "guide_id":"1",
      "listing_reference":"37",
      "trip_date":{
        "value":"2017-12-29 06:00:00",
        "value2":"2017-12-29 12:00:00",
        "timezone":"America\/New_York",
        "timezone_db":"America\/New_York",
        "date_type":"datetime"
      },
      "base_price":"600.00",
      "guide_fees":[
        {
          "fee_name":"Test Fee",
          "price":"100.00",
        },
        {
          "fee_name":"Test Fee 2",
          "price":"300.00",
        }
      ],
      "platform_fee":"40.00",
      "customer_total":"1041.00",
      "transaction_fee":"29.00",
      "commission":"0.00",
      "guide_payout":"971.00",
      "customer_id":"1",
      "customer_name":"John Doe",
      "customer_email":"johndoe@example.com",
      "customer_phone":"( 123 ) 123 - 2132",
      "customer_guest_count":"2",
      "cancellation_policy":"1",
      "confirmed_booking_reference":null
    }
  ],
  "self":{
    "title":"Self",
    "href":"http:\/\/openangler.test.dd:8083\/api\/v1.0\/requests\/157852"
  }
}
```

### HTTP Request

`GET http://openngler.com/api/requests/<ID>`


### Attributes

Parameter | Type | Description
--------- | ---- | -----------
name | string | The name of the trip request, convention is to use the name of the listing.
guide_id | string | The ID of the guide requested.
listing_reference | string | The ID of the listing requested.
trip_date | object | A date object.
* value | string | Start datetime. Formatted 2018-01-01 08:00:00
* value2 | string | Ending datetime. Formatted 2018-01-01 12:00:00
* timezone | string | The timezone of the datestamp.
* timezone_db | string | The timezone of the datestamp.
* date_type | string | datetime
base_price | string | The price of the trip before any booking or guide fees.
guide_fees | string | The price of any additional fees that may be offered for this trip.
platform_fee | string | The amount Open Angler uses to cover Stripe fees from the customer total.
customer_total | string | The total amount the customer will pay.
transaction_fee | string | The amount Open Angler uses to cover Stripe fees for the guide payout.
commission | string | The amount Open Angler keeps for referring the trip
guide_payout | string | The amount the guide will be paid via bank transfer.
customer_id | string | The user ID of the customer booking the trip.
customer_name | string | The name of the customer going on the trip.
customer_email | string | The email address of the customer going on the trip.
customer_phone | string | The phone number of the customer going on the trip.
customer_guest_count | string | The number of guests going on this trip.
cancellation_policy | string | The cancellation policy applied to this trip.


## Create a request

```
curl "https://openangler.com/api/requets"
  -X POST
  -H "Content-Type: application/json"
  -H "access-token: 123120-392103912-039"
  -d "{\"name\":\"test request\"}
```

> The above command returns JSON structured like this:

```json
{
  "data":[
    {
      "id":"157645",
      "self":"http:\/\/openangler.test.dd:8083\/api\/v1.0\/requests\/157645",
      "name":"test trip request",
      "guide_id":"1",
      "listing_reference":null,
      "trip_date":null,
      "base_price":null,
      "guide_fees":null,
      "platform_fee":null,
      "customer_total":null,
      "transaction_fee":null,
      "commission":null,
      "guide_payout":null,
      "customer_id":null,
      "customer_name":null,
      "customer_email":null,
      "customer_phone":null,
      "customer_guest_count":null,
      "cancellation_policy":null,
      "confirmed_booking_reference":null
    }
  ],
  "count":836,
  "self":{
    "title":"Self",
    "href":"http:\/\/openangler.test.dd:8083\/api\/v1.0\/requests"
  },
  "next":{
    "title":"Next",
    "href":"http:\/\/openangler.test.dd:8083\/api\/v1.0\/requests?page%5Bnumber%5D=2"
  }
}
```

### HTTP Request

`POST http://openangler.com/api/requests`



# Trips

Confirmed trips on Open Angler.


## Get a specific trip

```
curl "https://openangler.com/api/trips/<id>"
  -H "access-token: LoehxXU1OexRXmW7jl2XfjYMbRNbkAZo86wuXqKLUqw"
```

> The above command returns JSON structured like this:

```json
{
  "data":[
    {
      "id":"123456",
      "self":"https:\/\/openangler.com\/api\/v1.0\/trips\/123456",
      "name":"Lake Fishing Trip",
      "guide_id":"1",
      "listing_reference":"37",
      "trip_date":{
        "value":"2017-12-29 06:00:00",
        "value2":"2017-12-29 12:00:00",
        "timezone":"America\/New_York",
        "timezone_db":"America\/New_York",
        "date_type":"datetime"
      },
      "base_price":"600.00",
      "guide_fees":[
        {
          "fee_name":"Test Fee",
          "price":"100.00",
        },
        {
          "fee_name":"Test Fee 2",
          "price":"300.00",
        }
      ],
      "platform_fee":"40.00",
      "customer_total":"1041.00",
      "transaction_fee":"29.00",
      "commission":"0.00",
      "guide_payout":"971.00",
      "customer_id":"1",
      "customer_name":"John Doe",
      "customer_email":"johndoe@example.com",
      "customer_phone":"( 123 ) 123 - 2132",
      "customer_guest_count":"2",
      "cancellation_policy":"1",
      "request_reference" : "123455",
      "status": "16"
    }
  ],
  "self":{
    "title":"Self",
    "href":"https:\/\/openangler.com\/api\/v1.0\/requests\/123456"
  }
}
```

### HTTP Request

`GET http://openngler.com/api/trips/<ID>`


### Attributes

Parameter | Type | Description
--------- | ---- | -----------
name | string | The name of the trip, convention is to use the name of the listing.
guide_id | string | The ID of the guide.
listing_reference | string | The ID of the listing.
trip_date | object | A date object.
* value | string | Start datetime. Formatted 2018-01-01 08:00:00
* value2 | string | Ending datetime. Formatted 2018-01-01 12:00:00
* timezone | string | The timezone of the datestamp.
* timezone_db | string | The timezone of the datestamp.
* date_type | string | datetime
base_price | string | The price of the trip before any booking or guide fees.
guide_fees | string | The price of any additional fees that may be offered for this trip.
platform_fee | string | The amount Open Angler uses to cover Stripe fees from the customer total.
customer_total | string | The total amount the customer will pay.
transaction_fee | string | The amount Open Angler uses to cover Stripe fees for the guide payout.
commission | string | The amount Open Angler keeps for referring the trip
guide_payout | string | The amount the guide will be paid via bank transfer.
customer_id | string | The user ID of the customer booking the trip.
customer_name | string | The name of the customer going on the trip.
customer_email | string | The email address of the customer going on the trip.
customer_phone | string | The phone number of the customer going on the trip.
customer_guest_count | string | The number of guests going on this trip.
cancellation_policy | string | The cancellation policy applied to this trip.
request_reference | string | The ID of the Request node
workflow_state | string | The workflow state of the trip


## Workflow States

ID | Label
----- | -------
2 | Approved
3 | Referred
4 | Denied
6 | Requested
16 | Cancelled
21 | Trip Completed
26 | Customer Dispute
31 | Payment Issued
36 | Customer Refunded
41 | Deposit Payment Requested
46 | Payment Error
51 | No Response
56 | Expired
66 | Referral Accepted
71 | Referral Denied
76 | Customer Cancelled
81 | Checkout Completed
86 | Agent Cancelled
91 | Full Payment Requested


## Create a Trip

```
curl "https://openangler.com/api/trips"
  -X POST
  -H "access-token: LoehxXU1OexRXmW7jl2XfjYMbRNbkAZo86wuXqKLUqw"
  -d "{\"name\":\"test trip\", \"guide_id\": {\"uid\":1}, \"request_reference\":157857,  \"listing_reference\":37}"
```

> The above command returns JSON structured like this:

```JSON
{
  "data":[
    {
      "id":"157859",
      "self":"https:\/\/openangler.com\/api\/v1.0\/trips\/157859",
      "name":"test trip",
      "guide_id":"1",
      "listing_reference":"37",
      "trip_date":null,
      "base_price":null,
      "guide_fees":null,
      "platform_fee":null,
      "customer_total":null,
      "transaction_fee":null,
      "commission":null,
      "guide_payout":null,
      "customer_id":null,
      "customer_name":null,
      "customer_email":null,
      "customer_phone":null,
      "customer_guest_count":null,
      "cancellation_policy":null,
      "request_reference":"157857",
      "workflow_state":"6"
    }
  ],
  "count":475,
  "self":{
    "title":"Self","href":"http:\/\/openangler.test.dd:8083\/api\/v1.0\/trips"
  },
  "next":{
    "title":"Next","href":"http:\/\/openangler.test.dd:8083\/api\/v1.0\/trips?page%5Bnumber%5D=2"
  }
}


# Images

## Get All Images

```shell
curl "https://openangler.com/api/images"
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"   
```

> The above command returns JSON structured like this:

```json
{
  "data":[
    {
      "id": 1,
      "filename":"picture-2-1400630811.jpg",
      "image_metadata":{
        "uri":"public:\/\/pictures\/picture-2-1400630811.jpg",
        "filemime":"image\/jpeg",
        "filesize":15341,
        "status":1,
        "timestamp":1411524377,
        "height":320,
        "width":263
      }
    },
    {
      "id": 2,
      "filename":"picture-4-1400638221.jpg",
      "image_metadata":{
        "uri":"public:\/\/pictures\/picture-4-1400638221.jpg",
        "filemime":"image\/jpeg",
        "filesize":15341,
        "status":1,
        "timestamp":1411524377,
        "height":320,
        "width":263
      }
    }
  ],
  "count": 6142,
  "self": {
    "title": "Self",
    "href": "http://openangler.test.dd:8083/api/v1.0/images"
  },
  "next": {
    "title": "Next",
    "href": "http://openangler.test.dd:8083/api/v1.0/images?page%5Bnumber%5D=2"
  }
}
```

### HTTP Request

`GET https://openangler.com/api/images`

## Get a Specific Image

```shell
curl "https://openangler.com/api/images/2"
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"   
```

> The above command returns JSON structured like this:

```json
{
  "data":[
    {
      "id":"2",
      "filename":"picture-4-1400638221.jpg",
      "image_metadata":{
        "uri":"public:\/\/pictures\/picture-4-1400638221.jpg",
        "filemime":"image\/jpeg",
        "filesize":15341,
        "status":1,
        "timestamp":1411524377,
        "height":320,
        "width":263
      }
    }
  ],
  "self":{
    "title":"Self",
    "href":"https:\/\/openangler.com\/api\/v1.0\/images\/2"
  }
}
```



### HTTP Request

`GET https://openangler.com/api/images/<id>`



## Create an Image

```shell
  curl 'https://www.openangler.com/api/file-upload'
    -X POST
    -H "access-token: 2tlaxblv-vEAmYEe5rkjb5r6pMRXZBjf6Me4y7pNpUE"
    -F "image=@/path/to/file/file.jpg"
```

> The above command returns JSON structured like this:

```json

{
  "data":
  [
    [
      {
      "id":"39178",
      "label":"zanesboat2.jpg",
      "self":"http:\/\/openangler.test.dd:8083\/api\/file-upload\/39178"
      }
    ]
  ],
  "count":6142,
  "self":
  {
    "title":"Self",
    "href":"https:\/\/openangler.com\/api\/file-upload"
  },
  "next":
  {
    "title":"Next",
    "href":"https:\/\/openangler.com\/api\/file-upload?page%5Bnumber%5D=2"
  }
}
```

<aside class="warning">Upload images for listings and profiles prior to creating a new listing or profile.</aside>

### HTTP Request

`POST https://www.openangler.com/api/file-upload`


### Query Parameters

Name | Type | Description
--------- | ------- | -----------
None


## Delete an Image

```shell
curl "https://openangler.com/api/images/2"
  -X DELETE
  -H "access-token: 2tlaxblv-vEAmYEe5rkjb5r6pMRXZBjf6Me4y7pNpUE"   
```

### HTTP Request

`DELETE http://openngler.com/api/images/<ID>`

Response Code | Meaning
---------- | -------
200 | The image has been deleted
422 | The image does not exist

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the image to delete




# Categories

## Charter Types


This endpoint shows all charter Types

```shell
curl "https://openangler.com/api/chartertypes"
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"
```


You can filter by name using the built-in filtering mechanism

`filter[name]=Inshore%20Trip`

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 59,
      "self": "https://openangler.com/api/v1.0/chartertypes/59",
      "name": "Inland/Freshwater Trip"
    },
    {
      "id": 60,
      "self": "https://openangler.com/api/v1.0/chartertypes/60",
      "name": "Inshore Trip"
    },  
  ]
}
```

### HTTP Request

`GET https://openangler.com/api/chartertypes`


### Parameters

Parameter | description
--------- | -----------
id        | The id of the charter type
name      | The name of the charter type


## Fishing Types

This endpoint shows all fishing types

```shell
curl "https://openangler.com/api/fishingtypes"
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"
```

You can filter by name using the built-in filtering mechanism

`filter[name]=Bottom%20Fish`

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 66,
      "self": "https://openangler.com/api/v1.0/fishingtypes/66",
      "name": "Bottom Fish"
    },
    {
      "id": 67,
      "self": "https://openangler.com/api/v1.0/fishingtypes/67",
      "name": "Sport Fish/Trolling"
    }
  ]
}
```


### HTTP Request

`GET https://openangler.com/api/fishingtypes`


### Parameters

Parameter | description
--------- | -----------
id        | The id of the fishing type
name      | The name of the fishing type


## Reel Types

This endpoint shows all reel types

```shell
curl "https://openangler.com/api/reeltypes"
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"
```

You can filter by name using the built-in filtering mechanism

`filter[name]=Spinning`

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 3,
      "self": "https://openangler.com/api/v1.0/reeltypes/3",
      "name": "Spinning"
    },
    {
      "id": 44,
      "self": "https://openangler.com/api/v1.0/reeltypes/44",
      "name": "Conventional"
    }
  ]
}
```


### HTTP Request

`GET https://openangler.com/api/reeltypes`


### Parameters

Parameter | description
--------- | -----------
id        | The id of the reel type
name      | The name of the reel type


## Boat Types

This endpoint shows all boat types

```shell
curl "https://openangler.com/api/boattypes"
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"
```

You can filter by name using the built-in filtering mechanism

`filter[name]=Bay%20Boat`

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 171,
      "self": "https://openangler.com/api/v1.0/boattypes/171",
      "name": "Walk/Wade"
    },
    {
      "id": 176,
      "self": "https://openangler.com/api/v1.0/boattypes/176",
      "name": "Center Console"
    }
  ]
}
```


### HTTP Request

`GET https://openangler.com/api/boattypes`


### Parameters

Parameter | description
--------- | -----------
id        | The id of the boat type
name      | The name of the boat type


## Travel Types

This endpoint shows all travel types

```shell
curl "https://openangler.com/api/traveltypes"
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"
```

You can filter by name using the built-in filtering mechanism

`filter[name]=Raft`

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 139,
      "self": "https://openangler.com/api/v1.0/traveltypes/139",
      "name": "Walk/Wade"
    },
    {
      "id": 140,
      "self": "https://openangler.com/api/v1.0/traveltypes/140",
      "name": "Power Boat"
    }
  ]
}
```


### HTTP Request

`GET https://openangler.com/api/traveltypes`


### Parameters

Parameter | description
--------- | -----------
id        | The id of the travel type
name      | The name of the travel type


## Included Items

This endpoint shows all included items

```shell
curl "https://openangler.com/api/includeditems"
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"
```

You can filter by name using the built-in filtering mechanism

`filter[name]=Snacks`

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 76,
      "self": "https://openangler.com/api/v1.0/includeditems/76",
      "name": "Live Bait"
    },
    {
      "id": 77,
      "self": "https://openangler.com/api/v1.0/includeditems/77",
      "name": "Fish Cleaning"
    }
  ]
}
```


### HTTP Request

`GET https://openangler.com/api/includeditems`


### Parameters

Parameter | description
--------- | -----------
id        | The id of the included item
name      | The name of the included item


## Boat Amenities

This endpoint shows all boat amenities

```shell
curl "https://openangler.com/api/boatamenities"
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"
```

You can filter by name using the built-in filtering mechanism

`filter[name]=Tower`

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 20,
      "self": "https://openangler.com/api/v1.0/boatamenties/20",
      "name": "Head/Toilet"
    },
    {
      "id": 21,
      "self": "https://openangler.com/api/v1.0/boatamenities/21",
      "name": "Enclosed Cabin"
    }
  ]
}
```


### HTTP Request

`GET https://openangler.com/api/boatamenities`


### Parameters

Parameter | description
--------- | -----------
id        | The id of the boat amenity
name      | The name of the travel amenity


## Other Amenities

This endpoint shows all other amenities

```shell
curl "https://openangler.com/api/otheramenities"
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"
```

You can filter by name using the built-in filtering mechanism

`filter[name]=Overnight`

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 84,
      "self": "https://openangler.com/api/v1.0/otheramenities/84",
      "name": "Rod/Reel Rentals"
    },
    {
      "id": 85,
      "self": "https://openangler.com/api/v1.0/otheramenities/85",
      "name": "Boat/Raft Rentals"
    }
  ]
}
```


### HTTP Request

`GET https://openangler.com/api/otheramenities`


### Parameters

Parameter | description
--------- | -----------
id        | The id of the other amenity
name      | The name of the other amenity


## Terms and Conditions

This endpoint shows all terms and conditions

```shell
curl "https://openangler.com/api/terms"
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 57,
      "self": "https://openangler.com/api/v1.0/terms/57",
      "name": "Catch and Release"
    },
    {
      "id": 58,
      "self": "https://openangler.com/api/v1.0/terms/58",
      "name": "Catch and Keep"
    }
  ]
}
```


### HTTP Request

`GET https://openangler.com/api/terms`


### Parameters

Parameter | description
--------- | -----------
id        | The id of the term
name      | The name of the term


## Angler Types

This endpoint shows all Angler Types

```shell
curl "https://openangler.com/api/anglertypes"
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 56,
      "self": "https://openangler.com/api/v1.0/terms/56",
      "name": "Great For Children"
    },
    {
      "id": 151,
      "self": "https://openangler.com/api/v1.0/terms/151",
      "name": "Experienced Anglers"
    }
  ]
}
```


### HTTP Request

`GET https://openangler.com/api/anglertypes`


### Parameters

Parameter | description
--------- | -----------
id        | The id of the angler type
name      | The name of the angler type


## Tags

This endpoint shows all Tags used in blog posts

```shell
curl "https://openangler.com/api/tags"
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 2471,
      "self": "https://openangler.com/api/v1.0/tags/2471",
      "name": "Fishing"
    },
    {
      "id": 2476,
      "self": "https://openangler.com/api/v1.0/tags/2476",
      "name": "South Carolina"
    }
  ]
}
```


### HTTP Request

`GET https://openangler.com/api/tags`


### Parameters

Parameter | description
--------- | -----------
id        | The id of the tag
name      | The name of the tag
