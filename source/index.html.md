---
title: Latlong API Reference

language_tabs:
  - ruby
  - javascript
  - shell
  - java

toc_footers:
  - <a href='https://latlong.in/contact/'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Latlong API documentation. User can use our API endpoints, which can get information on various locatioon based services like reverse geocode, locality based driving directions, locality based auto-complete and geocode/geosearch.

Latlong also has APIs to serve its customer with endpoints for searching stores within given location and searching for their stores around a given geo point, etc.

We have language bindings in Shell, Ruby, javascript, java and Python! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```ruby
# With ruby, use `rest-client` for simpler access

# Request for access_token using client's credentials
require 'rest-client'
response = RestClient.post 'https://api.latlong.in/oauth/token', {
        grant_type: 'client_credentials',
        client_id: CLIENT ID,
        client_secret: SECRET ID
      }
token = JSON.parse(response)["access_token"]

```
<!-- 
```python
import kittn

api = kittn.authorize('meowmeowmeow')
``` -->

```shell
# clients request for accessing thier own access_token
curl https://api.latlong.in/oauth/token
  --data "grant_type=client_credentials&client_id=CLIENT ID&client_secret=SECRET ID"

# authenticating using access_token given for using general api
curl https://api.latlong.in/v2/search.json?query=STRING -H 'Authorization: Bearer <ACCESS_TOKEN>'
```

```javascript

        $.post("https://api.latlong.in/oauth/token",
        {
          grant_type: "client_credentials",
          client_id: '<CLIENT_ID>',
          client_secret: "<CLIENT_SECRET>"
        },
        function(data,status){
            console.log("Token: " + data.access_token + "\nStatus: " + status);
        });
```
```java
// Java code goes here

// Use any of the http client library for fetching rest service data
okhttp   //(http://square.github.io/okhttp/)
retrofit //(http://square.github.io/retrofit/)

// Or Use Standard java libraries like 
JAX-RS   //(http://docs.jboss.org/resteasy/docs/3.0.16.Final/userguide/html/RESTEasy_Client_Framework.html)
jersey   //(https://jersey.java.net/documentation/latest/client.html)
```

> Make sure to replace `CLIENT ID`,`SECRET ID`,`ACCESS_TOKEN` with proper values provided for you.

Users need to have `access_token` to access all latlong API. How to get your `access_token`?

