# [MongoDB](https://www.mongodb.com/)

MongoDB is a NoSQL document database, that stores data in JSON-like documents.

* [What is MongoDB - Quick Overview of MongoDB](https://www.mongodb.com/what-is-mongodb)
* [MongoDB Architecture](https://www.mongodb.com/mongodb-architecture)
* [MongoDB University - Might be free?](https://university.mongodb.com/)
* [MongoDB Node Driver](https://mongodb.github.io/node-mongodb-native/)
* [MongoDB CRUD Operations](https://docs.mongodb.com/manual/crud/)
* [Aggregation Pipeline](https://docs.mongodb.com/manual/core/aggregation-pipeline/)
* [Text Search](https://docs.mongodb.com/manual/text-search/)
* [MongoDB Compass](https://docs.mongodb.com/compass/current/)

## Getting Started with Docker

* Pull latest docker image from 'Docker Official Images' with `docker pull mongo`.
* Start like any other container, map ports and volumes etc, e.g.: `example command with good defaults`
* Attach to container and access the mongo shell: `docker exec -it mongo-example bash`

## Getting Started - Docs

### Mongo Shell

* Access with `mongo`, might need to start `mongod` first depending on environment, e.g. local install
* Check current database being used with `db` command
* Switch database with `use <database>` command
* Check databases available with `show dbs`
* Use [`db.getSiblingDB()`](https://docs.mongodb.com/manual/reference/method/db.getSiblingDB/#db.getSiblingDB) to access a different database from the current db without switching database context

### Compass

### Python

### Node.js

## [MongoDB Compass](https://docs.mongodb.com/compass/current/)

A gui for MongoDB, like PhpMyAdmin  for MySQL.

## Mongo Import

E.g. `mongoimport --db learning_mongo --collection tours --jsonArray --file tours.json`
