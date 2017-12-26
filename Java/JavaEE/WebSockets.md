# WebSockets

A solution to the inadequacies of prior web workarounds for asynchronous communication with a server. Before WebSockets, most solutions were resource intensive, used HTTP, awkard workarounds (except for AJAX), and not fully duplex. Whereas WebSockets are:

* Lightweight
* Bidirectional
* Fully duplexed communication

WebSockets are designed to be used by applications that use bidirectional communication, such as chat apps, collaboration, games, real-time dashboards, etc. Beyond the web, microservices and machine-to-machines (M2M) communications also make use of WebSockets. Additional usages:

* Telemetry data streams, e.g. live financial data streams to a site or client program
* Highly responsive asynchronous UIs with fluid UX
* Reactive APIs that are responsive and asynchronous

## WebSocket Implementations

WebSockets are defined by JSR 356 - Java API for WebSocket, which conforms to the IETF WebSocket protocol.

* [Tyrus](https://tyrus-project.github.io/) - Reference Implementation

## WebSocket Lifecycle and Topology

WebSocket implementations are deployed in the presentation layer (?), and are initiated by a client request (a server cannot make the first request).

* Server publishes the endpoint URI that the client can then connect to
* Client initates the WebSocket session with a request to the server using the endpoint URI
* Once the connection is made the flow of data can be bidirectional
* Connection is kept open for the duration of the session, either side can close the connection
  * Closing the browser/tab sends a connection close signal to the server
  * Connection is closed if there is a connection error

There are two parts to the protocol, a handshake and data transfer.

* Open with handshake over HTTP: `GET /websocket/path/to/endpoint HTTP/1.1`
* Upgrade to TCP: `HTTP/1.1 101 switching protocols`
* Endpoints represented by URIs:
  * `ws://host:port/path?query` - unencrypted
  * `wss://host:port/path?query` - encrypted