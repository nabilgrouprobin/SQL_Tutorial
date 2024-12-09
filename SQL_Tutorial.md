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
-----------------------------------------Group By , Order By --------------------------------------
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

