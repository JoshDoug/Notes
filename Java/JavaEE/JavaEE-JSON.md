# Java EE JSON

Notes on Java EE's JSON APIs.

* [JWT - JSON Web Token](https://jwt.io/)
* NoSQL/document stores, store data as JSON documents. A JSON document is just another term for a JSON string.
  * NoSQL Datastores: Hadoop, Cassandra, MonetDB, CouchDB, etc.

## [JSON-P API](https://javaee.github.io/jsonp/)

Low-level, lightweight JSON parser and generator for manipulating JSON data at the property value level.

* JSR 353: Java API for JSON Processing
* Current version: 1.1
* Generate, parse, query, and transform JSON
* Two models - object and streaming
  * Object-oriented representation
  * Streaming model - more effecient model
* Memory-based model - loads the entire JSON document into memory

Consists of 3 packages:

* `javax.json`
  * Provides object model API
  * Models JSON data structure
  * Provides factories for parsers and writers
* `javax.json.streaming`
  * Provides streaming model API
  * Provides factories for parsers and writers
* `javax.json.spi`
  * Plugin implementations
  * For implementers and isn't necessary to know in order to use JSON.

### Object Model

### Streaming Model

## [JSON-B API](http://json-b.net/)