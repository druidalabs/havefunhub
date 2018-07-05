# Sign UP

To start managing your Events, Places, Voucher and Tickets you need to [Create an account](https://havefunhub.com/tickets.html ) 

Then [Login to Console](https://organiser.havefunhub.com) to generate a token to use in your requests when needed.

# Rest API

## curl
### events

The below code will show events that are happening at any time:
```javascript
curl -XGET -H "accept: application/json" "https://test.havefunhub.com/api/events/query?when=any"
```

The below code will show you all events:
```javascript
curl -XGET -H "accept: application/json" "https://test.havefunhub.com/api/events/query"
```
The below code will show you events you made:
```javascript
curl -XGET -H "accept: application/json" "https://test.havefunhub.com/api/events/query?user=Gary"
```
The below code will show all events wth promos linked to them:
```javascript
curl -XGET -H "accept: application/json" "https://test.havefunhub.com/api/users/query?hasPromo=true"
```
The below code will show you all events without promo linked to them:
```javascript
curl -XGET -H "accept: application/json" "https://test.havefunhub.com/api/users/query?hasPromo=false"
```
The below code will show you all events with a certain keyword in them:
```javascript
curl -XGET -H "accept: application/json" "https://test.havefunhub.com/api/events/query?q=party"
```
The below code will show you events within a certain distance (km) from a chosen long and lat position:
```javascript
curl -XGET -H "accept: application/json" "https://test.havefunhub.com/api/events/query?Lat=51.5487&Long=67.243456&Dist=10"
```

### places


The below code will show you all places:
 ```javascript
 curl -XGET -H "accept: application/json" "https://test.havefunhub.com/api/places/query"
 ```
 The below code will find you places you made:
```javascript
curl -XGET -H "accept: application/json" "https://test.havefunhub.com/api/places/query?user=Felipe"
 ```
 The below code will find you all places with promos linked to them:
 ```javascript
 curl -XGET -H "accept: application/json" "https://test.havefunhub.com/api/places/query?hasPromo=true"
 ```
 The below code will find you all locations with a chosen keyword:
 ```javascript
 curl -XGET -H "accept: application/json" "https://test.havefunhub.com/api/places/query?q=town"
```
 The below code will find you any locations within a give dstance(km) around a point of long and lat:
```javascript
curl -XGET -H "accept: application/json" "https://test.havefunhub.com/api/places/query?Lat=23.234534&Long=-21.24435&Dist=1000"
```
### Tickets
Use the below code to find tickets linked to a certain event:
```javascript
curl -XGET -H "accept: application/json"  "https://test.havefunhub.com/api/event/30/tickets"
```
### Promo
Use the below code to find a promo linked to an event:
```javascript
curl -XGET -H "accept: application/json"  "https://test.havefunhub.com/api/event/30/promos"
```
Use the below code to find a promo linked to a place:
```javascript
curl -XGET -H "accept: application/json"  "https://test.havefunhub.com/api/place/36/promos"
```

Check our [API explorer](https://havefunhub.com/api-doc) for the available end points. You can consume services from your any client.
```javascript
$.ajax({
  url: 'https://havefunhub.com/api/events/query',
  dataType: "json",
  ...
  success: function (data) {
                  //do something with Events' JSON result
           }
})
```
# Java API

Soon. Working on it :) 

## Requirements

Java 1.7 or later

## Installation

### Maven users

Add this dependency to your project's POM:

```xml
<dependency>
  <groupId>com.druidalabs</groupId>
  <artifactId>havefunhub-api</artifactId>
  <version>3.0.0</version>
</dependency>
```
## Documentation

Please see the [Java API docs](http://druidalabs.com) for the most up-to-date documentation.

## Usage

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
