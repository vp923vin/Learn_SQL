#### these value functions use for analytics
### lead function
    access a value from next row within a window
    
    LEAD(EXPRESSION (Sales) , OFFSET (2), DEFAULT VALUE (10)) over (PARTITION BY productID ORDER BY orderDate)

    EXPRESSION is required (any data type )
    OFFSET is optional number of rows forward from the current row default = 1
    DEFAULT VALUE is optional return default value if next row is not available Default = NULL
    PARTITION BY is optional 
    ORDER BY is required


### lag function
    access a value fom previous row within a window


    LAG(EXPRESSION (Sales) , OFFSET (2), DEFAULT VALUE (10)) over (PARTITION BY productID ORDER BY orderDate)

    EXPRESSION is required (any data type )
    OFFSET is optional number of rows backward from the current row default = 1
    DEFAULT VALUE is optional return default value if previous row is not available Default = NULL
    PARTITION BY is optional 
    ORDER BY is required


#### USE CASES: 

#### IMPORTANT USE CASE: 

##### Time series analysis: 
    the process of analyzing  the data to understand pattern trends and behaviours over the time 

###### YoY: (Year-over-Year) alaysis
    analyze the overall growth or decline of the bussiness performance over the time 
###### MoM: (month-over-month) alaysis
    analyze the short term trends and dicover patterns in seasonality

    TASK:
    ANALYZE the month-over-month (MoM) performance by finding the percentage change in sales between the current and previous month  

    SELECT   
        *,
        CurrentMonthSales - PreviousMonthSales as MoM_change,
        ROUND((CurrentMonthSales - PreviousMonthSales)/PreviousMonthSales * 100, 1) MoM_percentChange
    FROM
        (
            SELECT 
                MONTH(OrderDate) as OrderMonth,
                Sum(Sales) as CurrentMonthSales,
                lag(SUM(Sales)) OVER(ORDER BY MONTH(OrderDate)) PreviousMonthSales
            FROM orders
            GROUP BY month(OrderDate)
        )t;



##### Customer retention analysis: 
    measures customer's behaviour and loyalty to help bussiness to build relationship with customers.

    TASK:
    Analyze customer loyalty by ranking customers based on the average number of days between orders 

    SELECT 
        CustomerID,
        AVG(DaysUntilNextOrder) AvgDays,
        RANK() OVER(ORDER BY COALESCE(AVG(DaysUntilNextOrder), 99999)) rankAvgDays
    FROM 
        (
            SELECT 
                OrderID,
                CustomerID,
                OrderDate currentOrder,
                LEAD(OrderDate) OVER(PARTITION BY CustomerID ORDER BY OrderDate) NextOrder,
                DATEDIFF(lead(OrderDate) OVER(PARTITION BY CustomerID ORDER BY OrderDate), OrderDate) DaysUntilNextOrder
            FROM orders 
            ORDER BY CustomerID, OrderDate
        )t 
    GROUP BY CustomerID;


##### Comparision analysis: 
### first value 
    FIRST_VALUE()
    access a value from the first row within a window 

    syntax: 
    FIRST_VALUE(Sales) OVER(ORDER BY Month RANGE BETWEEN UNBOUND PRECEDING AND CURRENT ROW)

    DEFAULT  => RANGE BETWEEN UNBOUND PRECEDING AND CURRENT ROW
### last value
    LAST_VALUE()
    access a value from the last row within a window


    syntax: 
    LAST_VALUE(Sales) OVER(ORDER BY Month RANGE BETWEEN UNBOUND PRECEDING AND CURRENT ROW)
    DEFAULT  => RANGE BETWEEN UNBOUND PRECEDING AND CURRENT ROW

    In last value default not able to achieve the last value from the window so need to change 

    LAST_VALUE(Sales) OVER(ORDER BY Month ROWS BETWEEN CURRENT ROW AND UNBOUND FOLLOWING)

    TASK:
    find the lowest and highest sales for each product

        SELECT 
            OrderID, 
            ProductID, 
            Sales,
            FIRST_VALUE(Sales) over(PARTITION BY ProductID ORDER BY Sales) lowest_sales,
            LAST_VALUE(Sales) over(PARTITION BY ProductID ORDER BY Sales ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING) highest_sales,
            FIRST_VALUE(Sales) over(PARTITION BY ProductID ORDER BY Sales desc) highestSales,
            MIN(Sales) over(PARTITION BY ProductID) lowSales,
            MAX(Sales) over(PARTITION BY ProductID) higeSales
        FROM orders;






    TASK: 
    find the difference in sales between the current and the lowest sales

        SELECT 
            OrderID, 
            ProductID, 
            Sales,
            FIRST_VALUE(Sales) over(PARTITION BY ProductID ORDER BY Sales) lowest_sales,
            LAST_VALUE(Sales) over(PARTITION BY ProductID ORDER BY Sales ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING) highest_sales,
            Sales - FIRST_VALUE(Sales) over(PARTITION BY ProductID ORDER BY Sales) SalesDifference
        FROM orders;
