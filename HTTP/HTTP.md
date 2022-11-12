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

general-header
request-header
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