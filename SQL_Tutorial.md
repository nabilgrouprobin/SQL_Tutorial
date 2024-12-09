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


