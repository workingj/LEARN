# SQL

- [SQL](#sql)
  - [Constraints](#constraints)
  - [SQL Operators](#sql-operators)
    - [SQL Logical Operators](#sql-logical-operators)
    - [SQL Arithmetic Operators](#sql-arithmetic-operators)
    - [SQL Comparison Operators](#sql-comparison-operators)
    - [SQL Compound Operators](#sql-compound-operators)
    - [SQL Bitwise Operators](#sql-bitwise-operators)
  - [Comments](#comments)
  - [SQL Statement](#sql-statement)
    - [CREATE TABLE](#create-table)
    - [ALTER TABLE](#alter-table)
    - [DROP TABLE](#drop-table)
    - [INSERT INTO](#insert-into)
    - [SELECT](#select)
    - [SELECT DISTINCT](#select-distinct)
    - [SELECT INTO](#select-into)
    - [UPDATE](#update)
    - [DELETE FROM](#delete-from)
    - [AS](#as)
    - [WHERE](#where)
    - [LIKE](#like)
    - [IS NULL](#is-null)
    - [IS NOT NULL](#is-not-null)
    - [BETWEEN](#between)
    - [OR](#or)
    - [ORDER BY](#order-by)
    - [LIMIT, SELECT TOP and ROWNUM](#limit-select-top-and-rownum)
    - [CASE](#case)

## Constraints

- `NOT NULL` - Ensures that a column cannot have a `NULL` value
- `UNIQUE` - Ensures that all values in a column are different
- `PRIMARY KEY` - A combination of a `NOT NULL` and `UNIQUE`. Uniquely identifies each row in a table
- `FOREIGN KEY` - Prevents actions that would destroy links between tables
- `CHECK` - Ensures that the values in a column satisfies a specific condition
- `DEFAULT` - Sets a default value for a column if no value is specified
- `CREATE INDEX` - Used to create and retrieve data from the database very quickly

## SQL Operators

### SQL Logical Operators

- `ALL` `TRUE` if all of the subquery values meet the condition
- `AND` `TRUE` if all the conditions separated by `AND` is `TRUE`
- `ANY` `TRUE` if any of the subquery values meet the condition
- `BETWEEN` `TRUE` if the operand is within the range of comparisons
- `EXISTS` `TRUE` if the subquery returns one or more records
- `IN` `TRUE` if the operand is equal to one of a list of expressions
- `LIKE` `TRUE` if the operand matches a pattern
- `NOT` Displays a record if the condition(s) is `NOT TRUE`
- `OR` `TRUE` if any of the conditions separated by `OR` is `TRUE`
- `SOME` `TRUE` if any of the subquery values meet the condition

### SQL Arithmetic Operators

- `+` Add
- `-` Subtract
- `*` Multiply
- `/` Divide
- `%` Modulo

### SQL Comparison Operators

- `=` Equal to
- `>` Greater than
- `<` Less than
- `>=` Greater than or equal to
- `<=` Less than or equal to
- `<>` Not equal to

### SQL Compound Operators

- `+=` Add equals
- `-=` Subtract equals
- `*=` Multiply equals
- `/=` Divide equals
- `%=` Modulo equals
- `&=` Bitwise `AND` equals
- `^-=` Bitwise exclusive equals
- `|*=` Bitwise `OR` equals

### SQL Bitwise Operators

- `&` Bitwise `AND`
- `|` Bitwise `OR`
- `^` Bitwise exclusive `OR`

## Comments

```sql
--SELECT * FROM Customers;
SELECT * FROM Products;
```

```sql
 SELECT * FROM Customers -- WHERE City='Berlin'; 
```

```sql
/*Select all the columns
of all the records
in the Customers table:*/
SELECT * FROM Customers;
```

## SQL Statement

### CREATE TABLE

```sql
CREATE TABLE awards (
    id INTEGER PRIMARY KEY,
    recipient TEXT NOT NULL,
    award_name TEXT DEFAULT 'Grammy'
);
```

### ALTER TABLE

- changes an existing table.

```sql
ALTER TABLE table_name
ADD column_name datatype

ALTER TABLE Customers
ADD Email varchar(255);
```

```sql
ALTER TABLE table_name
DROP COLUMN column_name
```

```sql
ALTER TABLE table_name
ALTER COLUMN column_name year;
```

### DROP TABLE

```sql
DROP TABLE table_name
```

### INSERT INTO

```sql
INSERT INTO table_name
VALUES (value1, value2, value3,....)
--or
INSERT INTO table_name
(column1, column2, column3,...)
VALUES (value1, value2, value3,....)
```

### SELECT

- queries data from a table.

```sql
SELECT * FROM Customers;

SELECT CustomerName, City FROM Customers;
```

### SELECT DISTINCT

- acts like a filter
- command returns only distinct (different) values

```sql
SELECT DISTINCT Country FROM Customers;
```

### SELECT INTO

- copies data from one table and inserts it into a new table

```sql
SELECT * INTO CustomersBackup2017
FROM Customers; 

SELECT CustomerName, ContactName INTO CustomersBackup2024
FROM Customers; 
```

- in an other data base

```sql
SELECT * INTO CustomersBackup2017 IN 'Backup.mdb'
FROM Customers;  
```

### UPDATE

- edits a row in a table.

```sql
UPDATE Customers
SET ContactName = 'Alfred Schmidt', City= 'Frankfurt'
WHERE CustomerID = 1;
```

### DELETE FROM

- deletes rows from a table.

```sql
DELETE FROM Customers WHERE CustomerName='The Dings';
```

### AS

- used to rename a column or table with an alias.
- alias exists for the duration of the query

```sql
SELECT CustomerName AS Customer, ContactName AS [Contact Person]
FROM Customers; 
```

```sql
SELECT CustomerName, Address + ', ' + PostalCode + ' ' + City + ', ' + Country AS Address
FROM Customers;
```

### WHERE

- filters a result set to include only records that fulfill a specified condition

```sql
SELECT * FROM Customers
WHERE CustomerID=1; 
```

- coditional

```sql
SELECT * FROM Customers
WHERE (logical and comparison operators);
```

### LIKE

- used in a WHERE clause to search for a specified pattern in a column

- `%` - Represents zero, one, or multiple characters
- `_` - Represents a single character (MS Access uses a question mark (?) instead)

```sql
SELECT * FROM Customers
WHERE CustomerName LIKE 'a%'; 

SELECT * FROM Customers
WHERE CustomerName LIKE 'a__%';

SELECT * FROM Customers
WHERE CustomerName LIKE '%or%';
```

### IS NULL

- used to test for empty values

```sql
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NULL;
```

### IS NOT NULL

- used to test for non-empty values

```sql
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NOT NULL;
```

### BETWEEN

- used to select values within a given range
- the values can be numbers, text, or dates
- it's inclusive: begin and end values are included.

```sql
Get your own SQL Server
SELECT * FROM Products
WHERE Price BETWEEN 10 AND 20;

SELECT * FROM Products
WHERE ProductName BETWEEN 'Carnarvon Tigers' AND 'Mozzarella di Giovanni'
ORDER BY ProductName;
```

### OR

- used with WHERE to include rows where either condition is true

```sql
SELECT *
FROM movies
WHERE genre = 'romance'
   OR genre = 'comedy';
```

### ORDER BY

- used to specify the number of records to return

```sql
SELECT * FROM Customers
ORDER BY CustomerName; 

SELECT * FROM Customers
ORDER BY CustomerName ASC; 

SELECT * FROM Customers
ORDER BY CustomerName DESC; 
```

### LIMIT, SELECT TOP and ROWNUM

- SQL Server uses SELECT TOP. MySQL uses LIMIT, and Oracle uses ROWNUM

```sql
SELECT * FROM Customers
LIMIT 3; 
```

### CASE

- used is to create different output based on conditions

```sql
SELECT name,
 CASE
  WHEN genre = 'romance' THEN 'Chill'
  WHEN genre = 'comedy' THEN 'Chill'
  ELSE 'Intense'
 END AS 'Mood'
FROM movies;

--or

SELECT OrderID, Quantity,
CASE
    WHEN Quantity > 30 THEN 'The quantity is greater than 30'
    WHEN Quantity = 30 THEN 'The quantity is 30'
    ELSE 'The quantity is under 30'
END
FROM OrderDetails;

-- or

SELECT CustomerName, City, Country
FROM Customers
ORDER BY
(CASE
    WHEN City IS NULL THEN Country
    ELSE City
END); 
```
