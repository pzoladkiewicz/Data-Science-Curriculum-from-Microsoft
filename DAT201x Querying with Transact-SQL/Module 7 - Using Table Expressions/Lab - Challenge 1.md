> **Challenge 1: Retrieve Product Information**   
Adventure Works sells many products that are variants of the same product model. You must write
queries that retrieve information about these products

####1. Retrieve product model descriptions   
Retrieve the product ID, product name, product model name, and product model summary for each
product from the SalesLT.Product table and the SalesLT.vProductModelCatalogDescription view.
```sql
SELECT	p.ProductID
		,p.Name AS ProductName
		,vPMCD.Name AS ProductModel
		,vPMCD.Summary AS Description
FROM SalesLT.Product AS p
JOIN SalesLT.vProductModelCatalogDescription AS vPMCD
	ON p.ProductModelID = vPMCD.ProductModelID
ORDER BY p.ProductID
```
####2. Create a table of distinct colors   
```
Tip: Review the documentation for Variables in Transact-SQL Language Reference.
```
Create a table variable and populate it with a list of distinct colors from the SalesLT.Product table. Then
use the table variable to filter a query that returns the product ID, name, and color from the
SalesLT.Product table so that only products with a color listed in the table variable are returned.
```sql
DECLARE @Kolor AS TABLE
(Color nvarchar(15))

INSERT INTO @Kolor(Color)
	SELECT DISTINCT Color
	FROM SalesLT.Product

SELECT	ProductID
		,Name
		,Color
FROM SalesLT.Product
WHERE Color IN (SELECT Color FROM @Kolor)
```
####3. Retrieve product parent categories   
The AdventureWorksLT database includes a table-valued function named dbo.ufnGetAllCategories,
which returns a table of product categories (for example ‘Road Bikes’) and parent categories (for
example ‘Bikes’). Write a query that uses this function to return a list of all products including their
parent category and category.
```sql

```
