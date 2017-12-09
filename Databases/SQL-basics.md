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