
# Smarter HTTP API  (HAPI?)
a better way to do network APIs like HTTP/REST

## Philosophy
* HTTP endpoints should be like function calls
* A function call has a name, some parameters (optional) and some return value.
* HTTP endpoints should be like functions calls.
* HTTP endpoints therefore should have a name, some parameters and some return value.
* WE don't care about CRUD. CRUD is the easiest shit in the world to do so we shouldn't base our protocol on making CRUD easier.
* The client should be as dumb as possible about what's going on.  It doesn't need to know whether state is changing or not (it is, always) only what it needs to send and receive, if anything.  
* Duplicating endpoints for CREATE and UPDATE that do almost the same thing (save a record) is fucking retarded.  But if you want to you need to.  
* Functions are often namespaced. 
* HTTP endpoints can be namespaced.  
* POST, PUT, PATCH, whaaat???  Fuck VERBS. Any request may return data and/or change state on the server, because that's how things really are in the real world.  The verb is your function name.  We don't need the function name in a request header (verb) and in the URL.  Remember DRY?

## Structure
* The URL is the function name with an optional namespace. 
* The request payload (JSON, XML, etc.) is the parameters.
* The response payload is the function result.
* Always use POST.  Because verbs in two places is goddamn stupid.  


## Examples:

### Find One Existing order:
URL: https://example.com/api/orders/find-one
Request: {"id": 1234}
Response: {"id": 1234, "customer": {"id": 234, "Bob SMith"}}

### Find all orders via a query:
URL: https://example.com/api/orders/find-all
Request: { "sort": "ASC", "maxResult": 25, "customerId": 456}
Response: [{"id": 1234, "customer": {"id": 234, "Bob SMith"}}]


### Save a new order:
URL: https://example.com/api/orders/save
Request: { "customer": {"name": "Bob Smith", "address": "234 Brecken St."}, "orderLines": [{"productId": 555, "quantity": 3}] }
Response: { "id": 1122, "customer": {"name": "Bob Smith", "address": "234 Brecken St."}, "orderLines": [{"productId": 555, "quantity": 3}] }


### Save an EXISTING order
URL: https://example.com/api/orders/save
Request: { "id": 1122, "customer": {"name": "Bob L. Smith", "address": "234 Brecken St."}, "orderLines": [{"productId": 555, "quantity": 3}] }
Response: { "id": 1122, "customer": {"name": "Bob L. Smith", "address": "234 Brecken St."}, "orderLines": [{"productId": 555, "quantity": 3}] }

### Delete an order
URL:  https://example.com/api/orders/delete
Request: {"id": 4567}
Response: {"id": 4567, "status": "Deleted"}

## Related projects
[Barrister RPC](http://barrister.bitmechanic.com)
[GRPC](http://grpc.io)

## How HAPI Differs From RPC
{{TODO}}
