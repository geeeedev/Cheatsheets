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


