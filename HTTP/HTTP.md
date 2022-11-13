[HTTP](#http?)

## HTTP ?

* The HTTP protocol is a request/response protocol.
* A client sends a request to the server in the form of a request method, URI, and protocol version, followed by a MIME-like message containing request modifiers, client information, and possible body content over a connection with a server
* The server responds with a status line, including the message's protocol version and a success or error code, followed by a MIME-like message containing server information, entity metainformation, and possible entity-body content
* HTTP communication usually takes place over TCP/IP connections

## Possible HTTP communication

* Simplest case:
  ```
  request chain ----------------------------->
  UA -------------------v------------------- O
  <---------------------------- response chain

  V: Single connection
  UA: User agent
  O: Origin
  ```
* Complex situation:
  ```
  request chain ------------------------------------------->
  UA -----v----- A -----v----- B -----v----- C -----v----- O
  <------------------------------------------ response chain

  A, B, C, D: intermediaries proxies.
  ```
* Cached situation:
  ```
  request chain -------------  >
  UA -----v----- A -----v----- B - - - - - - C - - - - - - O
  <--------- response chain

  Response cached at B proxy. 

  Still caching is experimented.
  ```

## HTTP 1.0 vs HTTP 1.1

In HTTP/1.0, most implementations used a new connection for each request/response exchange.

In HTTP/1.1, a connection may be used for one or more request/response exchanges, although connections may be closed for a variety of reasons.

## HTTP URL

```
"http:" "//" host [ ":" port ] [ abs_path [ "?" query ]]

port:80
```

## HTTP Request

A request message from a client to a server includes, within the first line of that message, the method to be applied to the resource, the identifier of the resource, and the protocol version in use.

```
Request-Line

general-header CLRF
request-header CLRF
entity-header CRLF
CRLF
[ message-body ]
```

general-header = `Cache-Control | Connection | Date | Pragma | Trailer | Transfer-Encoding | Upgrade | Via | Warning`

#### HTTP Methods


| Methods | Purpose                                                                                                                         | Demo                                                           |
| --------- | --------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| OPTIONS | used to get information about the communication options available on the request/response chain identified by the Request-URI   | https://reqbin.com/req/jecm0tqu/options-request-example        |
| GET     | used to retrieve information                                                                                                    | https://reqbin.com/req/ewk2va7p/get-request-to-retrieve-a-json |
| HEAD    | Similar to GET, except it transfers the status line and headers only                                                            | https://reqbin.com/req/gbfchnr8/head-request-example           |
| POST    | Send data to the server, including images, JSON strings, file downloads, etc                                                    | https://reqbin.com/post-online                                 |
| PUT     | Replace or update an existing resource on the server                                                                            | https://reqbin.com/req/p2fujlvb/put-request-example            |
| PATCH   | Partially modify the specified resource on the server. It is faster and requires less resources than the PUT method             | https://reqbin.com/req/6psxhnzo/patch-request-example          |
| DELETE  | Delete a resource from the server                                                                                               | https://reqbin.com/req/cvy4trgb/delete-request-example         |
| TRACE   | It is designed for diagnostic purposes. When used, the web server sends back to the client the exact request that was received. | [NA] https://reqbin.com/Article/HttpTrace                      |
| CONNECT | Establishes two-way communication with the server by creating an HTTP tunnel through a proxy server.                            | [NA] https://reqbin.com/Article/HttpConnect                    |


| Method  | Safe ? | Idempotent ? | Cacheable ? | Can req. have a body ? |
| --------- | -------- | -------------- | ------------- | ------------------------ |
| OPTIONS | yes    | yes          | no          | no                     |
| GET     | yes    | yes          | yes         | yes                    |
| HEAD    | yes    | yes          | yes         | no                     |
| POST    | no     | no           | no          | no                     |
| PUT     | no     | yes          | no          | yes                    |
| DELETE  | no     | yes          | no          | yes                    |
| TRACE   | yes    | yes          | no          | no                     |
| PATCH   | no     | no           | no          | yes                    |
| CONNECT | no     | no           | no          | no                     |

#### Request Header Fields


| Request<br /> Header | Details                                                                                                                         | example                                       |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------- |
| Accept               | used to specify certain media types which are acceptable for the response                                                       | Accept: audio/*; q=0.2, audio/basic           |
| Accept-Charset       | used to indicate what character sets are acceptable for the response                                                            | Accept-Charset: iso-8859-5, unicode-1-1;q=0.8 |
| Accept-Encoding      | similar to Accept, but restricts the content-codings that are acceptable in the response.                                       | Accept-Encoding: compress, gzip               |
| Accept-Language      | similar to Accept, but restricts the set of natural languages that are preferred as a response to the request                   | Accept-Language: da, en-gb;q=0.8, en;q=0.7    |
| Accept-Ranges        | allows the server to indicate its acceptance of range requests for resource                                                     | Accept-Ranges: bytes                          |
| Age                  | conveys the sender's estimate of the amount of time since the response (or its revalidation) was generated at the origin server | "Age" ":" age-value [ 1#range-unit            |

## HTTP response

After receiving and interpreting a request message, a server responds with an HTTP response message.

```
Status-Line
general-header CLRF
response-header CLRF
entity-header CLRF
CRLF
[message-body]
```

#### Response status codes

- 1xx: Informational - Request received, continuing process
- 2xx: Success - The action was successfully received,
  understood, and accepted
- 3xx: Redirection - Further action must be taken in order to
  complete the request
- 4xx: Client Error - The request contains bad syntax or cannot
  be fulfilled
- 5xx: Server Error - The server failed to fulfill an apparently
  valid request

###### Response codes

```
100 :  Continue
101 :  Switching Protocols 

200 :  OK
201 :  Created
202 :  Accepted
203 :  Non-Authoritative Information
204 :  No Content
205 :  Reset Content
206 :  Partial Content

301 :  Moved Permanently
302 :  Found
303 :  See Other
304 :  Not Modified
305 :  Use Proxy
307 :  Temporary Redirect

400 :  Bad Request
401 :  Unauthorized
402 :  Payment Required
403 :  Forbidden
404 :  Not Found
405 :  Method Not Allowed
406 :  Not Acceptable
407 :  Proxy Authentication Required
408 :  Request Time-out
409 :  Conflict
410 :  Gone
411 :  Length Required
412 :  Precondition Failed
413 :  Request Entity Too Large
414 :  Request-URI Too Large
415 :  Unsupported Media Type
416 :  Requested range not satisfiable
417 :  Expectation Failed

500 :  Internal Server Error
501 :  Not Implemented
502 :  Bad Gateway
503 :  Service Unavailable
504 :  Gateway Time-out
505 :  HTTP Version not supported
```

#### Response Header Fields

The response-header fields allow the server to pass additional information about the response which cannot be placed in the Status- Line. These header fields give information about the server and about further access to the resource identified by the Request-URI.

// TODO

Accept-Ranges

Age

ETag
provides the current value of the entity tag for the requested variant

Location

Proxy-Authenticate

Retry-After

Server

Vary

WWW-Authenticate

Except
used to indicate that particular server behaviors are required by the client.
"Expect" ":" 1#expectation
Except: 100-continue

## Entity

Request and Response messages MAY transfer an entity if not otherwise restricted by the request method or response status code. An entity consists of entity-header fields and an entity-body, although some responses will only include the entity-headers.

#### Entity Headers:


| Entity headers   | details                                                                                                                                                               | examples                                                                                                                                                                                           |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Allow            | lists the set of methods supported by the resource identified by the Request-URI                                                                                      | Allow: GET, HEAD, PUT                                                                                                                                                                              |
| Content-Encoding | used as a modifier to the media-type. When present, its value indicates what additional content codings have been applied to the entity-body                          | Content-Encoding: gzip                                                                                                                                                                             |
| Content-Language | describes the natural language(s) of the intended audience for the enclosed entity                                                                                    | Content-Language: de, en                                                                                                                                                                           |
| Content-Length   | indicates the size of the entity-body                                                                                                                                 | d Content-Length: 3495                                                                                                                                                                             |
| Content-Location | used to supply the resource location for the entity enclosed in the message when that entity is accessible from a location separate from the requested resource's URI | "Content-Location" ":"( absoluteURI / relativeURI                                                                                                                                                  |
| Content-MD5      | MD5 digest of the entity-body for the purpose of providing an end-to-end message integrity check (MIC)of the entity-body                                              | "Content-MD5" ":" md5-digest                                                                                                                                                                       |
| Content-Range    | sent with a partial entity-body to specify where in the full entity-body the partial body should be applied.                                                          | The first 500 bytes: bytes 0-499/1234 ----> The second 500 bytes: bytes 500-999/1234 -----> All except for the first 500 bytes: bytes 500-1233/1234 ------> The last 500 bytes:bytes 734-1233/1234 |
| Content-Type     | indicates the media  type of the entity-body sent to the recipient                                                                                                    | Content-Type: text/html; charset=ISO-8859-4                                                                                                                                                        |
| Expires          | date/time after which the response is considered stale                                                                                                                | Expires: Thu, 01 Dec 1994 16:00:00 GMT                                                                                                                                                             |
| Authorization    | The Authorization field value consists of credentials containing the authentication information of the user agent for the realm of the resource requested.            | "Authorization" ":" credentials                                                                                                                                                                    |

## Terminologies:

##### cache

A program's local store of response messages and the subsystem that controls its message storage, retrieval, and deletion. A cache stores cacheable responses in order to reduce the response time and network bandwidth consumption on future, equivalent requests. Any client or server may include a cache, though a cache  cannot be used by a server that is acting as a tunnel.

##### inbound/outbound

Inbound and outbound refer to the request and response paths for messages: "inbound" means "traveling toward the origin server", and "outbound" means "traveling toward the user agent"

#### Idempotent Methods

An HTTP method is idempotent if the intended effect on the server of making a single request is the same as the effect of making several identical requests.

#### Safe Methods

Request methods are considered "safe" if their defined semantics are essentially read-only; i.e., the client does not request, and does not expect, any state change on the origin server as a result of applying a safe method to a target resource.  Likewise, reasonable use of a safe method is not expected to cause any harm, loss of property, or unusual burden on the origin server.

## References and links

1. https://www.ietf.org/rfc/rfc2616.txt
2. To check request and response https://reqbin.com/
3. Resources: https://developer.mozilla.org/en-US/docs/Web/HTTP

## General Header

cache-control
Connection
Date
