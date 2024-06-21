### What is a Relational Database/RDBMS?<br>
-   A Relational Database is a type of database that stores and provides access to data points 
    that are related to one another. <br>
    Relational Database Management System (RDBMS) is a software system that manages relational databases. 
    In a relational database, data is organized into tables (also known as relations), which consist of rows and columns. 
    Each table represents a different type of entity, and relationships can be established between 
    different tables through foreign keys.
    <br>
- Key characteristics of an RDBMS include:
    - Structured Data: Data is organized into tables.
    - Schema: The structure of the database is defined by a schema.
    - SQL: Data manipulation and querying are typically done using Structured Query Language (SQL).
    - ACID Properties: Ensures reliable transactions with Atomicity, Consistency, Isolation, and Durability.

### How is Data Stored in a Relational Database?
-   In a relational database, data is stored in tables. Each table consists of rows and columns:

    - Tables: The fundamental unit where data is stored. Each table represents a different type of entity 
        (e.g., customers, orders).

    - Rows: Each row in a table represents a single record. For example, in a customer table, each row represents one customer.

    - Columns: Each column in a table represents a specific attribute of the entity. 
        For example, in a customer table, columns might include customer_id, name, email, and phone_number.

    - Primary Keys: A column (or a set of columns) that uniquely identifies each row in a table.

    - Foreign Keys: Columns that create a link between two tables. 
        A foreign key in one table points to a primary key in another table, establishing 
        a relationship between the two tables.

### What is a Schema with Respect to a Relational Database?
-   A schema in a relational database is a blueprint or structure that defines the way data is 
    organized and how the relationships between different tables are constructed. 
    It describes the logical configuration of all or part of a relational database.

- Key components of a schema include:

    - Tables: Definitions of the tables in the database, including their columns and data types.

    - Constraints: Rules applied to data in tables, such as primary keys, foreign keys, unique constraints, 
        and check constraints.

    - Indexes: Structures that improve the speed of data retrieval operations on a database table at the 
        cost of additional storage and maintenance.

    - Views: Virtual tables that are based on the result-set of a SQL query. 
        They provide a way to look at the data from one or more tables in a different perspective.

    - Stored Procedures: Precompiled collections of SQL statements that perform a particular task and can be executed on demand.

    - Triggers: SQL code that automatically executes in response to certain events on a particular table or view.

