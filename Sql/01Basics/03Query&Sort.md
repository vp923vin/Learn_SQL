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

- If the column alias contains spaces, you need to place it inside quotes like this:<br>
`SELECT CONCAT('Jane',' ','Doe') AS 'Full name';`

- MySQL SELECT statement doesn’t require the FROM clause.
- Assign an alias to a column to make it more readable.


### Sorting Data
- To sort the rows in the result set, add the ORDER BY clause to the SELECT statement.<br>
syntax:<br>
`SELECT 
   select_list
FROM 
   table_name
ORDER BY 
   column1 [ASC|DESC], 
   column2 [ASC|DESC],
   ...;`
<br>
- order by asc (increasing order) or desc (decreasing order).

- It is possible to sort the result set by a column in ascending order and then by another column in descending order:<br>
`ORDER BY
    column1 ASC,
    column2 DESC;`

    - First, sort the result set by the values in the column1 in ascending order.
    - Then, sort the sorted result set by the values in the column2  in descending order. Note that the order of values in the column1 will not change in this step, only the order of values in the column2 changes.



Execution Order of the avove query with select from and order by

 - When executing the SELECT statement with an ORDER BY clause, MySQL always evaluates the ORDER BY clause after the FROM and .

- SELECT clause before the ORDER BY clause, you can use the column alias specified in the SELECT clause in the ORDER BY clause.<br><br>
 `SELECT 
  orderNumber, 
  orderLineNumber, 
  quantityOrdered * priceEach AS subtotal 
FROM 
  orderdetails 
ORDER BY 
  subtotal DESC;`

The FIELD() function returns the index (position) of a value within a list of values.
- Suppose that you want to sort the sales orders based on their statuses in the following order:

- In Process, On Hold, Canceled, Resolved, Disputed, Shipped.

- To do this, you can use the FIELD() function to map each order status to a number and sort the result by the result of the FIELD() function:
- `SELECT 
  orderNumber, 
  status 
FROM 
  orders 
ORDER BY 
  FIELD(
    status, 
    'In Process', 
    'On Hold', 
    'Cancelled', 
    'Resolved', 
    'Disputed', 
    'Shipped'
  );
`
- NULL comes before non-NULL values. Therefore, when you the ORDER BY clause with the ASC option, NULLs appear first in the result set.

### Note: 
- Use the ORDER BY clause to sort the result set by one or more columns.
- Use the ASC option to sort the result set in ascending order and the DESC option to sort the result set in descending order.
- The ORDER BY clause is evaluated after the FROM and SELECT clauses.
- In MySQL, NULL is lower than non-NULL values