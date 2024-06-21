## Learn Sql

- Database: collection of data is called as database.
- DBMS: A Software application to manage the database.


- Databases are of Two types:
  - Relational Database: uses table to store the data eg. Mysql, Oracle, MariaDB, etc.
  - Non-Relational Database: data is stored in the key value format or json format but not in the table format. 
    eg. MongoDB.


- why sql? <br>
 we need language to interact with databases.
  So we use sql to interact with DB, to do some CRUD operations.

- then what is mysql?<br>
mysql is relational database management system (RDBMS) that uses sql as its querying language.

- what is sql? <br>
sql is programming language that is used to communicate and manupulate data in the database.
  
- How sql help us?<br>
sql allows users to perrform a variety of tasks related to the database
  - Retrieving Data: extracting precise information from a database through queries.
  - Manipulating Data: Adding, modifying and removing records within a database.
  - Defining Data: creating and adjusting the structure of a database, including table, views and indexes.
  - Controlling Data: managing databases access by granting or revoking permissions.

- Mysql server: Databse Server where data is stored, managed and accessed.

- Mysql WorkBench: It is a visual tool which is used for database design, development, administration and management.
                   It provide an UI (user interface) to interact with mysql server.

- Types of SQl Commands:
  - Data Query Language (DQL): used to retrieve the data from the database.<br>
        Commands: select

  - Data Manipulation Language (DML): used to manipulate data stored in the database.<br>
        Commands: insert, update, delete

  - Data Definition Language (DDL): used to define structure and schema of the database.<br>
        Commands: create, alter, drop, truncate, rename.

  - Data Control Language (DCL): deals with control and security of data within the database.<br>
        Commands: grant, revoke.

  - Transaction Control Language (TCL): TCL used to manage transactions within the database.<br>
        Commands: commit, rollback, savepoint.

- sql uqery satements are case insensitive.

- Create Database:<br>
    creating new database:
    Commands: create database dbname;

    to Avoid errors:
    Commands: create database if not exists dbname;

to access a particular database
commands: USE dbname;