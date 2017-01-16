> **Challenge 1: Retrieve Customer Addresses**   
Customers can have two kinds of address: a main office address and a shipping address. The accounts
department want to ensure that the main office address is always used for billing, and have asked you to
write a query that clearly identifies the different types of address for each customer.

Tip: Review the documentation for the UNION operator in the Transact-SQL Reference.

####1. Retrieve billing addresses
Write a query that retrieves the company name, first line of the street address, city, and a column
named AddressType with the value ‘Billing’ for customers where the address type in the
SalesLT.CustomerAddress table is ‘Main Office’.
```sql
SELECT	c.CompanyName
		,a.AddressLine1
		,a.City
		,'Billing' AS AddressType		
FROM SalesLT.Customer AS c
JOIN SalesLT.CustomerAddress AS ca
	ON c.CustomerID = ca.CustomerID
	AND ca.AddressType = 'Main Office'
JOIN SalesLT.Address AS a
	ON a.AddressID = ca.AddressID
```
####2. Retrieve shipping addresses
Write a similar query that retrieves the company name, first line of the street address, city, and a
column named AddressType with the value ‘Shipping’ for customers where the address type in the
SalesLT.CustomerAddress table is ‘Shipping’.
```sql
SELECT	c.CompanyName
		,a.AddressLine1
		,a.City
		,'Shipping' AS AddressType		
FROM SalesLT.Customer AS c
JOIN SalesLT.CustomerAddress AS ca
	ON c.CustomerID = ca.CustomerID
	AND ca.AddressType = 'Shipping'
JOIN SalesLT.Address AS a
	ON a.AddressID = ca.AddressID
```
####3. Combine billing and shipping addresses
Combine the results returned by the two queries to create a list of all customer addresses that is sorted
by company name and then address type.
```sql
SELECT	c.CompanyName
		,a.AddressLine1
		,a.City
		,'Billing' AS AddressType		
FROM SalesLT.Customer AS c
JOIN SalesLT.CustomerAddress AS ca
	ON c.CustomerID = ca.CustomerID
	AND ca.AddressType = 'Main Office'
JOIN SalesLT.Address AS a
	ON a.AddressID = ca.AddressID
UNION ALL -- we can use ALL as there are no duplicates because of 'AddressType' column
SELECT	c.CompanyName
		,a.AddressLine1
		,a.City
		,'Shipping' AS AddressType		
FROM SalesLT.Customer AS c
JOIN SalesLT.CustomerAddress AS ca
	ON c.CustomerID = ca.CustomerID
	AND ca.AddressType = 'Shipping'
JOIN SalesLT.Address AS a
	ON a.AddressID = ca.AddressID
ORDER BY c.CompanyName, AddressType
```
