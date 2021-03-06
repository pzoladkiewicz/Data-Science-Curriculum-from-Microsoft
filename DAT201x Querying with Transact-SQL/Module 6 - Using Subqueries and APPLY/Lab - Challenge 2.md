> **Challenge 2: Retrieve Customer Information**   
The AdventureWorksLT database includes a table-valued user-defined function named
dbo.ufnGetCustomerInformation. You must use this function to retrieve details of customers based on
customer ID values retrieved from tables in the database.

```
Tip: Review the documentation for the APPLY operator in Using APPLY.
```
####1. Retrieve customer information for all sales orders   
Retrieve the sales order ID, customer ID, first name, last name, and total due for all sales orders from
the SalesLT.SalesOrderHeader table and the dbo.ufnGetCustomerInformation function.
```sql
SELECT	soh.SalesOrderID
		,func.CustomerID
		,func.FirstName
		,func.LastName
		,soh.TotalDue
FROM SalesLT.SalesOrderHeader AS soh
CROSS APPLY dbo.ufnGetCustomerInformation(soh.CustomerID) AS func
```
####2. Retrieve customer address information   
Retrieve the customer ID, first name, last name, address line 1 and city for all customers from the
SalesLT.Address and SalesLT.CustomerAddress tables, and the dbo.ufnGetCustomerInformation
function.
```sql
SELECT	ca.CustomerID
		,func.FirstName
		,func.LastName
		,a.AddressLine1
		,a.City
FROM SalesLT.Address AS a
JOIN SalesLT.CustomerAddress AS ca
	ON a.AddressID = ca.AddressID
CROSS APPLY dbo.ufnGetCustomerInformation(ca.CustomerID) AS func
```
