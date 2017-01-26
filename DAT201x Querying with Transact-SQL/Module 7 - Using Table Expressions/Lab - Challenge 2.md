> **Challenge 2: Retrieve Customer Sales Revenue**
Each Adventure Works customer is a retail company with a named contact. You must create queries that
return the total revenue for each customer, including the company and customer contact names.

```
Tip: Review the documentation for the WITH common_table_expression syntax in the Transact-SQL
language reference.
```
####1. Retrieve sales revenue by customer and contact   
Retrieve a list of customers in the format Company (Contact Name) together with the total revenue for
that customer. Use a derived table or a common table expression to retrieve the details for each sales
order, and then query the derived table or CTE to aggregate and group the data.
```sql
WITH sales_CTE(CompanyContact, TotalDue)
AS
(
SELECT	CONCAT(c.CompanyName, '(', c.FirstName, c.LastName, ')')
		,soh.TotalDue
FROM SalesLT.Customer AS c
JOIN SalesLT.SalesOrderHeader AS soh
	ON c.CustomerID = soh.CustomerID
)

SELECT  CompanyContact
        ,SUM(TotalDue) AS TotalRevenue
FROM sales_CTE
GROUP BY CompanyContact
```
```sql
SELECT	CompanyContact
		,SUM(TotalDue) AS TotalRevenue
FROM
(
	SELECT	CONCAT(c.CompanyName, '(', c.FirstName, c.LastName, ')')
			,soh.TotalDue
	FROM SalesLT.Customer AS c
	JOIN SalesLT.SalesOrderHeader AS soh
		ON c.CustomerID = soh.CustomerID)
	AS Sales_DT(CompanyContact, TotalDue
)
GROUP BY CompanyContact
```
