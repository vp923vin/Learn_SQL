## Querying and Sorting Data
Querying Data: select From, select<br>
Sorting Data: OrderBy

### Querying Data

- select From: The SELECT statement allows you to select data from one or more tables

    `SELECT select_list
    FROM table_name;`

    - Use the SELECT FROM statement to select data from a table.
    - Use the SELECT * to select data from all columns of a table.

queries:

`SELECT employeeNumber,
       lastName,
       firstName,
       extension,
       email,
       officeCode,
       reportsTo,
       jobTitle
FROM   employees;`

`SELECT * 
FROM employees;`


- Also we can use SELECT statement to perform a simple calculation<br>
`SELECT 1 + 1;`

- SELECT statement to return the current date and time of the server<br>
`SELECT NOW();`

- to concatenate multiple strings into a single string<br> 
`SELECT CONCAT('John',' ','Doe');`

### Column alias
- By default, MySQL uses the expression specified in the SELECT clause as the column name of the result set. To change a column name of the result set, you can use a column alias:<br>
`SELECT expression AS column_alias;`<br><br>
The AS keyword is optional
