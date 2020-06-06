## What is a Database?
   A place where you can:-
   1. Store data
   2. Manipulate data
   3. Retrieve data

   **Example** facebook database that has different users fb accounts

## PostgreSQL 
   PostgreSQL is an *object-relational database system* that has the features of traditional proprietary database 
   systems with enhancements to be found in next-generation DBMS systems

   It has predominant features from SQL. SQL is a programming language.Manages data held in *relational* database. 
   SQL is easy to learn, powerful & widely used all over the internet. Some of the highlights of postgresql:-

   1. Object relational database management system

   2. Modern

   3. Open Source


## What is Relational Database?

   It is the relation between two or more tables where each table consist of rows and column.

## Download(for mac)
    
   go to https://postgresapp.com/ and then, click on download tab (**Additional releases**-->download).

   This downloads the Postgres server app on your computer which can be used to spin up a new db, with available versions, you can start or stop the db by seeing the app button on the menubar section on top of your screen. You can use GUI client, terminal/cmd or an application to connect to the databases.

## Terminal Mode (--> means you are executing these commands on terminal)

--> psql (get's you inside of that db server)

--> psql --help (any help you need to navigate)

--> \l (list of databases)

--> \q (to quit and come out of the database)

--> **CREATE DATABASE <NAME>;** (create your own database)

#### Connect to the database

--> ```psql -h localhost -p 5432 -U anshul.choudhary@ibm.com <NAME>```

#### Connect to another database if you are already in one of the database

--> ```\c <NAME>```

#### Delete a database (*A very DANGEROUS command*)

--> **DROP DATABASE <name>;**

#### How to create table with Postgres?

--> CREATE TABLE table_name ( 
    Column name + data type + constraints if any
    );

**Ex.**
-->
```
CREATE TABLE person(

     id int,
     first_name VARCHAR(50),       
     last_name VARCHAR(50), 
     gender VARCHAR(6), 
     date_of_birth DATE, 

);
```
--> CREATE TABLE (you will this message on terminal)
Here, 50 in bracket is signifying how many characters are allowed for that attribute for the VARCHAR data type

#### How to see the table you have just created?

--> \d (to see the list of all the tables in the database you are in right now)

**Ex.**
```
test=# \d
                 List of relations
 Schema |  Name  | Type  |          Owner
--------+--------+-------+--------------------------
 public | person | table | anshul.choudhary@ibm.com
(1 row)
```

--> \d <TABLE NAME> (to see what's inside the table)

**Ex.**          

```  
test=# \d person
                    Table "public.person"
    Column     |         Type          | Collation | Nullable | Default
---------------+-----------------------+-----------+----------+---------
 id            | integer               |           |          |
 first_name    | character varying(50) |           |          |
 last_name     | character varying(50) |           |          |
 gender        | character varying(7)  |           |          |
 date_of_birth | date                  |           |          |

```

**Ex.** 
```
CREATE TABLE person(

     id BIGSERIAL NOT NULL PRIMARY KEY,
     first_name VARCHAR(50) NOT NULL,       
     last_name VARCHAR(50) NOT NULL, 
     gender VARCHAR(6)NOT NULL, 
     date_of_birth DATE NOT NULL, 

);
```
* BIGSERIAL: It is the signed integer which auto increments

```
test=# \d
                      List of relations
 Schema |     Name      |   Type   |          Owner
--------+---------------+----------+--------------------------
 public | person        | table    | anshul.choudhary@ibm.com
 public | person_id_seq | sequence | anshul.choudhary@ibm.com
(2 rows)
```

```
                                       Table "public.person"
    Column     |          Type          | Collation | Nullable |              Default
---------------+------------------------+-----------+----------+------------------------------------
 id            | bigint                 |           | not null | nextval('person_id_seq'::regclass)
 first_name    | character varying(50)  |           | not null |
 last_name     | character varying(50)  |           | not null |
 gender        | character varying(6)   |           | not null |
 date_of_birth | date                   |           | not null |
 email         | character varying(150) |           |          |
Indexes:
    "person_pkey" PRIMARY KEY, btree (id)
```



```
test=# \d person_id_seq
                       Sequence "public.person_id_seq"
  Type  | Start | Minimum |       Maximum       | Increment | Cycles? | Cache
--------+-------+---------+---------------------+-----------+---------+-------
 bigint |     1 |       1 | 9223372036854775807 |         1 | no      |     1
Owned by: public.person.id
```
#### How to delete a table ?

**Ex.**
```
test=# DROP TABLE person;
DROP TABLE (message you will see on the screen)

```
#### How to view just the table?
```
test=# \dt
                 List of relations
 Schema |  Name  | Type  |          Owner
--------+--------+-------+--------------------------
 public | person | table | anshul.choudhary@ibm.com
(1 row)
```

#### How to insert records into table?

**Ex.**
-->
```
INSERT INTO person (
first_name,
last_name,
gender,
date_of_birth)
VALUES ('Anshul','Choudhary','MALE', DATE '1983-09-04');

```
--> INSERT 0 1 (you will see this message on terminal)


#### How to input a file with database onto the postgresql ?


```
test=# \i <path to file.sql>
```

#### How to view/read the database of the file uploaded?

```
test=# SELECT * FROM person;  (here, person is the table name)
```

* Viewing a particular record

```
test=# SELECT first_name FROM person;  (here, person is the table name)
```


* Viewing record in certain way

```
test=# SELECT first_name FROM person ORDER BY first_name;  (here, person is the table name)
```

```
test=# SELECT country_of_birth FROM person ORDER BY country_of_birth;  (here, person is the table name)
```

* Viewing only unique items using **DISTINCT** 

```
test=# SELECT DISTINCT country_of_birth FROM person ORDER BY country_of_birth;  (here, person is the table name)
```

#### Where Clause (*Allows us to filter the data based on conditions*) with Arithematic Operators, Comparisons etc.

Various Conditions & ex. :-

```
test=# SELECT gender FROM person WHERE gender = 'Male';  (here, person is the table name)
```

* Adding 'AND'

```
test=# SELECT gender FROM person WHERE gender = 'Male' AND country_of_birth ='USA';  (here, person is the table name)
```

* Adding 'OR' & 'AND'

```
test=# SELECT gender FROM person WHERE gender = 'Male' AND (country_of_birth ='USA' OR country_of_birth ='India');  (here, person is the table name)
```

* Comparison operator

```
test=# SELECT 1 = 2;
```

f (you will see this false message on the screen)

```
test=# SELECT 1 <> 2;
``` 
* (not equal <>)


#### Using LIMIT and OffSET

Below displays only the first 5 person using limit, first person is at id 1

```
test=# SELECT * FROM person LIMIT 5;  (here, person is the table name)
```

Below displays the 5 person using limit after an OFFSET of 5 which means the first person would be at id 6

```
test=# SELECT * FROM person OFFSET 5 LIMIT 5;  (here, person is the table name)
```

 **you can also use FETCH( like in SQL)

#### Using IN and BETWEEN

```
test=# SELECT * FROM person WHERE country_of_birth IN ('China','France','Brazil');  (here, person is the table name)
```

 is same as

```
test=# SELECT * FROM person WHERE country_of_birth = 'China' OR country_of_birth = 'France' OR country_of_birth = 'Brazil');  (here, person is the table name)
```


```
test=# SELECT * FROM person WHERE date_of_birth BETWEEN DATE '1983-05-04' AND '2000-0-01';  (here, person is the table name)
```

#### LIKE and iLIKE

Use to match the text values using pattern 

* %-> means any

```
test=# SELECT * FROM person WHERE email LIKE '%@bloomberg.com';  (here, person is the table name)

```

```
test=# SELECT * FROM person WHERE email LIKE '%@bloomberg.%';  (here, person is the table name)
```

* using _ to match the exact number of characters while searching

```
test=# SELECT * FROM person WHERE email LIKE '_ _ _ @%';  (here, person is the table name)
```

* using _ & character to match the exact number of characters while searching

```
test=# SELECT * FROM person WHERE email LIKE '_ _ o @%';  (here, person is the table name)
```

* Using iLIKE instead of LIKE makes the search not case-sensitive 

#### GROUP BY       

Below example finds how many people are from that particular country:-

```
test=# SELECT country_of_birth, COUNT(*) FROM person GROUP BY country_of_birth;
```

We don't have to define count before while creating the table.

#### HAVING

Below example finds how many people are from that particular country having count more than 5:-

```
test=# SELECT country_of_birth, COUNT(*) FROM person GROUP BY country_of_birth HAVING COUNT(*) > 5;
```

#### Using MAX, AVG and MIN

* Below 3 examples display the price:-

```
test=# SELECT MAX(price) FROM car; (here, car is the table name)
```

```
test=# SELECT MIN(price) FROM car; (here, car is the table name)
```

```
test=# SELECT AVG(price) FROM car; (here, car is the table name)
```

* Below command display the price and other attributes selected

```
test=# SELECT make, model, MIN(price) FROM car GROUP BY make, model; (here, car is the table name)
```

* Round the numbers

```
test=# SELECT ROUND(AVG(price)) FROM car; (here, car is the table name)
```

#### SUM

* Displays the sum over the entire table

```
test=# SELECT SUM(price) FROM car; (here, car is the table name)
```

* Displays the sum over the entire table with make 

```
test=# SELECT make, SUM(price) FROM car GROUP BY make; (here, car is the table name)
```

#### Arithematic Operations

* Factorial

SELECT 5!;

* Modulation

SELECT 10 % 3;

--> 1 (you will see this on screen, this is the remainder)

#### Rounding off the Value to a certain place

```
test=# SELECT make, SUM(price), ROUND(price * .10,2) FROM car GROUP BY make; (here, car is the table name)
```

**the number 2 inside ROUND signifies to round off the value to two decimal places

#### Using AS keyword to have alias for column name or override the original column name

```
test=# SELECT make, SUM(price), ROUND(price * .10,2) AS ten_percent FROM car GROUP BY make; (here, car is the table name)
```

#### COALESCE keyword (placeholder aka provides a default value if the first one is not present)

```
test=# SELECT COALESCE(1) AS number (here, car is the table name)
```
--> number 1 

```
test=# SELECT COALESCE(null,null,1,10) AS number (here, car is the table name)
```
--> number 1 (tried first value, then next)

```
test=# SELECT COALESCE(email,'Email not provided') FROM person (here, person is the table name & email is one of the column inside person table)
```
--> if email is not provided then 'Email not provided' will be displayed

#### Using NULLIF

* without NULLIF
```
test~# SELECT 10 / 0;
```
--> Error: division by zero (you see this on your screen)

*with NULL

```
test~# SELECT 10 / NULL;
```
--> empty with no error (you see this on your screen)

*with NULLIF

```
test~# SELECT 10 / NULLIF(0,0);
```
--> no error (you see this on your screen)

* with COALESCE & NULLIF

```
test~# SELECT COALESCE(10 / NULLIF(0,0)0);
```
--> 0 (you see this on your screen)

#### Using DATES

```
test~# SELECT NOW();
```
--> displays the date & time

```
test~# SELECT NOW()::DATE;
```
--> displays the date

```
test~# SELECT NOW()::TIME;
```
--> displays the time

```
test~# SELECT NOW() - INTERVAL '1 YEAR';
```
--> displays the date & time an year back

```
test~# SELECT NOW() + INTERVAL '10 DAYS';
```
--> displays the date & time 10 days ahead

```
test~# SELECT EXTRACT(YEAR FROM NOW());
```
--> displays the current year

#### Primary Key ( it's job is to identify a record in the table)

* We cannot add pk if we have duplicate row record in the table which we are trying to use as pk
* pk helps identifying a record uniquely

*If you want to cleanout duplicate records*

DELETE FROM person where id = <duplicate id>; (*in this example we chose id column of all the records as pk*)

* Now, you can use pk

```
test~# ALTER TABLE person ADD PRIMARY KEY (id)
```

#### Unique Constraints (it's not same as primary key)

* We cannot add unique constraints if we have duplicate column record in the table which we are trying to use as unique constraint

```
test~# ALTER TABLE person ADD CONSTRAINT unique_email_address UNIQUE (<unique column constraint>);
```

*OR*

```
test~# ALTER TABLE person ADD UNIQUE (<unique column constraint>);
```

#### Boolean Condition







*Reference*:- 
 1. [freeCodeCamp](https://youtu.be/qw--VYLpxG4)
 2. [Generate random data in postgresql](https://mockaroo.com)



   


