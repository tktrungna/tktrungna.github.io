---
title: "API Design"
date: 2024-01-10
---

# API Design
## Top 6 most popular API Architecture Styles
* SOAP
* RESTful (API with REST style)
* GraphQL
* gRPC (morden implementation of RPC)
* Websocket
* Webhook
Need to check SSE too

[<img src="https://img.youtube.com/vi/4vLxWqE94l4/maxresdefault.jpg" width="50%" height="50%">](http://www.youtube.com/watch?v=4vLxWqE94l4&ab_channel=ByteByteGo)

<img src="https://res.cloudinary.com/practicaldev/image/fetch/s--OFer-8Eq--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_800/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/um3l02jna0u8xhii9cde.png" width="50%" height="50%">

### RPC and REST calls comparison

| Operation | RPC | REST |
|---|---|---|
| Signup    | **POST** /signup | **POST** /persons |
| Resign    | **POST** /resign<br/>{<br/>"personid": "1234"<br/>} | **DELETE** /persons/1234 |
| Read a person | **GET** /readPerson?personid=1234 | **GET** /persons/1234 |
| Read a person’s items list | **GET** /readUsersItemsList?personid=1234 | **GET** /persons/1234/items |
| Add an item to a person’s items | **POST** /addItemToUsersItemsList<br/>{<br/>"personid": "1234";<br/>"itemid": "456"<br/>} | **POST** /persons/1234/items<br/>{<br/>"itemid": "456"<br/>} |
| Update an item    | **POST** /modifyItem<br/>{<br/>"itemid": "456";<br/>"key": "value"<br/>} | **PUT** /items/456<br/>{<br/>"key": "value"<br/>} |
| Delete an item | **POST** /removeItem<br/>{<br/>"itemid": "456"<br/>} | **DELETE** /items/456 |

<p align="center">
  <i><a href=https://apihandyman.io/do-you-really-know-why-you-prefer-rest-over-rpc/>Source: Do you really know why you prefer REST over RPC</a></i>
</p>

## Idempotent API
Api could be un-robust and un-predictable due to un-reliable networks and server (more reliable) may still fail. To solve that, we need to design APIs that
* Client retries to ensure consistency
* Retry with idempotency and idempotency keys to allow clients to pass a unique value
* Retry with exponential backoff and random jitter
Example with Stripe API
```
curl https://api.stripe.com/v1/customers \
  -u sk_test_4eC39HqLyjWDarjtT1zdp7dc: \
  -H "Idempotency-Key: KG5LxwFBepaKHyUD" \
  -d description="My First Test Customer (created for API docs at https://www.stripe.com/docs/api)"
```

## Reference
* [Top 6 Most Popular API Architecture Styles with Pros, Cons, and Use Cases](https://dev.to/kanani_nirav/top-6-most-popular-api-architecture-styles-you-need-to-know-with-pros-cons-and-use-cases-564j)
* [Do you really know why you prefer REST over RPC](https://apihandyman.io/do-you-really-know-why-you-prefer-rest-over-rpc/) 
  * resource vs operation request style, predictability and semantic
* [Learn REST: A RESTful Tutorial](https://restapitutorial.com/index.html)
  * [HTTP Status Codes](https://www.restapitutorial.com/httpstatuscodes.html)
* [When are RPC-ish approaches more appropriate than REST?](http://programmers.stackexchange.com/a/181186)
  * Tight coupling, reliable communication, uniform language
  * [JSON-RPC](https://www.wallarm.com/what/what-is-json-rpc#json__what_is_it_and_how_it_works__) allows for more expressive, less cumbersome API design
* [REST vs JSON-RPC](http://stackoverflow.com/questions/15056878/rest-vs-json-rpc)
  * The fundamental problem with RPC is coupling
  * REST style is very easy to guide clients by including control information in representation
* [Debunking the myths of RPC and REST](http://etherealbits.com/2012/12/debunking-the-myths-of-rpc-rest/)
* [What are the drawbacks of using REST](https://www.quora.com/What-are-the-drawbacks-of-using-RESTful-APIs)
* [Thrift](https://code.facebook.com/posts/1468950976659943/) a cross-language framework for handling RPC, including serialization/deserialization, protocol transport, and server creation
* [Why REST for internal use and not RPC](http://arstechnica.com/civis/viewtopic.php?t=1190508)
* [RPC vs REST](https://imtien.com/software-development/rpc-vs-rest/)
* [Designing robust and predictable APIs with idempotency](https://stripe.com/blog/idempotency)
* [Idempotency and retries with stripe-python](https://www.youtube.com/watch?v=y0ONKsP1LkU&t=17s&ab_channel=StripeDevelopers)