* If you are signed up with latlong we would have provided you your `secret` keys to generate `access_token`s.
* In case you are not yet signed up, you can register for `secret` keys at our [contact page](http://latlong.in/contact/).

By making a `POST` request call to latlong API using provided `CLIENT_ID` and `SECRET_ID` user can get their `access_token` which is valid for one hour of duration.

Latlong API expects access_token to be included in all API requests to the server in the url that looks like the following:

`access_token=a70bf52c9d649675152485e2c9b15cf9b2fc3ebb54628944ebd52e293813fbdc`

# Reverse Geocode
```ruby
require 'rest-client'
response = RestClient.get "https://api.latlong.in/v2/reverse_geocode.json", {
        params: {:latitude => '12.9306361', :longitude => '77.5783206'}
      }
```

```shell
curl https://api.latlong.in/v2/reverse_geocode.json?latitude=12.9306361&longitude=77.5783206 -H 'Authorization: Bearer <ACCESS_TOKEN>'
```

```javascript
https://api.latlong.in/v2/reverse_geocode.json?latitude=12.9306361&longitude=77.5783206
```

```java
// Java code goes here

// Use any of the http client library for fetching rest service data
okhttp   //(http://square.github.io/okhttp/)
retrofit //(http://square.github.io/retrofit/)

// Or Use Standard java libraries like 
JAX-RS   //(http://docs.jboss.org/resteasy/docs/3.0.16.Final/userguide/html/RESTEasy_Client_Framework.html)
jersey   //(https://jersey.java.net/documentation/latest/client.html)
```

> The above API returns JSON structured like this:

```json
{
    "data": {
        "poi": {},
        "road": {},
        "locality": [
            {
                "id": 750000108,
                "order": 4,
                "type": "Sub-Location",
                "name": "7th block"
            },
            {
                "id": 670000017,
                "order": 5,
                "type": "Locality",
                "name": "Jayanagar"
            },
            {
                "id": 510000021,
                "order": 7,
                "type": "City",
                "name": "Bengaluru"
            },
            {
                "id": 420000001,
                "order": 9,
                "type": "State",
                "name": "Karnataka"
            }
        ],
        "more": ""
    }
}
```

This endpoint returns the reverse geocoded address along with their unique identity number and area order for the given geo point. 

### HTTP Request
`GET https://api.latlong.in/v2/reverse_geocode.json`
####  example
`GET https://api.latlong.in/v2/reverse_geocode.json?latitude=12.9306361&longitude=77.5783206`


### Query Parameters

Parameter | Type | Presence | Description
--------- | ---- | -------- | -----------
latitude | integer/float | must | Latitude of the location
longitude | integer/float | must | Longitude of the location

<aside class="notice">
  you must add your <code>access_token</code> with all API request
</aside>
<aside class="success">
200 — suggestion and related info successfully retrieved.
</aside>


# Auto complete
```ruby
require 'rest-client'
response = RestClient.get "https://api.latlong.in/v2/autocomplete.json", {
        params: {:query => 'beng'}
      }
```

```shell
curl https://api.latlong.in/v2/autocomplete.json?query=beng -H 'Authorization: Bearer <ACCESS_TOKEN>'
```

```javascript
https://api.latlong.in/v2/autocomplete.json?query=beng
```

```java
// Java code goes here

// Use any of the http client library for fetching rest service data
okhttp   //(http://square.github.io/okhttp/)
retrofit //(http://square.github.io/retrofit/)

// Or Use Standard java libraries like 
JAX-RS   //(http://docs.jboss.org/resteasy/docs/3.0.16.Final/userguide/html/RESTEasy_Client_Framework.html)
jersey   //(https://jersey.java.net/documentation/latest/client.html)
```

> The above API returns JSON structured like this:

```json
{
  "data": [
          {
            "name": "Bengalur,Karnataka",
            "geo": 510000021
          },
          {
            "name": "Bengaluru Urban District,Karnataka",
            "geo": 440000004
          },
          {
            "name": "Bengaluru Rural District,Karnataka",
            "geo": 480000015
          },
          {
            "name": "Bengre,Mangaluru,Karnataka",
            "geo": 890001390
          },
          {
            "name": "Bengali Square,Indore,Indore",
            "geo": 1860001967
          },
          {
            "name": "Bengaluru Jalamandali,Gandhi Nagar:Central Bangalore:Central Bengaluru,Bengaluru Urban District,Karnataka",
            "geo": 240036855
          },
          {
            "name": "Bengalmattam,Ooty,Tamil Nadu",
            "geo": 680005109
          }
        ]
}
```

This endpoint returns matched location suggestion along with their unique identity number based on entered characters. API initially tries to match entered text within user's state. If it don't find any results then it will searches for match in India level. Results are populated based on their popularity. 


### HTTP Request
`GET https://api.latlong.in/v2/autocomplete.json`
####  example
`GET https://api.latlong.in/v2/autocomplete.json?query=beng`


### Query Parameters

Parameter | Type | Presence | Description
--------- | ---- | -------- | -----------
query | string | must | name to be searched

<aside class="notice">
  you must add your <code>access_token</code> with all API request
</aside>
<aside class="success">
200 — suggestion and related info successfully retrieved.
</aside>

# Search

## Store search within location

```ruby
require 'rest-client'
response = RestClient.get "https://api.latlong.in/v2/brands/[brand_id]/find.json", {
        params: {:query => 'bengaluru'}
      }
```

```shell
curl https://api.latlong.in/v2/brands/[brand_id]/find.json?query=bengaluru -H 'Authorization: Bearer <ACCESS_TOKEN>'
```

```javascript
https://api.latlong.in/v2/brands/[brand_id]/find.json?query=bengaluru
```

```java
// Java code goes here

// Use any of the http client library for fetching rest service data
okhttp   //(http://square.github.io/okhttp/)
retrofit //(http://square.github.io/retrofit/)

// Or Use Standard java libraries like 
JAX-RS   //(http://docs.jboss.org/resteasy/docs/3.0.16.Final/userguide/html/RESTEasy_Client_Framework.html)
jersey   //(https://jersey.java.net/documentation/latest/client.html)
```

> The above API returns JSON structured like this:

```json
{
  "lr": {
        "name": "Bengaluru",
        "type": 4,
        "id": 510000021,
        "geoproperty": "POLYGON ((77.4333697482847 12.9408367512911, 77.4497203721123 12.9162692658496, 
              .,
              .,
              77.4450402753991 12.9831397444511, 77.4333697482847 12.9408367512911))",
        "anchor_point": "POINT (77.570708 12.977246)"
      },
  "search_type": "within",
  "count": 1,
  "stores": [{
              "id": 1,
              "dealer_id": null,
              "wp_name": "ONZE Technologies (Latlong) - 7th Block Jayanagar, Bangalore",
              "category_id": 270,
              "distance": 0,
              "is_routeable": true,
              "wp_id": 240090126,
              "phone_no": "+918026712175",
              "email_id": null,
              "address": "​#l/B-48, Jaylakshmi Arcade, 27th Cross Road, 7th Block, Jayanagar, Bengaluru - 560070",
              "city": "Bengaluru",
              "state": "Karnataka",
              "store_timings": "Monday - Friday, 9 AM - 6 PM",
              "geofeature": {
                  "geoproperty": "POINT (77.5663626194 12.9186399138545)"
              }
            }]
}
```

This endpoint returns stores within entered location along with geo property of the entered location and count of stores found within entered location.


### HTTP Request
`GET https://api.latlong.in/v2/brands/[brand_id]/find.json`
####  example
`GET https://api.latlong.in/v2/brands/[brand_id]/find.json?query=bengaluru`

### Using latlong's unique location id for faster search
API works faster with latlong's unique geofeature id returned from autocomplete API for interested location name.
####  example
`GET https://api.latlong.in/v2/brands/[brand_id]/find.json?geofeature=510000021`

### Query Parameters

Parameter | Type | Presence | Description
--------- | ---- | -------- | -----------
brand_id | integer | must | registered brand id from latlong
query | string | must | location name where stores to be searched
category | integer | optional | category id of registered brand
geofeature | integer | optional | latlong's unique id for location
metadata | integer | optional | metadata id
shuffle | boolean | optional | whether to shuffle the response list or not
sure_search | boolean | optional | true - calls the around me method if no stores present inside the polygon, false - gives the empty array

<aside class="notice">
  you must add your <code>access_token</code> with all API request
</aside>
<aside class="success">
200 — Store search and related info successfully retrieved.
</aside>

## Store search around geo point

```ruby
require 'rest-client'
response = RestClient.get "https://api.latlong.in/v2/brands/[brand_id]/stores_around.json", {
        params: {:lat => 12.976182 ,:long => 77.570901}
      }
```

```shell
curl https://api.latlong.in/v2/brands/[brand_id]/stores_around.json?lat=12.976182&long=77.570901 -H 'Authorization: Bearer <ACCESS_TOKEN>'
```

```javascript
https://api.latlong.in/v2/brands/[brand_id]/stores_around.json?lat=12.976182&long=77.570901
```

```java
// Java code goes here

// Use any of the http client library for fetching rest service data
okhttp   //(http://square.github.io/okhttp/)
retrofit //(http://square.github.io/retrofit/)

// Or Use Standard java libraries like 
JAX-RS   //(http://docs.jboss.org/resteasy/docs/3.0.16.Final/userguide/html/RESTEasy_Client_Framework.html)
jersey   //(https://jersey.java.net/documentation/latest/client.html)
```

> The above API returns JSON structured like this:

```json
{
  "count": 1,
  "stores": [{
              "id": 1,
              "dealer_id": null,
              "wp_name": "ONZE Technologies (Latlong) - 7th Block Jayanagar, Bangalore",
              "category_id": 270,
              "distance": 0,
              "is_routeable": true,
              "wp_id": 240090126,
              "phone_no": "+918026712175",
              "email_id": null,
              "address": "​#l/B-48, Jaylakshmi Arcade, 27th Cross Road, 7th Block, Jayanagar, Bengaluru - 560070",
              "city": "Bengaluru",
              "state": "Karnataka",
              "store_timings": "Monday - Friday, 9 AM - 6 PM",
              "geofeature": {
                  "geoproperty": "POINT (77.5663626194 12.9186399138545)"
              }
            }]
}
```

This endpoint returns 10 stores around given geo point (lattitude and longitude). Store list is sorted based on distance from given location to the given point.


### HTTP Request
`GET https://api.latlong.in/v2/brands/[brand_id]/stores_around.json`
####  example
`GET https://api.latlong.in/v2/brands/[brand_id]/stores_around.json?lat=12.976182&long=77.570901`

### Query Parameters

Parameter | Type | Presence | Description
--------- | ---- | -------- | -----------
brand_id | integer | must | registered brand id from latlong
category_id | integer | optional | category id of registered brand
lat | integer/float | must | lattitude of location
long | integer/float | must | longitude of location
metadata | integer | optional | metadata id

<aside class="notice">
  you must add your <code>access_token</code> with all API request
</aside>

<aside class="success">
200 — Store search and related info successfully retrieved.
</aside>

# Location Specifier
```ruby
require 'rest-client'
response = RestClient.get "https://api.latlong.in/v2/get_ls.json", {
        params: {:id => '240090126'}
      }
```

```shell
curl https://api.latlong.in/v2/get_ls.json?query=240090126 -H 'Authorization: Bearer <ACCESS_TOKEN>'
```

```javascript
https://api.latlong.in/v2/get_ls.json?query=240090126
```

```java
// Java code goes here

// Use any of the http client library for fetching rest service data
okhttp   //(http://square.github.io/okhttp/)
retrofit //(http://square.github.io/retrofit/)

// Or Use Standard java libraries like 
JAX-RS   //(http://docs.jboss.org/resteasy/docs/3.0.16.Final/userguide/html/RESTEasy_Client_Framework.html)
jersey   //(https://jersey.java.net/documentation/latest/client.html)
```

> The above API returns JSON structured like this:

```json
{
    "ls": [
        "27th Cross Road\nNEAR Nanda Talkies Road-Ganesha Temple Signal\nNEXT TO Dream Zone Furnishings\n7th block,Jayanagar,Bengaluru"
    ]
}
```

This endpoint returns the landmark based address for the given latlong's unique id for location points. 


### HTTP Request
`GET https://api.latlong.in/v2/get_ls.json`
####  example
`GET https://api.latlong.in/v2/get_ls.json?id=240090126`


### Query Parameters

Parameter | Type | Presence | Description
--------- | ---- | -------- | -----------
id | integer | must | latlong's unique id for location

<aside class="notice">
  you must add your <code>access_token</code> with all API request
</aside>
<aside class="success">
200 — suggestion and related info successfully retrieved.
</aside>

# Stores

## Store details

```ruby
require 'rest-client'
response = RestClient.get "https://api.latlong.in/v2/brands/[brand_id]/stores/[store_id].json"
```

```shell
curl https://api.latlong.in/v2/brands/[brand_id]/stores/[store_id].json? -H 'Authorization: Bearer <ACCESS_TOKEN>'
```

```javascript
https://api.latlong.in/v2/brands/[brand_id]/stores/[store_id].json?
```

```java
// Java code goes here

// Use any of the http client library for fetching rest service data
okhttp   //(http://square.github.io/okhttp/)
retrofit //(http://square.github.io/retrofit/)

// Or Use Standard java libraries like 
JAX-RS   //(http://docs.jboss.org/resteasy/docs/3.0.16.Final/userguide/html/RESTEasy_Client_Framework.html)
jersey   //(https://jersey.java.net/documentation/latest/client.html)
```

> The above API returns JSON structured like this:

```json
{
    "store": {
        "id": 1,
        "wp_name": "ONZE Technologies (Latlong) - 7th Block Jayanagar, Bangalore",
        "category_id": 270,
        "distance": null,
        "is_routeable": true,
        "way_point": {
            "id": 240090126,
            "phone_no": "+918026712175",
            "email_id": "",
            "address": "#l/B-48, Jaylakshmi Arcade, 27th Cross Road, 7th Block, Jayanagar, Bengaluru - 560070",
            "geofeature": {
                "geoproperty": "POINT (77.5783206 12.9306361)"
            }
        },
        "store_timings": "Monday - Friday, 9 AM - 6 PM"
    }
}
```

This endpoint returns all store  count along with state level store counts.


### HTTP Request
`GET https://api.latlong.in/v2/brands/[brand_id]/stores/[store_id].json`
####  example
`GET https://api.latlong.in/v2/brands/24/stores/1.json?`

### Query Parameters

Parameter | Type | Presence | Description
--------- | ---- | -------- | -----------
brand_id | integer | must | registered brand id from latlong
store_id | integer | must | store id of registered brand

<aside class="notice">
  you must add your <code>access_token</code> with all API request
</aside>
<aside class="success">
200 — Store search and related info successfully retrieved.
</aside>

## Store Metadata

```ruby
require 'rest-client'
response = RestClient.get "https://api.latlong.in/v2/brands/[brand_id]/stores/[store_id]/metadata.json"
```

```shell
curl https://api.latlong.in/v2/brands/[brand_id]/stores/[store_id]/metadata.json? -H 'Authorization: Bearer <ACCESS_TOKEN>'
```

```javascript
https://api.latlong.in/v2/brands/[brand_id]/stores/[store_id]/metadata.json?
```

```java
// Java code goes here

// Use any of the http client library for fetching rest service data
okhttp   //(http://square.github.io/okhttp/)
retrofit //(http://square.github.io/retrofit/)

// Or Use Standard java libraries like 
JAX-RS   //(http://docs.jboss.org/resteasy/docs/3.0.16.Final/userguide/html/RESTEasy_Client_Framework.html)
jersey   //(https://jersey.java.net/documentation/latest/client.html)
```

> The above API returns JSON structured like this:

```json
{
    "store_timings": "Monday - Friday, 9 AM - 6 PM",
    "store_images": [],
    "metadatas": []
}
```

This endpoint returns all store's metadata information for the given store id.


### HTTP Request
`GET https://api.latlong.in/v2/brands/[brand_id]/stores/[store_id]/metadata.json`
####  example
`GET https://api.latlong.in/v2/brands/24/stores/1/metadata.json?`

### Query Parameters

Parameter | Type | Presence | Description
--------- | ---- | -------- | -----------
brand_id | integer | must | registered brand id from latlong
store_id | integer | must | store id of registered brand

<aside class="notice">
  you must add your <code>access_token</code> with all API request
</aside>
<aside class="success">
200 — Store search and related info successfully retrieved.
</aside>

## Store places
```ruby
require 'rest-client'
response = RestClient.get "https://api.latlong.in/v2/brands/[brand_id]/places.json"
```

```shell
curl https://api.latlong.in/v2/brands/[brand_id]/places.json -H 'Authorization: Bearer <ACCESS_TOKEN>'
```

```javascript
https://api.latlong.in/v2/brands/[brand_id]/places.json
```

```java
// Java code goes here

// Use any of the http client library for fetching rest service data
okhttp   //(http://square.github.io/okhttp/)
retrofit //(http://square.github.io/retrofit/)

// Or Use Standard java libraries like 
JAX-RS   //(http://docs.jboss.org/resteasy/docs/3.0.16.Final/userguide/html/RESTEasy_Client_Framework.html)
jersey   //(https://jersey.java.net/documentation/latest/client.html)
```

> The above API returns JSON structured like this:

```json
{
  "data": [
          {
      		"state": "Andhra Pradesh",
      		"cities": [
       					 "Guntur",
        				 "Tirupati Taluk",
        				 "Vijayawada Taluk",
       					 "Vishakhapatnam"
      					]
   		 },
    	{
      		"state": "Assam",
      		"cities": [
        				"Guwahati"
     				 	]
    	}
    	]
}
```

This endpoint returns alphabetically ordered list of States including Cities which are all contains brand's stores in it.


### HTTP Request
`GET https://api.latlong.in/v2/brands/[brand_id]/places.json`
####  example
`GET https://api.latlong.in/v2/brands/1234/places.json`


<aside class="notice">
  you must add your <code>access_token</code> with all API request
</aside>
<aside class="success">
200 — suggestion and related info successfully retrieved.
</aside>

## All Stores
```ruby
require 'rest-client'
response = RestClient.get "https://api.latlong.in/v2/brands/[brand_id]/stores.json"
```

```shell
curl https://api.latlong.in/v2/brands/[brand_id]/stores.json -H 'Authorization: Bearer <ACCESS_TOKEN>'
```

```javascript
https://api.latlong.in/v2/brands/[brand_id]/stores.json
```

```java
// Java code goes here

// Use any of the http client library for fetching rest service data
okhttp   //(http://square.github.io/okhttp/)
retrofit //(http://square.github.io/retrofit/)

// Or Use Standard java libraries like 
JAX-RS   //(http://docs.jboss.org/resteasy/docs/3.0.16.Final/userguide/html/RESTEasy_Client_Framework.html)
jersey   //(https://jersey.java.net/documentation/latest/client.html)
```

> The above API returns JSON structured like this:

```json
[
    {
        "id": 1,
        "wp_name": "ONZE Technologies (Latlong) - 7th Block Jayanagar, Bangalore",
        "category_id": 270,
        "is_routeable": true,
        "way_point": {
            "id": 240090126,
            "phone_no": "+918026712175",
            "email_id": "",
            "address": "#l/B-48, Jaylakshmi Arcade, 27th Cross Road, 7th Block, Jayanagar, Bengaluru - 560070",
            "geofeature": {
                "geoproperty": "POINT (77.5783206 12.9306361)"
            }
        },
        "store_timings": null
    }
]
```

This endpoint returns all the stores for customer along with its details and geo property.


### HTTP Request
`GET https://api.latlong.in/v2/brands/[brand_id]/stores.json`
####  example
`GET https://api.latlong.in/v2/brands/24/stores.json`

### Query Parameters

Parameter | Type | Presence | Description
--------- | ---- | -------- | -----------
brand_id | integer | must | registered brand id from latlong
category_id | integer | optional | category id of registered brand

<aside class="notice">
  you must add your <code>access_token</code> with all API request
</aside>

<aside class="success">
200 — Store search and related info successfully retrieved.
</aside>

## Store Count - State level

```ruby
require 'rest-client'
response = RestClient.get "https://api.latlong.in/v2/brands/[brand_id]/counts.json"
```

```shell
curl https://api.latlong.in/v2/brands/[brand_id]/counts.json? -H 'Authorization: Bearer <ACCESS_TOKEN>'
```

```javascript
https://api.latlong.in/v2/brands/[brand_id]/counts.json?
```

```java
// Java code goes here

// Use any of the http client library for fetching rest service data
okhttp   //(http://square.github.io/okhttp/)
retrofit //(http://square.github.io/retrofit/)

// Or Use Standard java libraries like 
JAX-RS   //(http://docs.jboss.org/resteasy/docs/3.0.16.Final/userguide/html/RESTEasy_Client_Framework.html)
jersey   //(https://jersey.java.net/documentation/latest/client.html)
```

> The above API returns JSON structured like this:

```json
{
    "total_count": 1,
    "state_count": [
        {
            "state": "Karnataka",
            "count": 1
        }
    ]
}
```

This endpoint returns all stores count along with state level store counts.

### HTTP Request
`GET https://api.latlong.in/v2/brands/[brand_id]/counts.json`
####  example
`GET https://api.latlong.in/v2/brands/[brand_id]/counts.json?category_id=12`

### Query Parameters

Parameter | Type | Presence | Description
--------- | ---- | -------- | -----------
brand_id | integer | must | registered brand id from latlong
category_id | integer | optional | category id of registered brand

<aside class="notice">
  you must add your <code>access_token</code> with all API request
</aside>
<aside class="success">
200 — Store search and related info successfully retrieved.
</aside>

#Direction

## Search Landmarks

```ruby
require 'rest-client'
response = RestClient.get "https://api.latlong.in/v2/search_landmarks.json", {
  params: {:lat => 12.9306361, :lon => 77.5783206}
}
```

```shell
curl https://api.latlong.in/v2/search_landmarks.json?lat=12.9306361&lon=77.5783206 -H 'Authorization: Bearer <ACCESS_TOKEN>'
```

```javascript
https://api.latlong.in/v2/search_landmarks.json?lat=12.9306361&lon=77.5783206
```

```java
// Java code goes here

// Use any of the http client library for fetching rest service data
okhttp   //(http://square.github.io/okhttp/)
retrofit //(http://square.github.io/retrofit/)

// Or Use Standard java libraries like 
JAX-RS   //(http://docs.jboss.org/resteasy/docs/3.0.16.Final/userguide/html/RESTEasy_Client_Framework.html)
jersey   //(https://jersey.java.net/documentation/latest/client.html)
```

> The above API returns JSON structured like this:

```json
[
    {
        "name": "Jayanagar Shopping Complex;Jayanagar 4th Block Shopping Complex;Jayanagar BDA Shopping Complex",
        "id": 240031566,
        "geofeature": {
            "geoproperty": "POINT (77.5839042663574 12.9287518923715)"
        }
    },
    {
        "name": "Jaynagar 3rd Block ICICI Bank Circle;3rd Block ICICI Bank Signal",
        "id": 1710000181,
        "geofeature": {
            "geoproperty": "POINT (77.58393438562915 12.93292469256794)"
        }
    },
    {
        "name": "Nettakallappa Circle",
        "id": 1710000158,
        "geofeature": {
            "geoproperty": "POINT (77.57336945509768 12.9402066771197)"
        }
    },
    {
        "name": "Sangam Circle",
        "id": 1710000006,
        "geofeature": {
            "geoproperty": "POINT (77.57776858850612 12.91743624395743)"
        }
    }
]
```

This endpoint returns the 4 popular landmarks around the given point with its geo property .


### HTTP Request
`https://api.latlong.in/v2/search_landmarks.json`
####  example
`GET https://api.latlong.in/v2/search_landmarks.json?lat=12.9306361&lon=77.5783206`

### Query Parameters

Parameter | Type | Presence | Description
--------- | ---- | -------- | -----------
lat | integer/float | must | Latitude of the location
lon | integer/float | must | Longitude of the location

<aside class="notice">
  you must add your <code>access_token</code> with all API request
</aside>
<aside class="success">
200 — Store search and related info successfully retrieved.
</aside>

## Get Direction

```ruby
require 'rest-client'
response = RestClient.get "https://api.latlong.in/v2/directions.json", {
  params: {:type => 1, :from => 240031566, :to => 240090126}
}
```

```shell
curl https://api.latlong.in/v2/directions.json?type=1&from=240031566&to=240090126 -H 'Authorization: Bearer <ACCESS_TOKEN>'
```

```javascript
https://api.latlong.in/v2/directions.json?type=1&from=240031566&to=240090126
```

```java
// Java code goes here

// Use any of the http client library for fetching rest service data
okhttp   //(http://square.github.io/okhttp/)
retrofit //(http://square.github.io/retrofit/)

// Or Use Standard java libraries like 
JAX-RS   //(http://docs.jboss.org/resteasy/docs/3.0.16.Final/userguide/html/RESTEasy_Client_Framework.html)
jersey   //(https://jersey.java.net/documentation/latest/client.html)
```

> The above API returns JSON structured like this:

```json
{
    "from_name": "Jayanagar Shopping Complex",
    "to_name": "Latlong - Onze Technologies (I) Pvt Ltd.",
    "distance": 0.828,
    "from_point": {
        "lat": 12.9287518923715,
        "long": 77.5839042663574
    },
    "to_point": {
        "lat": 12.9306361,
        "long": 77.5783206
    },
    "hint_count": 5,
    "hints": [
        "START-Jayangr Shopping Cmplx ON RIGHT\n",
        "GO ON 9th Main Road TOWARDS Jaynagar 3rd Block ICICI Bank Circle,GO 0.2K\n",
        ...
    ],
    "points": [
        {
            "lat": 12.9287518923715,
            "long": 77.58383
        },
        ...
    ]
}
```

This endpoint returns driving direction coordinates and hints from given source to destination .


### HTTP Request
`GET https://api.latlong.in/v2/directions.json`
####  example
`GET https://api.latlong.in/v2/directions.json?type=1&from=240031566&to=240090126`

### Query Parameters

Parameter | Type | Presence | Description
--------- | ---- | -------- | -----------
type | integer | must | Type of source and destination given
from | integer/float/text | must | Source location
to | integer/float/text | must | destination location

Type values : 

1 - Direction from geoid to geoid <br/>
2 - Direction from place to place<br/>
3 - Direction from geo point to geo point<br/>
4 - Direction from geo point to geo id<br/>
5 - Direction from geo id to geo point<br/>
6 - Direction from geo point to place<br/>
7 - Direction from place to geo point<br/>
8 - Direction from geo id to place<br/>
9 - Direction from place to geo id<br/>

<aside class="notice">
  you must add your <code>access_token</code> with all API request
</aside>
<aside class="success">
200 — Store search and related info successfully retrieved.
</aside>

## PgRoute
```ruby
require 'rest-client'
response = RestClient.get "https://api.latlong.in/v2/route.json", {
  params: {:source => 670000042, :target => 670000039}
}
```

```shell
curl https://api.latlong.in/v2/route.json?source=670000042&target=670000039 -H 'Authorization: Bearer <ACCESS_TOKEN>'
```

```javascript
https://api.latlong.in/v2/route.json?source=670000042&target=670000039
```

```java
// Java code goes here

// Use any of the http client library for fetching rest service data
okhttp   //(http://square.github.io/okhttp/)
retrofit //(http://square.github.io/retrofit/)

// Or Use Standard java libraries like 
JAX-RS   //(http://docs.jboss.org/resteasy/docs/3.0.16.Final/userguide/html/RESTEasy_Client_Framework.html)
jersey   //(https://jersey.java.net/documentation/latest/client.html)
```

> The above API returns JSON structured like this:

```json
{
    "route": true,
    "distance": 6818,
    "coordinates": [
        "LINESTRING(77.5383936945382 12.9730498638944,77.5382105723534 12.9728945444162,77.5378891920946 12.9725533100707)",
        "LINESTRING(77.5383936945382 12.9730498638944,77.5386210531133 12.972976822418)",
        "LINESTRING(77.5386210531133 12.972976822418,77.5387239786652 12.9728577044917)",
        ...
    ]
}
```

This endpoint returns the driving direction with distance from start to end point.


### HTTP Request
`GET https://api.latlong.in/v2/route.json`
####  example
`GET https://api.latlong.in/v2/route.json?source=670000042&target=670000039`

### Query Parameters

Parameter | Type | Presence | Description
--------- | ---- | -------- | -----------
source | integer | must | latlong's unique id for source location
target | integer | must | latlong's unique id for destination location

<aside class="notice">
  you must add your <code>access_token</code> with all API request
</aside>

<aside class="success">
200 — Store search and related info successfully retrieved.
</aside>

#SMS

## Send OTP

```ruby
require 'rest-client'
response = RestClient.get "https://api.latlong.in/v2/otp.json", {
  params: {:mobile_number => 1234567890}
}
```

```shell
curl https://api.latlong.in/v2/otp.json?mobile_number=1234567890 -H 'Authorization: Bearer <ACCESS_TOKEN>'
```

```javascript
https://api.latlong.in/v2/otp.json?mobile_number=1234567890
```

```java
// Java code goes here

// Use any of the http client library for fetching rest service data
okhttp   //(http://square.github.io/okhttp/)
retrofit //(http://square.github.io/retrofit/)

// Or Use Standard java libraries like 
JAX-RS   //(http://docs.jboss.org/resteasy/docs/3.0.16.Final/userguide/html/RESTEasy_Client_Framework.html)
jersey   //(https://jersey.java.net/documentation/latest/client.html)
```

> The above API returns JSON structured like this:

```json
{
    "message": "OTP sent"
}
```

This endpoint sends the otp to the user mobile number .


### HTTP Request
`https://api.latlong.in/v2/otp.json`
####  example
`GET https://api.latlong.in/v2/otp.json?mobile_number=1234567890`

### Query Parameters

Parameter | Type | Presence | Description
--------- | ---- | -------- | -----------
mobile_number | integer | must | Users mobile number

<aside class="notice">
  you must add your <code>access_token</code> with all API request
</aside>
<aside class="success">
200 — Store search and related info successfully retrieved.
</aside>

## Send SMS response
```ruby
require 'rest-client'
response = RestClient.get "https://api.latlong.in/v2/brands/[brand_id]/stores/[store_id]/send_sms.json", {
  params: {:mobile_number => 1234567890}
}
```

```shell
curl https://api.latlong.in/v2/brands/[brand_id]/stores/[store_id]/send_sms.json?mobile_number=1234567890 -H 'Authorization: Bearer <ACCESS_TOKEN>'
```

```javascript
https://api.latlong.in/v2/brands/[brand_id]/stores/[store_id]/send_sms.json?mobile_number=1234567890
```

```java
// Java code goes here

// Use any of the http client library for fetching rest service data
okhttp   //(http://square.github.io/okhttp/)
retrofit //(http://square.github.io/retrofit/)

// Or Use Standard java libraries like 
JAX-RS   //(http://docs.jboss.org/resteasy/docs/3.0.16.Final/userguide/html/RESTEasy_Client_Framework.html)
jersey   //(https://jersey.java.net/documentation/latest/client.html)
```

> The above API returns JSON structured like this:

```json
{
    "Message": "Message sent successfully"
}
```

This endpoint sends the store details as a message to user mobile number.


### HTTP Request
`GET https://api.latlong.in/v2/brands/[brand_id]/stores/[store_id]/send_sms.json`
####  example
`GET https://api.latlong.in/v2/brands/[brand_id]/stores/[store_id]/send_sms.json?mobile_number=1234567890`

### Query Parameters

Parameter | Type | Presence | Description
--------- | ---- | -------- | -----------
brand_id | integer | must | registered brand id from latlong
store_id | integer | must | store id of registered brand
mobile_number | integer | must | User's mobile number

<aside class="notice">
  you must add your <code>access_token</code> with all API request
</aside>

<aside class="success">
200 — Store search and related info successfully retrieved.
</aside>