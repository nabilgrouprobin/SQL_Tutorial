- to create a table
```SQL
  CREATE TABLE EmployeeDetails
(
	EmployeeID int,
	FirstName varchar(50),
	LastName varchar(50),
	Age int,
	Gender varchar(50)
)
```
- to hard refresh   ` ctrl + shift + R `
- to insert data
```SQL
INSERT INTO EmployeeDetails VALUES 
('1001', 'Jim', 'Halpert', 30, 'Male')
```
- to insert multiple values
```SQL
INSERT INTO EmployeeDetails VALUES 
('1002', 'Abdur', 'Rouf', 29, 'Male'),
('1003', 'Pam', 'Beasley', 30, 'Female'),
('1004', 'Pan', 'Hook', 35, 'Female')
```
----------------------------------------------- SELECT ----------------------------------------------
- to select all data from a table named EmployeeDetails
```SQL
SELECT * 
FROM EmployeeDetails
```

- to select some coloumn (FirstName, LastName)  from table (EmployeeDetails)
```SQL
SELECT FirstName, LastName 
FROM EmployeeDetails
```
- to select top 2 values from table(EmployeeDetails) with column (FirstName, LastName)
```SQL
SELECT TOP 2 FirstName, LastName
  FROM SQLTutorial..EmployeeDetails
```
- if all rows and column needed then replace column name with *
- to select individual values in one column like (Gender, LastName, Age)
- DISTINCT shows `NULL` and `0` also
```SQL
SELECT DISTINCT(Gender)
  FROM SQLTutorial..EmployeeDetails
```
- to select rows number without null value in one column(Gender)
- COUNT ignore `NULL` bt counts `0` in counting
```SQL
SELECT COUNT(Gender)
  FROM SQLTutorial..EmployeeDetails
```
- to add a derived column name we use `AS`
```SQL
SELECT count(EmployeeID) AS EmployeeIDCount
  FROM SQLTutorial..EmployeeDetails
```
- or
```SQL
SELECT DISTINCT(Age) AS IndividualAgeNumber
  FROM SQLTutorial..EmployeeDetails
```
- to show maximum value in column(Age)
```SQL
SELECT MAX(Age)
FROM SQLTutorial..EmployeeDetails
```
- to show minimum value in column(Age)
```SQL
SELECT MIN(Age)
FROM SQLTutorial..EmployeeDetails
```
- to show average value in column(Age)
```SQL
SELECT AVG(Age)
FROM SQLTutorial..EmployeeDetails
```
----------------------------------------------- FROM ----------------------------------------------
- to `FROM` keyword we can locate our table initiating through out database name
```SQL
FROM EmployeeDetails 
FROM SQLTutorial.dbo.EmployeeDetails
FROM SQLTutorial..EmployeeDetails
```
----------------------------------------------- WHERE ----------------------------------------------
- to filter data with a criteria (FirstName = 'Abdur')
```SQL
SELECT *
FROM SQLTutorial..EmployeeDetails
WHERE FirstName = 'Abdur'
```
- some operator
```
Equal =
Not Equal <>
less than <
greater than >
less than equla <=
greater than equal >=
```
- some logical operator
```
WHERE Age = 30 AND Gender = 'Female'
WHERE Age = 30 OR Gender = 'Female' 
```
- we use `LIKE` for string operation mainly
- % (percent): Represents zero, one, or multiple characters.
- _ (underscore): Represents a single character.
```SQL
SELECT *
FROM SQLTutorial..EmployeeDetails
WHERE LastName LIKE 'R%'
```
- we can also use `NOT LIKE`
```SQL
SELECT *
FROM SQLTutorial..EmployeeDetails
WHERE LastName NOT LIKE 'R%'
```
- we can filter `NULL` values through WHERE statement
```SQL
SELECT *
FROM SQLTutorial..EmployeeDetails
WHERE EmployeeID is NULL
```
- we can also use `NOT NULL`
```SQL
SELECT *
FROM SQLTutorial..EmployeeDetails
WHERE EmployeeID is NOT NULL
```
- we use `IN` for like equal statement bt it is multiple equal statement
```
SELECT *
FROM SQLTutorial..EmployeeDetails
WHERE FirstName IN ('Rayem', 'Abdur')
```
----------------------------------------- Group By , Order By --------------------------------------
- to Group By Gender in Gender column and count it
```SQL
SELECT Gender, COUNT(Gender) AS CountGender
FROM SQLTutorial..EmployeeDetails
GROUP BY Gender
```
- we can also add filter in group by statement
```SQL
SELECT Gender, COUNT(Gender) AS CountGender
FROM SQLTutorial..EmployeeDetails
WHERE Age > 29
GROUP BY Gender
```
- we can set order in query by `ORDER BY` keywords has two method `ASC` or` DESC`
- default is `ASC`
```SQL
SELECT Gender, COUNT(Gender) AS CountGender
FROM SQLTutorial..EmployeeDetails
GROUP BY Gender
ORDER BY CountGender DESC
```
- we can do multiple column order
```SQL
SELECT *
FROM SQLTutorial..EmployeeDetails
ORDER BY Age DESC, Gender DESC
```
- we can also do it by column number
```SQL
SELECT *
FROM SQLTutorial..EmployeeDetails
ORDER BY 4 DESC, 5 DESC
```
----------------------------------------- JOIN ------------------------------------------------------
- join is to combine multiple tables
- `JOIN` denotes `INNER JOIN`
```SQL
SELECT *
FROM SQLTutorial..EmployeeDemographics dem
JOIN SQLTutorial..EmployeeSalary sal
 ON dem.EmployeeId = sal.EmployeeId
```
- Types of JOIN
 	- INNER
 	- LEFT OUTER
 	- RIGHT OUTER
 	- FULL OUTER
