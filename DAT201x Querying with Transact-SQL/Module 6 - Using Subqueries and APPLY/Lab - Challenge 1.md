> **Challenge 1: Retrieve Product Price Information**   
Adventure Works products each have a standard cost price that indicates the cost of manufacturing the
product, and a list price that indicates the recommended selling price for the product. This data is stored
in the SalesLT.Product table. Whenever a product is ordered, the actual unit price at which it was sold is
also recorded in the SalesLT.SalesOrderDetail table. You must use subqueries to compare the cost and
list prices for each product with the unit prices charged in each sale.   

```
Tip: Review the documentation for subqueries in Subquery Fundamentals.
```
####1. Retrieve products whose list price is higher than the average unit price   
Retrieve the product ID, name, and list price for each product where the list price is higher than the
average unit price for all products that have been sold.
```sql
SELECT	ProductID
		,Name
		,ListPrice
FROM SalesLT.Product
WHERE ListPrice > (
					SELECT AVG(UnitPrice)
					FROM SalesLT.SalesOrderDetail
					)
```
####2. Retrieve Products with a list price of $100 or more that have been sold for less than $100   
Retrieve the product ID, name, and list price for each product where the list price is $100 or more, and
the product has been sold for less than $100.
```sql
SELECT	ProductID
		,Name
		,ListPrice
FROM SalesLT.Product
WHERE ListPrice >= 100 AND
      ProductID IN (
			SELECT ProductID
			FROM SalesLT.SalesOrderDetail
			WHERE UnitPrice < 100
			)
```
####3. Retrieve the cost, list price, and average selling price for each product   
Retrieve the product ID, name, cost, and list price for each product along with the average unit price for
which that product has been sold.
```sql
SELECT	p.ProductID
		,p.Name
		,p.StandardCost
		,p.ListPrice
		,(SELECT AVG(sod.UnitPrice)
		FROM SalesLT.SalesOrderDetail AS sod
		WHERE sod.ProductID = p.ProductID		
		) AS AverageSellingPrice
FROM SalesLT.Product AS p
```
####4. Retrieve products that have an average selling price that is lower than the cost   
Filter your previous query to include only products where the cost price is higher than the average
selling price
```sql
SELECT	p.ProductID
		,p.Name
		,p.StandardCost
		,p.ListPrice
		,(SELECT AVG(sod.UnitPrice)
		FROM SalesLT.SalesOrderDetail AS sod
		WHERE sod.ProductID = p.ProductID
		) AS AverageSellingPrice
FROM SalesLT.Product AS p
WHERE p.StandardCost > 
		(
		SELECT AVG(sod.UnitPrice)
		FROM SalesLT.SalesOrderDetail AS sod
		WHERE sod.ProductID = p.ProductID
		)
```
