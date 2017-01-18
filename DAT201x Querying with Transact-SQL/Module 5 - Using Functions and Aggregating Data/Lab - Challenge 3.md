> **Challenge 3: Aggregate Product Sales**
The product manager would like aggregated information about product sales.

```
Tip: Review the documentation for the GROUP BY clause in the Transact-SQL Reference.
```
####1. Retrieve total sales by product
Write a query to retrieve a list of the product names and the total revenue calculated as the sum of the
LineTotal from the SalesLT.SalesOrderDetail table, with the results sorted in descending order of total
revenue.
```sql
SELECT	p.Name
		,SUM(sod.LineTotal) AS TotalRevenue
FROM SalesLT.Product AS p
JOIN SalesLT.SalesOrderDetail AS sod
	ON p.ProductID = sod.ProductID
GROUP BY p.Name
ORDER BY TotalRevenue DESC
```
####2. Filter the product sales list to include only products that cost over $1,000
Modify the previous query to include sales totals for products that have a list price of more than $1000.
```sql

```
####3. Filter the product sales groups to include only total sales over $20,000
Modify the previous query to only include only product groups with a total sales value greater than
$20,000.
```sql

```
