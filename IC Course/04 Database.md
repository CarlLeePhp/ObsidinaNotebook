#### Entities:
- Staff
- Product
- Store
- Sales record
- HR manager

#### Home work
1. Picks up staff members who only associated one store.
2. Querry list staff names and number of stores their associated with.
3. Create some sales items, total cost of mutiple products. The number of product and amount of products cost.

- A function a number of stores of giving staff ID

#### Question 2 & 1
COUNT, GROUP BY, querry to table, LEFT JOIN
```sql
SELECT StaffId, FirstName, LastName, dbo.StaffType.Name AS StaffTypeName
FROM
(SELECT COUNT(StoreId) AS NumberOfStores, StaffId
FROM dbo.StoreStaff
GROUP BY StaffId) AS NumberOfStoresStaff
LEFT JOIN dbo.Staff
ON NumberOfStoresStaff.StaffId = dbo.Staff.Id
LEFT JOIN dbo.StaffType
ON dbo.Staff.StaffTypeId = dbo.StaffType.Id
WHERE NumberOfStores = 1;
```


#### Question 3
**I cannot add 2 same records into SaleProduct table, same product id for same sale.** 
Join 3 tables:
![[Pasted image 20230521202940.png]]

```sql
SELECT dbo.Product.Name, COUNT(dbo.Product.Name) AS Qty, SUM(dbo.Product.Price) AS Subtotal
FROM dbo.Sale LEFT OUTER JOIN
dbo.SaleProduct
ON dbo.Sale.Id = dbo.SaleProduct.SaleId
LEFT OUTER JOIN
dbo.Product
ON dbo.SaleProduct.ProductId = dbo.Product.Id
GROUP BY dbo.Product.Name;
```

#### Bonus
User Defined Function Syntaxes (Refer: https://www.sqlshack.com/learn-sql-user-defined-functions/)
```sql
CREATE FUNCTION [database_name.]function_name (parameters)
RETURNS data_type AS
BEGIN
    SQL statements
    RETURN value
END;
ALTER FUNCTION [database_name.]function_name (parameters)
RETURNS data_type AS
BEGIN
    SQL statements
    RETURN value
END;
DROP FUNCTION [database_name.]function_name;
```

How to use a function returning a table?
```sql
SELECT *
FROM dbo.udfNumberStoresByStaffId(1);
```