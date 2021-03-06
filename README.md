# Welcome

This guide is oriented to developers who want to start integrating against our core API in our testing environment. 

We expose our core resources as RESTful API. All responses are serialised in JSON format. 

Generally spaking GET verbs dont require authentication. On the other hand, any POST, PUT or DELETE will require the request to be authenticated via JWT token. 

# Getting started

Events always have a Place associated with it. We support queries on both. 
Places can have Promotions. Events, on the other hand, can have both Promotions and Tickets.
Vouchers can be claimed against Promotions.

# Sign UP

To start managing your Events, Places, Tickets, Promotions and Vouchers you need to [Create an account](https://test.havefunhub.com/tickets.html ) 

Then [Login to Console](https://test.organiser.havefunhub.com) to generate a token to use in your requests when needed.

# Documentation
Go to our [API Explorer](https://test.havefunhub.com/api-doc)

Additional information about parameters [in this guide](https://docs.google.com/document/d/1IaTtZkc7Y9mAsOTxDUIZ0FlKQ-VBZX59RMI1nUAbOMI)

### Events
Replace {eventId} by your current id; for example 30, and {username} for your current username for example Gary.
#### GET
The below code will show events that are happening at any time (string):
```javascript
curl -XGET "https://test.havefunhub.com/api/events/query?when=any"
```

The below code will show you all events:
```javascript
curl -XGET  "https://test.havefunhub.com/api/events/query"
```
The below code will show you events you made (string):
```javascript
curl -XGET "https://test.havefunhub.com/api/events/query?user={username}"
```
The below code will show all events wth promos linked to them (boolean):
```javascript
curl -XGET "https://test.havefunhub.com/api/users/query?hasPromo=true"
```
The below code will show you all events without promo linked to them (boolean):
```javascript
curl -XGET "https://test.havefunhub.com/api/users/query?hasPromo=false"
```
The below code will show you all events with a certain keyword in them (string):
```javascript
curl -XGET "https://test.havefunhub.com/api/events/query?q=party"
```
The below code will show you events within a certain distance (km) from a chosen long and lat position (decimal):
```javascript
curl -XGET "https://test.havefunhub.com/api/events/query?Lat=51.5487&Long=67.243456&Dist=10"
```
Use the below code to find tickets linked to a certain event:
```javascript
curl -XGET "https://test.havefunhub.com/api/event/{eventId}/tickets"
```

Use the below code to find a promo linked to an event:
```javascript
curl -XGET "https://test.havefunhub.com/api/event/{eventID}/promos"
```
#### POST
The code below wll create an event. The -H parameter is passing **X-AUTH-TOKEN** as a header. Reaplce *Token_to_be_replaced* by your actual token. Check [this guide to generate yours](https://docs.google.com/document/d/1IaTtZkc7Y9mAsOTxDUIZ0FlKQ-VBZX59RMI1nUAbOMI)
```javascript
curl -XPOST  -v -H "X-AUTH-TOKEN:Token_to_be_replaced" "https://test.havefunhub.com/services/events" -H "Content-Type: application/json"  -d '{"placeId":{placeID},"start":"2018-08-09T10:00:00+0000","description":"fun for all","phone":"01373 813 721","name":"enter_name_of_event","category": "Disco", "end":"2018-08-09T23:00:00+0000"}'
```
#### PUT
The below code will edit an event MAKE SURE YOU ENTER A TOKEN (strings:
```javascript
curl -XPUT  -v -H "X-AUTH-TOKEN:Enter_token_here" "https://test.havefunhub.com/services/event/{eventID}" -H "Content-Type: application/json"  -d '{"hasPromo":true,"placeId":Info_to_be_changed,"start":"2018-08-09T10:00:00+0000","description":"Annual village get together with drinks and music\n","userName":"Your_username","funIndicator":0,"phone":"Info_to_be_changed","name":"Info_to_be_changed","end":"2018-08-09T23:00:00+0000","place":{"country":"United Kingdom","address":"Info_to_be_changed","city":"Info_to_be_changed","hasPromo":false,"latitude":51.508530,"placeId":{placeID},"active":true,"description":"Mells barn","priceIndicator":0,"userName":"Your_username","phone":"Info_to_be_changed","name":"Info_to_be_changed","category":" #Disco","longitude": -0.076132},"category":" #Disco","checkins":0}'
```
#### DELETE
The below code will delete an event MAKE SURE YOU ENTER A TOKEN:
```javascript
curl -XDELETE  -v -H "X-AUTH-TOKEN:Your_token_here" "https://test.havefunhub.com/services/event/{eventID}" -H "Content-Type: application/json"  
```
### Places
Replace {placeID} for your id for example 33, also replace {username} for your username for example Tim.
#### GET
The below code will show you all places:
 ```javascript
 curl -XGET "https://test.havefunhub.com/api/places/query"
 ```
 The below code will find you places you made (string):
```javascript
curl -XGET "https://test.havefunhub.com/api/places/query?user={username}"
 ```
 The below code will find you all places with promos linked to them (boolean):
 ```javascript
 curl -XGET "https://test.havefunhub.com/api/places/query?hasPromo=true"
 ```
 The below code will find you all locations with a chosen keyword (string):
 ```javascript
 curl -XGET "https://test.havefunhub.com/api/places/query?q=town"
```
 The below code will find you any locations within a give dstance(km) around a point of long and lat (decimals):
```javascript
curl -XGET "https://test.havefunhub.com/api/places/query?Lat=23.234534&Long=-21.24435&Dist=1000"
```
Use the below code to find a promo linked to a place:
```javascript
curl -XGET "https://test.havefunhub.com/api/place/{placeID}/promos"
```
#### POST
The below code will create a place MAKE SURE YOU ENTER A TOKEN (strings):
```javascript
curl -XPOST  -v -H "X-AUTH-TOKEN: token_to_be_replaced" "https://test.havefunhub.com/services/places" -H "Content-Type: application/json"  -d '{"name":"Info_to_be_replaced","description":"Info_to_be_replaced","category":"Info_to_be_replaced","priceIndicator":0,"address":"Info_to_be_replaced"}’,"address2":"Info_to_be_replaced","postCode":"Info_to_be_replaced","city":"Info_to_be_replaced","latitude":51.508530"longitude":-0.076132"country":"England","Phone": "Info_to_be_replaced"}'
```
#### PUT
The below code will edit a place MAKE SURE YOU ENTER A TOKEN (strings):
```javascript
curl -XPUT  -v -H "X-AUTH-TOKEN:Insert_token_here" "https://test.havefunhub.com/services/place/{placeID}" -H "Content-Type: application/json"  -d '{"name":"Info_to_be_changed","description":"Info_to_be_changed","category":" #Bar","priceIndicator":0,"address":"Info_to_be_changed","address2":"Info_to_be_changed","postCode":"Info_to_be_changed","city":"Info_to_be_changed","latitude":51.508530,"longitude":-0.076132,"active":true,"hasPromo":false,"country":"Info_to_be_changed","phone":null,"userName":"Your_username"}'
```
#### DELETE
The below code will delete a place MAKE SURE YOU ENTER A TOKEN (integer):
```javascript
curl -XDELETE  -v -H "X-AUTH-TOKEN: " "https://test.havefunhub.com/services/place/{placeID}" -H "Content-Type: application/json"
```





## javascript

Check our [API explorer](https://test.havefunhub.com/api-doc) for the available end points. You can consume services from your any client.
```javascript
$.ajax({
  url: 'https://test.havefunhub.com/api/events/query',
  dataType: "json",
  ...
  success: function (data) {
                  //do something with Events' JSON result
           }
})
```
## Java API

Soon. Working on it :) 

### Requirements

Java 1.7 or later

### Installation

#### Maven users

Add this dependency to your project's POM:

```xml
<dependency>
  <groupId>com.druidalabs</groupId>
  <artifactId>havefunhub-api</artifactId>
  <version>3.0.0</version>
</dependency>
```
### Documentation

Please see the [Java API docs](http://druidalabs.com) for the most up-to-date documentation.

### Usage

HaveFunHubExample.java

```java
import java.util.HashMap;
import java.util.Map;

public class HaveFunHubExample {

    public static void main(String[] args) {
        RequestOptions requestOptions = (new RequestOptionsBuilder()).setApiKey("YOUR-SECRET-KEY").build();
        Map<String, Object> eventsMap = new HashMap<String, Object>();
        eventsMap.put("Lat", 34.6037); 
        eventsMap.put("Long", 58.3816);
        eventsMap.put("when", "now");
        try {
            ArrayList<Event> events = Event.query(eventsMap, requestOptions);
            System.out.println(events);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Entities
### Events
### Places
### Promotions
### Tickets
