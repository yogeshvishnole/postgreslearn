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

##### Inserting into a table

INSERT INTO cities(name,country,population,area)
VALUES
('Delhi','India',23458488,2342),
('Tokyo','Japan',72839929,8223);

##### Retrive data using select

`SELECT * FROM cities;`

-  means all columns

For retriving only the specific columns

`SELECT name,country FROM cities`

selecting same column

`SELECT name,name,name FROM cities;`

## Some powerful sql

SQL isnot just about pullong the raw data

We can write SQL to transform or process data before we recieive it.

Example
` SELECT name,|/area FROM cities`

Some common math operators

-  Add - Subtract / divivsion |/ square root ^ exponent \* multiply @ absolute value % remainder

Renaming a callculated column

` SELECT name , population/area AS population_density FROM cities`

## String operators and functions

|| Join two strings CONCAT() Join two strings LOWER() Gives a lowercase string
LENGTH() gives number of characters ina string UPPER() Gives an uppercase string

example query `SELECT name || ', ' || country FROM cities`

`SELECT UPPER(CONCAT(name,', ',country)) AS location FROM cities;`
`SELECT (CONCAT(LOWER(name),', ',LOWER(country))) AS location FROM cities;`

## Filtering Rows with Where Clause ( Select operation in relatinal algebra)

`SELECT name,area FROM cities WHERE area > 2000;`

Evaluation order of the above query.

1. SELECT name,area --> Third
2. WHERE area > 2000 --> second
3. FROM cities --> third.

##### Comparison Math Operators for used in the where clause

1. = Are the values equal
2. > Is the value on the left greater.
3. < Is the value on the left less
4. > = Is value on left greater or equal
5. IN Is the value present in a list
6. BETWEEN
7. NOT IN
8. <= Is the value on the left less than or equal to.
9. <> Are the values not equal
10.   != Are the values not equal

Example of between

`SELECT name,area FROM cities WHERE area BETWEEN 2000 AND 4000`

Example of IN

`SELECT name,area FROM cities WHERE name IN("Delhi","Shanghai") `

Example of NOT IN

`SELECT name,area FROM cities WHERE name NOT IN("Delhi","Shanghai") `

we can use any data type inside list.

### Compound Checks using AND and OR operator

`SELECT name,area FROM cities WHERE name NOT IN("Delhi","Shanghai") AND name = "Delhi"`

```
SELECT name,area
FROM cities
WHERE name NOT IN("Delhi","Shanghai") OR name = "Delhi" OR name = "TOKYO"
```

##### Using column calculation inside the where clause

`SELECT name population/area AS population_density FROM cities WHERE population/area > 6000 `

##### Updating rows

`UPDATE cities SET population = 39000000 WHERE name = 'Tokyo';` careful that the condition should select the specific city that you want.

##### Deleting rows

`DELETE FROM citites WHERE name = "Tokyo"`

# Database design ( my favourite topic)

Now we head over by considering a real time situation

We design a database for a photo sharing app

Users photos
Comments Likes

Types of relationships

1. One to one
2. One to many
3. Many to one
4. Many to Many

The constructs for implementing relationships.

1. Primary key = Uniquely identifies a record in a table.
2. Foreign key = Uniquely identifies a record (usually in another table) that this row is associated with.

### Now SQL for relationships , primary keys and foriegn keys.

// Creating the users table

CREATE TABLE users (
id SERIAL PRIMARY KEY,
username VARCHAR(50)
)

// Creating a photos table

CREATE TABLE photos (
id SERIAL PRIMARY KEY,
url VARCHAR(200),
user_id INTEGER REFERENCES users(id)
)

-- Firstly, remove PRIMARY KEY attribute of former PRIMARY KEY
ALTER TABLE <table_name> DROP CONSTRAINT <table_name>\_pkey;
-- Then change column name of your PRIMARY KEY and PRIMARY KEY candidates properly.
ALTER TABLE <table_name> RENAME COLUMN <primary_key_candidate> TO id;
-- Lastly set your new PRIMARY KEY
ALTER TABLE <table_name> ADD PRIMARY KEY (id);

#### Now running queries on the associated data

We are usually doing it with joins but we are going to it in a little time.

SELECT \* FROM photos where user_id = 4;

### Foriegn key constraints

Around Insertion

1. We insert a photo that tieds to a existing user === Everyhing ok.
2. We insert a photo that refers to a user that not exists === Foreign key constraint error.
3. We insert a photot that is not tied to any user === NULL

query for inserting a null

INSERT INTO photos(url,user_id)
VALUES ("http://hello",NULL);

Constraints around deletion,

Now when we delete a user has various photos own by it, then we can take following steps.

1. On delete restrict --> Throw an error on deletion of user.
2. On delete no action --> Throw an error on deletion of user.
3. On delete cascade --> Delete the user with all the photos associated with it.
4. On delete set null --> Set the user_id of photo to null.
5. On delete set default --> Set the user_id of the photo to a default value , if one is provided.

Now setting up the ON DELETE CASCADE constraint

CREATE TABLE photos (
id SERIAL PRIMARY KEY,
url VARCHAR(200),
user_id INTEGER REFERENCES users(id) ON DELETE CASCADE
);

INSERT INTO photos (url, user_id)
VALUES
('http:/one.jpg', 4),
('http:/two.jpg', 1),
('http:/25.jpg', 1),
('http:/36.jpg', 1),
('http:/754.jpg', 2),
('http:/35.jpg', 3),
('http:/256.jpg', 4);

Now setting up the ON DELETE SET NULL constraint

CREATE TABLE photos (
id SERIAL PRIMARY KEY,
url VARCHAR(200),
user_id INTEGER REFERENCES users(id) ON DELETE SET NULL
);

INSERT INTO photos (url, user_id)
VALUES
('http:/one.jpg', 4),
('http:/two.jpg', 1),
('http:/25.jpg', 1),
('http:/36.jpg', 1),
('http:/754.jpg', 2),
('http:/35.jpg', 3),
('http:/256.jpg', 4);

Constraints around updating.

### What is a schema diagram ?

A diagram with all the basic structure of all tables of database ( with attributes name and datatypes ) is called as the schema diagram of the database.

### Now lets add some complexity by adding the "comments" table to our db.
