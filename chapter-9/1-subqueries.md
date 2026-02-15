# SubQueries
  A Query inside the another query

  main Query -> outer query
  sub query -> inner query  
  sub query inside subquery -> nested subquery

### categories
1. Dependency  
    - non-corelated subquery  
    - corelated subquery
2. Result types
    - scalar subquery - return single value
    - row subquery - return mutiple rows and single column
    - table subquery - return multiple rows and mutiple columns
3. location/clauses can use with
    - select => Used to aggregate data side by side with the main query's data, allowing for direct comparision 
    - from   => Used as temporary table for the main query
    - join   => used to prepare the data (filtering or aggregation) before joining it with other tables.
    - where -> comparision and logical operatore  => 

subquery in the form clause
- TASK: 
    find the products that have a price higher than the average price of all products.

        SELECT
            * 
        FROM
        -- subquery
            (
                SELECT 
                    ProductID, 
                    Price, 
                    AVG(Price) OVER() AvgPrice
                FROM products
            )t
        WHERE Price > AvgPrice;
 
- TASK: 
    Rank customers based on their total amount of sales 

        SELECT
            *,
            RANK() OVER(ORDER BY totalSales desc) customerRank
        FROM (
                SELECT
                CustomerID,
                SUM(Sales) as totalSales
                FROM orders
                GROUP BY CustomerID
            )t;



#### subquery in the select clause
rules: only scalar subqueries are allowed to use 


- TASK: show the product ids, name, prices and total number of orders
    SELECT 
        ProductID, 
        Product, 
        Price ,
        (SELECT COUNT(*) FROM orders) totalOrders
    FROM products;


- TASK: show all customer details and find the total orders for each customer
    SELECT 
        c.*,
        co.totalOrder
    FROM customers c
    LEFT JOIN (
            SELECT 
                CustomerID,
                COUNT(OrderID) totalOrder
            FROM orders o
            GROUP BY CustomerID
        ) co
    ON co.CustomerID= c.CustomerID;


- TASK: find the products that have a price higher than the average price of all products 
    SELECT 
        *,
        (
            SELECT 
            AVG(price)
            FROM products
        ) avgPrice
    FROM products 
    WHERE price > (
                SELECT 
                AVG(price)
                FROM products
            );


- TASK: show the details of orders made by customers in germany 
    SELECT 
	    * 
    FROM orders
    WHERE CustomerID IN (
            SELECT
            CustomerID 
            FROM customers WHERE country = 'Germany'
        );


- TASK: show the details of orders for customers who are not from germany
    SELECT 
	    * 
    FROM orders
    WHERE CustomerID NOT IN (
            SELECT
            CustomerID 
            FROM customers WHERE country = 'Germany'
        );


- ANY Operator
checks if a value matches any value within a list 
used to check if a value is true for atleast one of the values in a list 


- TASK:  find the female employees whose salaries are greater than the salaries of any male employees
    SELECT 
        EmployeeID, 
        FirstName, 
        LastName 
    FROM employees 
    WHERE Gender = 'F' AND  Salary > ANY ( 
        SELECT 
            Salary 
        FROM employees 
        WHERE Gender = 'M'
    );


- ALL Operator 
checks if a value matches all value within a list. 

- TASK: find the female employees whose salaries are greater than the salaries of all male employees
    SELECT 
        EmployeeID, 
        FirstName, 
        LastName 
    FROM employees 
    WHERE Gender = 'F' AND  Salary > ALL ( 
        SELECT 
            Salary 
        FROM employees 
        WHERE Gender = 'M'
    );


- non-coreleated and corelated subquery  
    - Definition:
        non-coreleated subquery: a subquery that run independently from the main query.
        corelated subquery: a subquery that relays on the values from the main query.
    - Execution:
        non-coreleated subquery: executed once and its result is used by the main query.
                                can be executed on its own. 
        corelated subquery: executed for each row processed by the main query.
                            can't be executed on its own.
    - Easy to use: 
        non-coreleated subquery: easier to read.
        corelated subquery: harder to read and more complex.
    - Performance: 
        non-coreleated subquery: executed only once leads to better performance
        corelated subquery: executed multiple times lead to bad performance 
    - usage: 
        non-coreleated subquery: static comparisons, filtering with constants 
        corelated subquery: row by row comparisons, dynamic filtering


- TASK: show all customer details and find the total orders for each customer   

    SELECT 
        * ,
        (
            SELECT 
                count(*) 
            FROM orders o 
            WHERE o.CustomerID = c.CustomerID
        ) totalSales
    FROM customers c;


- corelated subquery in where clause exists operator 

    SELECT column1, column2, column3 
    FROM Table1
    WHERE EXISTS (
            SELECT 1
            FROM Table2
            WHERE Table2.ID = Table1.ID
        );
    Note: here table1 inside the sub query which show they are co-related


- TASK: show the details of orders made by customers in germany 
    SELECT 
        * 
    FROM orders o 
    WHERE Exists (
        SELECT 1 
        FROM customers c 
        WHERE Country = 'Germany' and o.CustomerID = c.CustomerID
    );


- NOT USE : 


    SELECT 
        * 
    FROM orders o 
    WHERE NOT Exists (
        SELECT 1 
        FROM customers c 
        WHERE Country = 'Germany' and o.CustomerID = c.CustomerID
    );


