clean up:
just need formating and spacing for .md


- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 
# T-SQL Indexing Refresher
-  Follwing Articles: 
-  https://www.sqlshack.com/sql-query-performance-killers-understanding-poor-database-indexing/
-  https://www.sqlshack.com/poor-database-indexing-sql-query-performance-killer-recommendations/


##  Indexes: 
-  speed up data search and SQL query performance
-  reduce the number of data pages that have to be read in order to find the specific record
-  less reads are required to retrieve the records requested by a query or stored procedure 
-  Therefore, fewer disk I/O are preformed and the operation is completed faster

-  Biggest challenge with indexing: 
-  to determine the right ones for each table


##  Heap Table
-  A table without a clustered index is called a heap, due to its unordered structure. 
-  Data in a heap table isn’t sorted, usually the records are added one after another, 
-  as they are inserted into the table. 
-  They can also be rearranged by the database engine, but again, without a specific order. 
-  When you insert a lot of rows into a heap table, the new records are written on data pages 
-  without a specific order. 
-  When searching for a specific record in a heap table, SQL Server has to go through all table rows. 
-  Finding a record in a heap table can be compared to finding a specific leaf in a heap of leaves. 
-  It is inefficient and requires time.
-  As rows in a heap table are unordered, they are identified by a row identifier (RID) 
-  which consists of the file number, page number, and slot number of the row.
-  A heap can have one or several NONclustered indexes, or no indexes at all.


## Clustered Indexes
-  A clustered index organizes table data, so data is queried quicker and more efficiently. 
-  A clustered index consists of both index pages and data pages, 
-  while a heap table has no index pages; it consists only of data pages. 
-  In other words, a clustered index is not just an index, i.e. a pointer to the data row that contains the key value, 
-  but it also contains table data. The data in the clustered table is sorted using the values of the columns 
-  the clustered index is made of. 
-  Again, the data in the clustered table IS SORTED USING THE VALUES OF THE COLUMNS THE CLUSTERED INDEX IS MADE OF.
-  Finding a record from a table with a proper clustered index is quick and easy like 
-  finding a name in an alphabetically ordered list. 
-  A general recommendation for all SQL tables is to have a proper clustered index
-  With a proper clustered index, less reads are required to retrieve the records requested by a query or stored procedure. 
-  Therefore, fewer disk I/O are preformed and the operation is completed faster.
-  While there can be only one clustered index on a table, a table can have up to 999 nonclustered indexes
-  Both clustered and nonclustered indexes can be built from one or more table columns


## NonClustered Indexes
-  A nonclustered index is made of index pages that contain only row locators (pointers) for records in data pages. 
-  It doesn’t contain data pages, like clustered indexes.
-  Both clustered and nonclustered indexes can be built from one or more table columns

|              |   Heap Table    |   Clustered Index     |   NonClustered Index          |
|    ---       |   ---           |   ---                 |   ---                         |
| consists of: |   data pages    |   data pages          |                               |
|              |                 |  index pages          |   index pages (row pointers)  |


-  T-SQL Clustered Indexing Example
CREATE TABLE [Person].[Address](
    [AddressID] [int] IDENTITY(1,1) NOT FOR REPLICATION NOT NULL,
    [AddressLine1] [nvarchar](60) NOT NULL,
    [AddressLine2] [nvarchar](60) NULL,
    [City] [nvarchar](30) NOT NULL,
CONSTRAINT [PK_Address_AddressID] PRIMARY KEY CLUSTERED 
(
    [AddressID] ASC
) ON [PRIMARY]

-  When you execute the select statement on a clustered table where an ascending clustered index is created, 
-  the results will be ordered ascending by the clustered key column. In this example, it’s the AddressID column will be listed in order.
-  The same table, but with a descending clustered index will return the results sorted by the AddressID column descending.
CONSTRAINT [PK_Address_AddressID] PRIMARY KEY CLUSTERED 
(
	    [AddressID] DESC
) ON [PRIMARY]


-  T-SQL NONClustered Indexing Example
CREATE TABLE [Person].[Address4](
    [AddressID] [int] IDENTITY(1,1) NOT FOR REPLICATION NOT NULL,
    [AddressLine1] [nvarchar](60) NOT NULL,
    [AddressLine2] [nvarchar](60) NULL,
    [City] [nvarchar](30) NOT NULL)

CREATE NONCLUSTERED INDEX [IX_Address_StateProvinceID4] ON [Person].[Address4]
(
	[AddressID] ASC
) ON [PRIMARY]

-  When you execute the select statement on a heap table with the same columns and data, the results returned will be unordered.
-  So in this case, the AddressID column will be listed/printed out of order.

