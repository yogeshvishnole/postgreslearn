what is potgressql ?

It is a database to store data in disk in proper format .
It also provide a way to query and manipulate that data.
It provides a convenient and efficient environment.

SQL

sql is an interfacing language to any relational databases like

MS sql
postgres
mysql
oracle etc.

What are challenges with postgres.

1. How to query and retrive data in an optimized and performant way.
2. Desinging the structur of the database also called the schema design.
3. Knowing when to use advanced features.
4. Maintain the production database.

Now Database design.

Ask three questions

What is the entity.
What propertie entity exhibits.
What type of data each propert helfdd

name of entity == table name
properties == columns in tables
type of data == column data type

##### syntax for creating a table

CREATE TABLE cities(
name VARCHAR(50),
country VARCHAR(50),
population INTEGER,
area INTEGER
)

CREATE ,TABLE === keyword of database
name cities country population === Identifiers
Varchar , Integer === column datatypes,
