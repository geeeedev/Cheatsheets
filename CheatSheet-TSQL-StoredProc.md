- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
# T-SQL Stored Procedure Refresher
-  Follwing Articles: 
-  https://www.pluralsight.com/guides/writing-t-sql-stored-procedures
-  https://www.pluralsight.com/guides/introduction-tsql-querying
-  https://www.pluralsight.com/guides/writing-select-queries
-  https://www.pluralsight.com/guides/querying-multiple-tables
-  https://www.sqlservertutorial.net/sql-server-basics/sql-server-insert-into-select/
-  https://docs.microsoft.com/en-us/sql/relational-databases/triggers/use-the-inserted-and-deleted-tables?view=sql-server-ver15
-  https://www.educba.com/sql-keywords/  


1. stored proc supports input and output parameters
1. stored proc can return rows of data or single values
1. batch statement uses the GO; separator

##  Two types of stored proc: System Stored Proc & Extended Stored Proc
-  System Stored Proc
    -  written in T-SQL
    -  found in the master database with every SQL Server installation
-  Extended Stored Proc
    - written in native code C++
    - supplied via a dynamic-link library


###  Create Stored Proc
```sql
CREATE PROCEDURE procedure_name
AS
sql_statement
GO;
```

###  Update exisiting Stored Proc
-  alter explicitely using ALTER PROCEDURE or drop and recreate stored procedure
```sql
ALTER PROCEDURE procedure_name
AS
sql_statement
GO;
```

###  Execute Stored Proc
-  qualify the procedure name with the schema name to improve performance
```sql
EXECUTE schemaName.procedure_name;
```

###  Delete Stored Proc
-  remove the procedure from the database
```sql
DROP PROCEDURE schemaName.procedure_name;
```
>  to drop an extended  stored proc, use sp_dropextendedproc


###  Parameterized Stored Proc
-  allow to pass values in and out of stored proc, making it reusable
-  Input Parameters
```sql
CREATE PROCEDURE getEmployeeDetails
@empid int
AS
    select name, address, phone
    from employee
    where employeeid = @empid;
GO;
```

###  Output Parameters
-  must specify the OUTPUT keyword in both the Create stmt and the Execute stmt
```sql
CREATE PROCEDURE getEmployeeName
@empid INT
@empName VARCHAR(50) OUTPUT
AS
BEGIN
    select @empName = name
    from employee
    where employeeid = @empid;
END
GO;

DECLARE @retrievedEmpName VARCHAR(50)
EXECUTE schemaName.getEmployeeName @empName = @retrievedEmpName OUTPUT
selet @retrievedEmpName
```

###  Insert Into Select example
-  https://www.sqlservertutorial.net/sql-server-basics/sql-server-insert-into-select/
```sql
INSERT INTO sales.addresses (street, city, state, zip_code) 
SELECT
    street,
    city,
    state,
    zip_code
FROM
    sales.customers
WHERE
    city IN ('Santa Cruz', 'Baldwin')
ORDER BY
    first_name,
    last_name; 
```
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
Example: Table of Employees  
| id   |  name  | address   | age   | phone      |
| ---  |  ---   | ---       | ---   | ---        |
| 1    |  dom   | USA       | 35    | 1111111111 | 
| 2    |  brian | USA       | 30    | 2222222222 | 
| 3    |  letty | USA       | 32    | 3333333333 | 


```sql
CREATE TABLE employee (
    id int,
    name varchar(50),
    age int,
    address varchar(100),
    phone varchar(10)
); 
GO;
```

###  multiple insert at a time is limited to 1000 rows
```sql
INSERT INTO employee VALUES 
(1,'dom',35,'USA','1111111111'),
(2,'brain',30,'USA','2222222222'),
(3,'letty',32,'USA','3333333333');

-- or

INSERT INTO employee (                  --  id is auto applied; specifying the list of fields to match
    name,
    age,
    address,
    phone
) 
OUTPUT inserted.id, inserted.name       --  inserted.???
VALUES 
('dom',35,'USA','1111111111'),
('brain',30,'USA','2222222222'),
('letty',32,'USA','3333333333');

select * from employee;
```


> Trigger Example:  
> https://docs.microsoft.com/en-us/sql/relational-databases/triggers/use-the-inserted-and-deleted-tables?view=sql-server-ver15

> SQL Keywords:  
> https://www.educba.com/sql-keywords/



####  Example 1: A stored procedure that returns a list of peopele older than 31 yrs old
```sql
CREATE PROCEDURE getmployeeByAge
AS
BEGIN
    select * 
    from employee
    where age > 31
END
GO;

EXECUTE dbo.getmployeeByAge;
```

####  Example 2: Modify the above procedure to take age as a parameter 
```sql
ALTER PROCEDURE getmployeeByAge
    @ageLimit int
AS
BEGIN
    select * 
    from employee
    where age > @ageLimit
END
GO;
```

