> **Challenge 1: Generate Invoice Reports**   
Adventure Works Cycles sells directly to retailers, who must be invoiced for their orders. You have been
tasked with writing a query to generate a list of invoices to be sent to customers.

####1. Retrieve customer orders   
As an initial step towards generating the invoice report, write a query that returns the company name
from the SalesLT.Customer table, and the sales order ID and total due from the
SalesLT.SalesOrderHeader table.
```sql
SELECT	c.CompanyName
		,oh.SalesOrderID
		,oh.TotalDue 
FROM SalesLT.Customer AS c
INNER JOIN SalesLT.SalesOrderHeader AS oh
ON c.CustomerID = oh.CustomerID
```
####2. Retrieve customer orders with addresses   
Extend your customer orders query to include the Main Office address for each customer, including the
full street address, city, state or province, postal code, and country or region
```
Tip: Note that each customer can have multiple addressees in the SalesLT.Address table, so the
database developer has created the SalesLT.CustomerAddress table to enable a many-to-many
relationship between customers and addresses. Your query will need to include both of these tables,
and should filter the join to SalesLT.CustomerAddress so that only Main Office addresses are included.
```
```sql
SELECT	c.CompanyName
		,oh.SalesOrderID
		,oh.TotalDue 
		,a.AddressLine1
		,ISNULL(a.AddressLine2, '') AS AddressLine2
		,a.City
		,a.StateProvince
		,a.PostalCode
		,a.CountryRegion
FROM SalesLT.Customer AS c
INNER JOIN SalesLT.SalesOrderHeader AS oh
ON c.CustomerID = oh.CustomerID
JOIN SalesLT.CustomerAddress AS ca
ON c.CustomerID = ca.CustomerID
JOIN SalesLT.Address AS a
ON ca.AddressID = a.AddressID
WHERE ca.AddressType = 'Main Office'
```
