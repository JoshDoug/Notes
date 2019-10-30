# [Neo4j](neo4j.com)

* [The Neo4j Getting Started Guide](https://neo4j.com/docs/getting-started/current/)
* [Introduction to Neo4j](https://neo4j.com/graphacademy/online-training/introduction-to-neo4j)
* [Cypher Manual](https://neo4j.com/docs/cypher-manual/current/)
* [Cypher Reference Card](https://neo4j.com/docs/cypher-refcard/current/)

## [Introduction to Neo4j](https://neo4j.com/graphacademy/online-training/introduction-to-neo4j)

### [Intro to Graph DBs](https://neo4j.com/graphacademy/online-training/introduction-to-neo4j/part-1/)

Graph DBs use CRUD operations and are generally used for online transaction processing (OLTP) systems, as they are optimised for transactional performance. Neo4j is ACID compliant. Relationships are first class citizens in graph databases, so it doesn't need to infer connections using foreign keys or MapReduce (is out-of-band porcessing, such as MapReduce, a NoSql thing?). This way of modelling allows graph databases to better reflect the relationships of real world data.

A graph is composed of two elements: **nodes** and **relationships**, a node represents an entity (a thing, person, category, or other piece of data), and a relationship represents how two nodes are connected. Nodes can have lables that are used to define types for nodes.

### [Intro to Neo4j](https://neo4j.com/graphacademy/online-training/introduction-to-neo4j/part-2)

**Neo4j Database** - the heart of the Neo4j Graph Platform. The platform provides APIs, drivers, and tools that help create applications and custom tooling for accessing and visualising graphs.

**Index-free adjacency** - short summary is Neo4j uses pointer navigation which is apparently very fast so indexs aren't necessary.

**ACID** - it's ACID.

**Clusters** - Neo4j supports clusters that provide high availability, scalablity for read access to the data, and failover.

#### Graph Engine

The graph engine is used to interpet Cypher statements and executes kernel-level code (like OS level kernel code?) to store and retrieve data. Apparently you can tune the performance of the engine to suit your particular application needs?

#### Language and Driver Support

Neo4j provides a full stack that implements all levels of access to the database and clustering layer with published APIs. Cypher is used for querying the database. Neo4j supports Java, JavaScript, Python, C#, and Go drivers out of the box that use Neo4j's bolt protocol for binary access tp the database layer. Bolt is an efficent binary protocol that compresses data sent over the wire as well as encrypting it.

It's also possible to develop server-side extensions in Java that access the data in the database directly without using Cypher. There are also community drivers for Ruby, PHP, R, and more. The functionality of Neo4j can also be extended by creating user defined functions and procedures that are callable from Cypher.

#### Libraries

Neo4j provides an open source Cypher library, Awesome Procedures on Cypher (APOC) that contains useful procedures that can be called from Cypher. Graph Algorithms is another library that can help anlayse data in graphs. The GraphQL library can also be used to access a Neo4j Database. These libraries are available as plugins for a Neo4j development environment, but there are more community plugins as well.

#### Tools

Neo4j browser or a web browser can be used to access data and test Cypher statements, which can then be used as part of application code. Bloom is a tool for visualising a graph without knowing much about Cypher. There are also tools for importing and exporting data between flat files and a Neo4j Database, as well as an ETL (Extract, Transfer, and Load?) tool.

### [Setting up a Neo4j development environment](https://neo4j.com/graphacademy/online-training/introduction-to-neo4j/part-3/)

Just `brew cask install neo4j`, which installs the desktop app which also includes the server and Neo4j browser, but is limited to a single running database at a time. The non-cask brew version of neo4j doesn't include the desktop app, but is probably accessible via the neo4j browser using localhost and the port 7474.

Neo4j Browser is different to the Neo4j Desktop, how is it different? I don't know yet.

#### Neo4j Browser

Has a command pane, commands are prefixed with a `:` colon, Cypher statements are not.

* `:help commands`
  * `:help keys` - handy keyboard shortcuts
  * `:help MATCH` - get help on Cypher keywords, e.g. `MATCH`
* `:sysinfo` - system info, self explanatory
* `:history` - shows prior commands/queries, which can then be selected and re-run
* `:clear`

The Browser can save and sync data such as favourite statements/snippets, but only when accessed via a web browser instead of through the Desktop app (although the Desktop app might get this functionality, it might even already have it?).

### [Introduction to Cypher](https://neo4j.com/graphacademy/online-training/introduction-to-neo4j/part-4/)

Cypher is a declarative query language that aims to be simple to use, yet very powerful. It's desinged to be a human-friendly language, using ASCII art for readability (seems quite annoying to type...), and borrows from SQL, SPARQL, and even Haskell & Python. It's available as an open standard called [openCypher](opencypher.org).

#### Nodes

Cypher uses a pair of parentheses, `()`, to represent a node, `(n)`, much like a circle on a whiteboard - neat!

#### Lables

Nodes in a graph are typicall labeled, and these are used to group nodes and filter queries against the graph, this helps otimise queries(?).

#### Comments

`//`

#### Examining the data model

View or get information about the ddata model of the graph with `CALL db.schema`.

#### Using MATCH to retrieve nodes

* `MATCH (n) RETURN n // return all nodes in the graph`
* `MATCH (p:Person) RETURN p // return all Person nodes in the graph`

Nodes can also be viewed as table data in a JSON-style format using the table option on the query section in the Neo4j browser. When nodes are displayed as tables values, the node labels and ids are not shown, only the property values for the nodes.

#### Retrieving nodes

#### Properties

##### Examining property keys

##### Retrieving nodes filtered by a property value

##### Returning property values

##### Specifying aliases

#### Filtering queries using property values

#### Relationships

##### ASCII art

##### Querying using relationships

##### Examining relationships

##### Using a relationship in a query

##### Querying by multiple relationships

##### Using anonymous nodes for a query

##### Using an anonymous relationship for a query

##### Retrieving the relationship types

##### Retrieving properties for relationships
