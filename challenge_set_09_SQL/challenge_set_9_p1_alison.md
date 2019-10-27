# Challenge Set 9
## Part I: W3Schools SQL Lab 

*Introductory level SQL*

--

This challenge uses the [W3Schools SQL playground](http://www.w3schools.com/sql/trysql.asp?filename=trysql_select_all). Please add solutions to this markdown file and submit.

1. Which customers are from the UK?

SELECT CustomerName FROM Customers WHERE Country='UK';

Around the Horn
B's Beverages
Consolidated Holdings
Eastern Connection
Island Trading
North/South
Seven Seas Imports

2. What is the name of the customer who has the most orders?

SELECT COUNT(OrderID) AS order_cnt , CustomerName FROM Orders JOIN Customers ON Orders.CustomerID = Customers.CustomerID GROUP BY CustomerName ORDER BY order_cnt DESC;
Ernst Handel

3. Which supplier has the highest average product price?

SELECT SupplierName, MAX(avg_price) FROM (SELECT AVG(Price) AS avg_price, SupplierName FROM Products JOIN Suppliers ON Products.SupplierID = Suppliers.SupplierID GROUP BY SupplierName) AS price_averages;

Aux joyeux ecclésiastiques	140.75

4. How many different countries are all the customers from? (*Hint:* consider [DISTINCT](http://www.w3schools.com/sql/sql_distinct.asp).)

SELECT COUNT(DISTINCT(Country)) FROM Customers;

21

5. What category appears in the most orders?

SELECT COUNT(DISTINCT(OrderID)) AS cnts, CategoryName FROM OrderDetails JOIN Products ON OrderDetails.ProductID = Products.ProductID JOIN Categories ON Products.CategoryID = Categories.CategoryID GROUP BY Categories.CategoryName ORDER BY cnts DESC LIMIT 1;

80	Beverages

6. What was the total cost for each order?

SELECT SUM(Quantity\*Price) AS order_price, OrderID FROM OrderDetails JOIN Products ON OrderDetails.ProductID = Products.ProductID GROUP BY OrderID ORDER BY order_price DESC;

15353.6	10372
14366.5	10424
14104	10417
13427	10353
9244.250000000002	10360
7698.45	10324
...

7. Which employee made the most sales (by total price)?

SELECT MAX(total_sales), LastName, FirstName FROM (SELECT SUM(order_price) AS total_sales,EmployeeID FROM (SELECT SUM(Quantity\*Price) AS order_price, OrderID FROM OrderDetails JOIN Products ON OrderDetails.ProductID = Products.ProductID GROUP BY OrderID) as prices_order JOIN Orders ON prices_order.OrderID = Orders.OrderID GROUP BY EmployeeID) AS employee_sales JOIN Employees ON employee_sales.EmployeeID = Employees.EmployeeID;

105696.49999999999	Peacock	Margaret

8. Which employees have BS degrees? (*Hint:* look at the [LIKE](http://www.w3schools.com/sql/sql_like.asp) operator.)

SELECT LastName, FirstName FROM Employees WHERE Notes LIKE '%BS%';

Leverling	Janet
Buchanan	Steven

9. Which supplier of three or more products has the highest average product price? (*Hint:* look at the [HAVING](http://www.w3schools.com/sql/sql_having.asp) operator.)

SELECT COUNT(DISTINCT(ProductID)) AS num_prods, AVG(Price) AS avg_price, SupplierName FROM Products JOIN Suppliers ON Products.SupplierID = Suppliers.SupplierID GROUP BY SupplierName HAVING num_prods >= 3 ORDER BY avg_price DESC LIMIT 1;


num_prods	avg_price	SupplierName
3	46	Tokyo Traders


