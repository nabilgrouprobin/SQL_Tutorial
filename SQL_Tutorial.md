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
- 

