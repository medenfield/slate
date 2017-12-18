---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  #- php
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

# Images

## Get All Images

```shell
curl "https://openangler.com/api/images"
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"   
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 2,
    "name": "Offshore trip",
    "type": "offshore",
    "guide": 5
  },
  {
    "id": 3,
    "name": "Inshore trip",
    "type": "Inshore",
    "guide": 6
  }
]
```

### HTTP Request

`GET https://openangler.com/api/images/`

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

### Query Parameters


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


## Get a Specific Listing

```shell
curl "https://openangler.com/api/listings/2"
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Offshore trip",
  "type": "offshore",
  "guide": 5
}
```

This endpoint retrieves a specific listing.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET https://openangler.com/api/listings/<ID>`

### Query Parameters


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


## Create a Listing

```shell
curl "https://openangler.com/api/listings"
  -X "POST"
  -H "Content-Type: application/json"
  -H "access-token: UxotI49THODxc4Gbz0c_lggFww3Q1q7k9dd-IhUVGeg"
  -d "{\"name\":\"test api user\"}"
```

### HTTP Request

`POST https://openangler.com/api/listings/`


### Query Parameters

Name | Type | Description
--------- | ------- | -----------
id | integer | Unique ID of the listing.
name | string | The name of the listing.
description | string | The listing description, usually formatted HTML.
what_to_bring | string | What anglers will need to bring.
charter_type | integer | The charter type ID of the trip.
travel_type | integer | The travel type ID of the trip. 

## Delete a Specific Listing

```shell
curl "https://openangler.com/api/listings/2"
  -X DELETE
  -H "access-token: YZR5Ol_myOpa7k88CNj02HbYkOWzoxh0mNAqzpKXlNs"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific listing.

### HTTP Request

`DELETE http://openngler.com/api/listings/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the listing to delete