- Examples :
- LEFT OUTER JOIN
```SQL
SELECT *
FROM SQLTutorial..EmployeeDemographics dem
 LEFT OUTER JOIN SQLTutorial..EmployeeSalary sal
 ON dem.EmployeeId = sal.EmployeeId
```
- RIGHT OUTER JOIN
```SQL
SELECT *
FROM SQLTutorial..EmployeeDemographics dem
 RIGHT OUTER JOIN SQLTutorial..EmployeeSalary sal
 ON dem.EmployeeId = sal.EmployeeId
```
- FULL OUTER JOIN
```SQL
SELECT *
FROM SQLTutorial..EmployeeDemographics dem
FULL OUTER JOIN SQLTutorial..EmployeeSalary sal
 ON dem.EmployeeId = sal.EmployeeId
```
- IF we select any column which have same name in two tables we have to specify in join statement
```SQL
SELECT SQLTutorial..EmployeeDemographics.EmployeeId , FirstName, LastName
FROM SQLTutorial..EmployeeDemographics
FULL OUTER JOIN SQLTutorial..EmployeeSalary
 ON SQLTutorial..EmployeeDemographics.EmployeeId = SQLTutorial..EmployeeSalary.EmployeeId
```
- we can do it also by aliasing name
```SQL
SELECT dem.EmployeeId , FirstName, LastName
FROM SQLTutorial..EmployeeDemographics dem
FULL OUTER JOIN SQLTutorial..EmployeeSalary sal
 ON dem.EmployeeId = sal.EmployeeId
```
- We can use `ORDER BY` and `GROUP BY` in `JOIN` Operator
```SQL
SELECT JobTitle, AVG(Salary)
FROM SQLTutorial.dbo.EmployeeDemographics dem
FULL OUTER JOIN SQLTutorial..EmployeeSalary sal
 ON dem.EmployeeId = sal.EmployeeId
WHERE JobTitle = 'Salesman'
GROUP BY JobTitle
```
----------------------------------------- UNION, UNION ALL -------------------------------------------
- JOIN AND UNION are simmilar at combining two table and generate one Output.
- Differences : JOIN combines both table based on a common column (EmployeeId)
- Differences : UNION combines both table based on nothing
- UNION is like copy paste
- UNION is taking out and removing the duplicates
- UNION ALL is not removing duplicates
- UNION AND UNION ALL works where data types are similar and same number of columns
- Same data type and same number of column
- UNION
```SQL
SELECT EmployeeID, FirstName, Age FROM dbo.EmployeeDetails
UNION 
SELECT * FROM dbo.EmployeeSalary
```
- UNION ALL
```SQL
SELECT EmployeeID, FirstName, Age FROM dbo.EmployeeDetails
UNION ALL
SELECT * FROM dbo.EmployeeSalary
```
---------------------------------------- CASE STATEMENT ---------------------------------
- Case statement allows you specify condition and specify returns
- Case statement creates new column
- If various condition meet then the first one is executed
```SQL
SELECT EmployeeID, FirstName, LastName, Age, 
CASE
	WHEN Age > 27 AND Age <30 THEN 'MATURE'
	WHEN Age > 30 THEN 'OLD'
	ELSE 'BABY'
END
FROM DBO.EmployeeDetails
```
- AND
```SQL
SELECT DBO.EmployeeDetails.EmployeeID, FirstName, LastName, Department, Salary, 
CASE
	WHEN Department = 'Accounting' THEN Salary + (Salary * 0.5)
	WHEN Department = 'HR' THEN Salary + (Salary * 0.2)
	ELSE Salary + (Salary * 0.1)
END AS SalaryAfterRaise
FROM DBO.EmployeeDetails
JOIN DBO.EmployeeSalary ON DBO.EmployeeDetails.EmployeeID = DBO.EmployeeSalary.EmployeeID
```
----------------------------------- HAVING -----------------------------------------
- AN aggregate may not appear in the WHERE clause
- so we use Having
- HAVING Statement is completely depended on GROUP BY Statement So it is going under GROUP BY statement
```SQL
SELECT Age,  COUNT(Age)
FROM dbo.EmployeeDetails ed
GROUP BY Age
HAVING COUNT(Age) > 1
```
- AND
```SQL
SELECT  Age,  AVG(Salary)
FROM dbo.EmployeeDetails ed
JOIN dbo.EmployeeSalary es ON ed.EmployeeID = es.EmployeeID
GROUP BY Age
HAVING AVG(Salary) > 25
ORDER BY AVG(Salary)
```
------------------------------ UPDATE AND DELETE/REMOVE DATA ---------------------------------
- NORMAL QUERY
```SQL
UPDATE dbo.EmployeeSalary
SET Salary = 35000
WHERE EmployeeID = 1004
```
- MULTIPLE VALUE UPDATE
```SQL
UPDATE dbo.EmployeeSalary
SET Salary = 35000, Department = 'Admin'
WHERE EmployeeID = 1004
```
- DELETE
```SQL
DELETE dbo.EmployeeDetails
WHERE EmployeeID = 1004
```
- please before DELETE statement use SELECT statement to show what do you want to delete.
----------------------------------- ALIASING -----------------------------------------
- use for readability of SQL
- temporary changing the column name or table name
- we can use as or ' '
```SQL
SELECT FirstName + ' '+ LastName as FullName
FROM dbo.EmployeeDetails
```
- or
```SQL
SELECT FirstName + ' ' + LastName FullName
FROM dbo.EmployeeDetails
```
- we use aliasing when we use aggregate function
```SQL
SELECT AVG(Salary) as AvgSalary
FROM dbo.EmployeeSalary
```
- Aliasing Table Name
```SQL
SELECT sal.EmployeeID,  Salary
FROM dbo.EmployeeSalary as sal
JOIN dbo.EmployeeDetails as det ON sal.EmployeeID = det.EmployeeID
```
---------------------------------------- Partition By -----------------------------------------
- group by statement is going to reduce the number of rows in our output by rolling them up with some calculation 
- Aggregates data into summary rows (one row per group)
- Used with aggregate functions like SUM(), COUNT(), AVG(), MAX(), MIN().
- Divides the result set into partitions without reducing the number of rows
- Used with window functions like ROW_NUMBER(), RANK(), SUM() OVER(), etc
- Use GROUP BY when you want fewer rows with aggregated results.
- Use PARTITION BY when you want all rows with group-wise calculations
```SQL
SELECT FirstName, LastName, Gender, Salary, 
COUNT(Gender) OVER (PARTITION BY Gender) as TotalGender 
FROM dbo.EmployeeSalary as sal
JOIN dbo.EmployeeDetails as det ON sal.EmployeeID = det.EmployeeID

SELECT FirstName, LastName, Gender, Salary, 
COUNT(Gender) as TotalGender 
FROM dbo.EmployeeSalary as sal
JOIN dbo.EmployeeDetails as det ON sal.EmployeeID = det.EmployeeID
GROUP BY FirstName, LastName, Gender, Salary

SELECT  Gender, 
COUNT(Gender) as TotalGender 
FROM dbo.EmployeeSalary as sal
JOIN dbo.EmployeeDetails as det ON sal.EmployeeID = det.EmployeeID
GROUP BY Gender
```
-------------------------------- CTEs --------------------------------------------------------
- Common Table Expression
- use to manupulate complex subquery data
- very much like subquery
- CTE is called WITH Query
```SQL
WITH CTE_Employee as 
(
	SELECT FirstName, LastName, Gender, Salary,
	COUNT(Gender) OVER (PARTITION BY gender) as totalGender,
	AVG(Salary) OVER (PARTITION BY gender) as AvgSalary
	FROM dbo.EmployeeDetails det
	JOIN dbo.EmployeeSalary sal ON det.EmployeeID = sal.EmployeeID
	WHERE Age > 29
)
SELECT * 
FROM CTE_Employee
```
-------------------------------- Temp Tables --------------------------------------------
- temp tables is temporary tables
```SQL
CREATE TABLE #temp_Employee (
EmployeeID int,
JobTitle varchar(100),
Salary int
)
INSERT INTO #temp_Employee VALUES (
'1001', 'HR', '45000'
)
SELECT * 
FROM #temp_Employee
```
- we use if exists statement to more efficient
```SQL
DROP TABLE IF EXISTS #Temp_Employee2
CREATE TABLE #Temp_Employee2 (
JobTitle varchar(50),
EmployeesPerJob int,
AvgAge int,
AvgSalary int
	)

INSERT INTO #Temp_Employee2 
SELECT Department, COUNT(Department), AVG(Age),Avg(Salary)
FROM dbo.EmployeeSalary sal
JOIN dbo.EmployeeDetails  det ON sal.EmployeeID = det.EmployeeID
GROUP BY Department

SELECT * 
FROM #Temp_Employee2
```
--------------------- STRING FUNCTION ----------------------------------------------------
- TRIM, LTRIM, RTRIM, REPLACE, SUBSTRING, UPPER, LOWER
```SQL
CREATE TABLE EmployeeErrors (
EmployeeID varchar(50),
FirstName varchar(50),
LastName varchar(50)
)

INSERT INTO EmployeeErrors VALUES
('1001   ', 'Jimbo', 'Halbert'),
('  1002','Pamela', 'Basely'),
('1005', 'T0by', 'Flenderson - Fired' )

SELECT * 
FROM EmployeeErrors

SELECT EmployeeID, TRIM(EmployeeID) as IDTRIM
FROM EmployeeErrors

SELECT EmployeeID, LTRIM(EmployeeID) as IDTRIM
FROM EmployeeErrors

SELECT EmployeeID, RTRIM(EmployeeID) as IDTRIM
FROM EmployeeErrors

SELECT LastName, REPLACE(LastName, '- Fired', '') as LastNameFixed
FROM EmployeeErrors

SELECT FirstName, SUBSTRING(FirstName, 1, 3) as Substring
FROM EmployeeErrors

SELECT FirstName, SUBSTRING(FirstName, 3, 3) as Substring
FROM EmployeeErrors

SELECT LastName, LOWER(LastName)
FROM EmployeeErrors

SELECT LastName, UPPER(LastName)
FROM EmployeeErrors
```
------------------- Stored Procedures -------------------------------------------------------
- Stored Procedure is a group of SQL Statement that has been created and stored in the database
- Stored procedure can accept input parameters
- Single Stored Procedure can be used over the network by several different users with different input data
- Reduce the traffic and increase the performance
- Modified data can automatically updated for all users
- A Stored Procedure is a precompiled collection of one or more SQL statements stored in the database.
- Performance: Precompiled and cached, reducing parsing and compilation time.
- Reusability: Write once and call multiple times.
- Security: Grant permission to execute procedures without exposing underlying tables.
- Maintainability: Centralized business logic simplifies updates.
- Example 1: Simple Stored Procedure Without Parameters
```SQL
CREATE PROCEDURE GetAllEmployees
AS
BEGIN
    SELECT * FROM Employees;
END;


EXEC GetAllEmployees;
```
- Example 2: Stored Procedure With Parameters
```SQL
CREATE PROCEDURE GetEmployeeByID
    @EmployeeID INT
AS
BEGIN
    SELECT * FROM Employees WHERE EmployeeID = @EmployeeID;
END;


EXEC GetEmployeeByID @EmployeeID = 5;

```
- Example 3: Stored Procedure With Input and Output Parameters
```SQL
CREATE PROCEDURE GetEmployeeName
    @EmployeeID INT,
    @EmployeeName NVARCHAR(100) OUTPUT
AS
BEGIN
    SELECT @EmployeeName = EmployeeName FROM Employees WHERE EmployeeID = @EmployeeID;
END;

DECLARE @Name NVARCHAR(100);
EXEC GetEmployeeName @EmployeeID = 3, @EmployeeName = @Name OUTPUT;
PRINT @Name;
```
- Example 4: Stored Procedure With Transactions and Error Handling
```SQL
CREATE PROCEDURE UpdateEmployeeSalary
    @EmployeeID INT,
    @NewSalary DECIMAL(10,2)
AS
BEGIN
    BEGIN TRY
        BEGIN TRANSACTION;
        
        UPDATE Employees
        SET Salary = @NewSalary
        WHERE EmployeeID = @EmployeeID;

        COMMIT TRANSACTION;
    END TRY
    BEGIN CATCH
        ROLLBACK TRANSACTION;
        PRINT 'Error occurred while updating salary.';
    END CATCH
END;

```

- Modifying and Dropping Stored Procedures
```SQL
-- Modify a stored procedure
ALTER PROCEDURE ProcedureName
AS
BEGIN
    -- Updated SQL code
END;

-- Drop a stored procedure
DROP PROCEDURE ProcedureName;

```








