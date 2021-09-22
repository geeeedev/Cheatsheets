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

