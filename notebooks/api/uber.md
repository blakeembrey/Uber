---
site: https://anypoint.mulesoft.com/apiplatform/popular/admin/#/dashboard/apis/7782/versions/7918/portal/pages/6523/edit
apiNotebookVersion: 1.1.66
title: Gists
---

```javascript
load('https://github.com/chaijs/chai/releases/download/1.9.0/chai.js')
```

See http://chaijs.com/guide/styles/ for assertion styles

```javascript
assert = chai.assert
```

```javascript

API.createClient('client', '#REF_TAG_DEFENITION');
```

```javascript
clientId = prompt("Please, enter your Client ID")
clientSecret = prompt("Please, enter your Client Secret")
```

```javascript
API.authenticate(client,"oauth_2_0",{
  clientId: clientId,
  clientSecret: clientSecret
})
```
The Products endpoint returns information about the Uber products offered at a given location. The response includes the display name and other details about each product, and lists the products in the proper display order.

Some Products, such as experiments or promotions such as UberPOOL and UberFRESH, will not be returned by this endpoint.

```javascript
productsResponse = client.products.get({}, {
  "latitude": "latitudeValue",
  "longitude": "longitudeValue"
})
```

```javascript
assert.equal( productsResponse.status, 200 )
```

Returns information about the Uber product.
```javascript
productIdResponse = client.products.product_id("product_idValue").get()
```

```javascript
assert.equal( productIdResponse.status, 200 )
```
The Price Estimates endpoint returns an estimated price range for each product offered at a given location. The price estimate is provided as a formatted string with the full price range and the localized currency symbol.

The response also includes low and high estimates, and the ISO 4217 currency code for situations requiring currency conversion. When surge is active for a particular product, its surge_multiplier will be greater than 1, but the price estimate already factors in this multiplier.

```javascript
priceResponse = client.estimates.price.get({}, {
  "end_latitude": "end_latitudeValue",
  "end_longitude": "end_longitudeValue",
  "start_latitude": "start_latitudeValue",
  "start_longitude": "start_longitudeValue"
})
```

```javascript
assert.equal( priceResponse.status, 200 )
```

The Time Estimates endpoint returns ETAs for all products offered at a given location, with the responses expressed as integers in seconds. We recommend that this endpoint be called every minute to provide the most accurate, up-to-date ETAs.
```javascript
timeResponse = client.estimates.time.get({}, {
  "start_latitude": "start_latitudeValue",
  "start_longitude": "start_longitudeValue"
})
```

```javascript
assert.equal( timeResponse.status, 200 )
```
The Promotions endpoint returns information about the promotion that will be available to a new user based on their activity's location. These promotions do not apply for existing users.
```javascript
promotionsResponse = client.promotions.get({}, {
  "end_latitude": "end_latitudeValue",
  "end_longitude": "end_longitudeValue",
  "start_latitude": "start_latitudeValue",
  "start_longitude": "start_longitudeValue"
})
```

```javascript
assert.equal( promotionsResponse.status, 200 )
```
The User Profile endpoint returns information about the Uber user that has authorized with the application.
```javascript
meResponse = client.me.get()
```

```javascript
assert.equal( meResponse.status, 200 )
```
The Request endpoint allows a ride to be requested on behalf of an Uber user given their desired product, start, and end locations.
```javascript
requestsCreateResponse = client.requests.post({}, {
  "product_id": "product_idValue",
  "end_latitude": "end_latitudeValue",
  "end_longitude": "end_longitudeValue",
  "start_latitude": "start_latitudeValue",
  "start_longitude": "start_longitudeValue"
})
```

```javascript
assert.equal( requestsCreateResponse.status, 200 )
```

Get the real time status of an ongoing trip that was created using the Ride Request endpoint.
```javascript
requestIdResponse = client.requests.request_id("request_idValue").get()
```

```javascript
assert.equal( requestIdResponse.status, 200 )
```

Get the receipt information of the completed request.
```javascript
receiptResponse = client.requests.request_id("request_idValue").receipt.get()
```

```javascript
assert.equal( receiptResponse.status, 200 )
```

Get a map with a visual representation of a Request.
```javascript
mapResponse = client.requests.request_id("request_idValue").map.get()
```

```javascript
assert.equal( mapResponse.status, 200 )
```

Cancel an ongoing Request on behalf of a rider.
```javascript
requestIdDeleteResponse = client.requests.request_id("request_idValue").delete()
```

```javascript
assert.equal( requestIdDeleteResponse.status, 200 )
```

The Request Estimate endpoint allows a ride to be estimated given the desired product, start, and end locations. If the end location is not provided, only the pickup ETA and details of surge pricing information are provided. If the pickup ETA is null, there are no cars available, but an estimate may still be given to the user.

You can use this endpoint to determine if surge pricing is in effect. Do this before attempting to make a request so that you can preemptively have a user confirm surge by sending them to the surge_confirmation_href provided in the response.

```javascript
estimateCreateResponse = client.requests.estimate.post({}, {
  "product_id": "product_idValue",
  "start_latitude": "start_latitudeValue",
  "start_longitude": "start_longitudeValue"
})
```

```javascript
assert.equal( estimateCreateResponse.status, 200 )
```