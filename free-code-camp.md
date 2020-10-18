// why postgres

1. Robust
2. High Performance
3. Open source

Lot of startups are using it

We are learning using interactive shell psql , there is also gui pgadmin.

best way is learning the raw commands

use sql language -->

What we are going to learning

1. Create database
2. Create tables
3. Insert
4. Update
5. Delete
6. join tables
7. Foreign key
8. Primary key
9. Relations
10.   Sequences
11.   Exporting data to CSV
12.   Grouping
13.   Annotation
14.   Dtabase constraints

what is a databse ?

Database managemnet systems are used to store , retrieve , manipulate the data ,via a computer can called as server.

What is postgresql

psotgres --> Database engine
sql --> structured query language

Running psql in cmd

set path for postgres bin directory.

then enter the following command in cmd

`psql ` never use this.

it will ask for default window user created in postgres but we do not create any user so never use this.

Always use the following

`psql -U postgres`

it will open the psql for user postgres and we can access all the postgres objects for user postgres.

`\q` for quit the shell
`\?` for more help
`help` for help
`\l` for listing the databases

command for listing psql commands

`psql --help`

command for connecting to a particular database remote or local

### Method 1

`psql -h localhost -p 5432 -U postgres test`

-h === hostname
-p === port
-U === username
test is the name of database

### Methid 2 ( while log in as a user)

`\c test` \c === connect test === db name

### A very dangerous command

Dangerous command because it delete the years of important data in matter of milli seconds.

it is for deleting a database

`DROP DATABASE test `

so thats why always maintain the backup of your database.

### Creating a table in the postgres database

```CREATE TABLE table_name (
column_name + data_type +constraints if any
)
```

Example

```CREATE TABLE (
id INT,
first_name VARCHAR(50),
last_name VAR_CHAR(50),
gender VARCHAR(6),
date_of_birth TIMESTAMP
)
```

for knowing and familiar with all the datatypes use postgres documentation.

## command for listing table

`\d` d for describe

## command for describing a particular table

`\d table_name`

## deleting a table

` DROP TABLE person`

## creating a table with constraints

`CREATE TABLE person ( id BIGSERIAL NOT NULL PRIMARY KEY, first_name VARCHAR(50) NOT NULL, last_name VARCHAR(50) NOT NULL , gender VARCHAR(6) NOT NULL, date_of_birth DATE NOT NULL ); `

## inserting a data into a table

`INSERT INTO person ( first_name, last_name, gender, date_of_birth, ) VALUES ("Yogesh","Vishnole","male",DATE "1990-11-27")`

## commad for describing only table not sequences

`\dt`
