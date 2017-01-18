> **Challenge 2: Rank Customers by Revenue**   
The sales manager would like a list of customers ranked by sales.

```
Tip: Review the documentation for Ranking Functions in the Transact-SQL Reference.
```
####1. Retrieve companies ranked by sales totals   
Write a query that returns a list of company names with a ranking of their place in a list of highest
TotalDue values from the SalesOrderHeader table
```sql
SELECT	c.CompanyName
		,oh.TotalDue
		,RANK() OVER(ORDER BY oh.TotalDue DESC) AS Rank
FROM SalesLT.Customer AS c
JOIN SalesLT.SalesOrderHeader AS oh
	ON c.CustomerID = oh.CustomerID
```
