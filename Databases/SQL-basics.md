# SQL - Structured Query language-basics

A database query language.
Current stable standard: SQL:2011, or ISO/IEC 9075:2011

* ISO - International Standards Organisation
* IEC - International Electrotechnical Commission
* ANSI - American National Standards Institute

Query clauses/statements/keywords:

* SELECT - columns to select from
* FROM - tables to query
* WHERE -
* GROUP BY
* HAVING
* ORDER BY
* DISTINCT - Eliminates duplicate data

## Basic Examples

```sql
SELECT * FROM table
WHERE lang="en"
ORDER BY location
```

Parts to cover:

* Joins
* DB Design (normalisation etc)
* data types

## Oracle SQL Useful Snippets

Check the Oracle Server type and version: `SELECT * FROM V$VERSION`

Get a list of commands to drop all the tables of a database (copy and run the output of the command to actually drop the tables):

`select 'drop table '||table_name||' cascade constraints;' from user_tables;`

Get the primary keys of a table using just the table name (useful for checking the primary keys are properly set):

```SQL
SELECT cols.table_name, cols.column_name, cols.position, cons.status, cons.owner
FROM all_constraints cons, all_cons_columns cols
WHERE cols.table_name = 'TABLE_NAME'
AND cons.constraint_type = 'P'
AND cons.constraint_name = cols.constraint_name
AND cons.owner = cols.owner
ORDER BY cols.table_name, cols.position;
```

It's Oracle, so replace 'TABLE_NAME' with the name of the table and ensure it is in upper case.

Oracle SQL [Triggers](https://docs.oracle.com/cd/B19306_01/server.102/b14200/statements_7004.htm), example tables with triggers:

```SQL
CREATE TABLE FreightWagonType
(
FreightWagonTypeID  number(3) PRIMARY KEY,
FreightWagonType    varchar2(24) NOT NULL,
NumberOwned         number(3) DEFAULT 0 /* hope this works */
)

CREATE TABLE FreightWagon
(
SerialNumber    number(5) PRIMARY KEY
    REFERENCES RollingStock(SerialNumber),
FreightWagonTypeID number(3)
    REFERENCES FreightWagonType(FreightWagonTypeID)
TareWeight      number(4) NOT NULL,
MaxPayload      number(4) NOT NULL,
Capacity        number(4),
Description     varchar2(1024) NOT NULL
)

/* Increment number of Freight Wagons owned */
CREATE OR REPLACE TRIGGER increment_freight_number
    AFTER INSERT ON FREIGHTWAGON
    FOR EACH ROW
    BEGIN
        UPDATE FREIGHTWAGONTYPE
        SET FREIGHTWAGONTYPE.NUMBEROWNED = FREIGHTWAGONTYPE.NUMBEROWNED + 1
        WHERE FREIGHTWAGONTYPE.FREIGHTWAGONTYPEID = :NEW.FreightWagonTypeID;
    END;

/* Decrement number of Freight Wagons owned */
CREATE OR REPLACE TRIGGER decrement_freight_number
    AFTER DELETE ON FREIGHTWAGON
    FOR EACH ROW
    BEGIN
        UPDATE FREIGHTWAGONTYPE
        SET FREIGHTWAGONTYPE.NUMBEROWNED = FREIGHTWAGONTYPE.NUMBEROWNED - 1
        WHERE FREIGHTWAGONTYPE.FREIGHTWAGONTYPEID = :OLD.FreightWagonTypeID;
    END;
```

Here an addition to the FreightWagon table will increment the number owned in the FreightWagonType table, and a delete will decrement it.

To remove a trigger: `DROP TRIGGER increment_freight_number;`

### Auto Increment Alternative (for Oracle DBs prior to 12c, such as 11g)

* [Oracle: How to Create an Auto Increment Field Using Sequence](http://www.tech-recipes.com/rx/19736/oracle-how-to-create-an-auto-increment-field-using-sequence/)

Using a Sequence:

```SQL
CREATE sequence driverSeq start with 1
increment by 1;

INSERT INTO DRIVER /* Test */
(DriverID, DriverType)
VALUES (driverSeq.nextval, 'Driver');
```

Can also have min and max values:

```SQL
Create sequence sequence_name start with value
increment by value
minvalue value
maxvalue value;
```