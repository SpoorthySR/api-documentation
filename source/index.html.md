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





# Search

## Store search within location

```ruby
require 'rest-client'
response = RestClient.get "https://api.latlong.in/v2/brands/[brand_id]/newsearch.json", {
        params: {:query => 'bengaluru'}
      }
```

```shell
curl https://api.latlong.in/v2/brands/[brand_id]/newsearch.json?query=bengaluru -H 'Authorization: Bearer <ACCESS_TOKEN>'
```

```javascript
https://api.latlong.in/v2/brands/[brand_id]/newsearch.json?query=bengaluru
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
  "count": 1,
  "stores": [
            {
              "id": 1,
              "wp_name": "ONZE Technologies (Latlong) - Banashankari 2nd Stage, Bangalore",
              "category_id": 270,
              "distance": 0,
              "is_routeable": true,
              "way_point": {
                  "id": 240090126,
                  "phone_no": "+918026712175",
                  "email_id": null,
                  "address": "​#1757/A, 1st Floor, 34th Cross, Banashankari 2nd Stage, Bangalore - 5600701",
                  "geofeature": {
                      "geoproperty": "POINT (77.5663626194 12.9186399138545)"
                      }
                  },
              "store_timings": "Monday - Friday, 9 AM - 6 PM"
            }
          ]
}
```

This endpoint returns stores within entered location along with geo property of the entered location and count of stores found within entered location.


### HTTP Request
`GET https://api.latlong.in/v2/brands/[brand_id]/newsearch.json`
####  example
`GET https://api.latlong.in/v2/brands/[brand_id]/newsearch.json?query=bengaluru`

### Using latlong's unique location id for faster search
API works faster with latlong's unique geofeature id returned from autocomplete API for interested location name.
####  example
`GET https://api.latlong.in/v2/brands/[brand_id]/newsearch.json?geofeature=510000021`

### Query Parameters

Parameter | Type | Presence | Description
--------- | ---- | -------- | -----------
brand_id | integer | must | registered brand id from latlong
query | string | must | location name where stores to be searched
category | integer | optional | category id of registered brand
geofeature | integer | optional | latlong's unique id for location

<aside class="notice">
  you must add your <code>access_token</code> with all API request
</aside>
<aside class="success">
200 — Store search and related info successfully retrieved.
</aside>

## Store search around geo point

```ruby
require 'rest-client'
response = RestClient.get "https://api.latlong.in/v2/brands/[brand_id]/stores_around_me.json", {
        params: {:lat => 12.976182 ,:lon => 77.570901}
      }
```

```shell
curl https://api.latlong.in/v2/brands/[brand_id]/stores_around_me.json?lat=12.976182&lon=77.570901 -H 'Authorization: Bearer <ACCESS_TOKEN>'
```

```javascript
https://api.latlong.in/v2/brands/[brand_id]/stores_around_me.json?lat=12.976182&lon=77.570901
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
  "stores": [
            {
              "id": 1,
              "wp_name": "ONZE Technologies (Latlong) - Banashankari 2nd Stage, Bangalore",
              "category_id": 270,
              "distance": 6.42,
              "is_routeable": true,
              "way_point": {
                  "id": 240090126,
                  "phone_no": "+918026712175",
                  "email_id": null,
                  "address": "​#1757/A, 1st Floor, 34th Cross, Banashankari 2nd Stage, Bangalore - 5600701",
                  "geofeature": {
                      "geoproperty": "POINT (77.5663626194 12.9186399138545)"
                      }
                  },
              "store_timings": "Monday - Friday, 9 AM - 6 PM"
            }
          ]
}
```

This endpoint returns 10 stores around given geo point (lattitude and longitude). Store list is sorted based on distance from given location to the given point.


### HTTP Request
`GET https://api.latlong.in/v2/brands/[brand_id]/stores_around_me.json`
####  example
`GET https://api.latlong.in/v2/brands/[brand_id]/stores_around_me.json?lat=12.976182&lon=77.570901`

### Query Parameters

Parameter | Type | Presence | Description
--------- | ---- | -------- | -----------
brand_id | integer | must | registered brand id from latlong
lat | integer/float | must | lattitude of location
lon | integer/float | must | longitude of location

<aside class="notice">
  you must add your <code>access_token</code> with all API request
</aside>

<aside class="success">
200 — Store search and related info successfully retrieved.
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

# Store places
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
    	},
    	{
      		"state": "Bihar",
      		"cities": [
        				"Gaya",
        				"Muzaffarpur",
        				"Patna"
      					]
    	},
    	{
      		"state": "Chhattisgarh",
      		"cities": [
        				"Bhilai",
        				"Bilaspur",
        				"Durg",
        				"Jagdalpur",
        				"Korba",
        				"Raigarh",
        				"Raipur"
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
	