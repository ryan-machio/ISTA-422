# Ryan Manchanthasouk
## TSQL Chapter 9
## March 31st, 2020
1. What is a temporal table?
  - A temporal table is a type of table designed to keep a full history of data changes and allow easy point in time analysis.
2. Under what circumstances would you use a temporal table? Temporal tables are in widespread use in certain kinds of businesses.
  - When you want to audit, point-in-time analysis, comparing current states with older states.
3. What are the semantics of a temporal table? There are seven of them.
  - primary key
  - two columns defined as datetime2 with any precision, which are non-nullable and represent the start and end of the row's validity period in the UTC time zone
  - a start column that should be marked with the option GENERATED ALWAYS AS ROW start
  - a designation of the period columns with the option PERIOD FOR SYSTEM_TIME (<startcol>, <endcol>)
  - The table option SYSTEM.VERSIONING, which should be set to ON
  - A linked history table (which SQL Server can create for you) to hold the past states of modified rows.
4. How do you search a history table?
  - the same way you would search a normal table
5. How do you modify a history table?
  - Modify current table with INSERT, UPDATE, DELETE, and MERGE statements.  SQL Server updates the period columns and moves rows to the history table as needed.
6. How do you delete date from a history table? Why would you want to delete data from a history table?
  - DELETE FROM history.table
  - WHERE value = #;
  - You would delete a date from the history table when you want to move the old version of the row to the history table with the transaction time as the period end time and keep the current version of the row in the curren table with the transaction time as the period start time and maximum value in the type as the period end time.
7. How do you search a history table?
  - The same way you search a normal table
8. How do you query all data from both a history file and the current data?
  - You query the current table, but you add the clause called FOR SYSTEM_TIME and a subclause that indicates the validity point or period of time you're interested in.
9. How do you drop a temporal table?
  - DROP TABLE IF EXISTS temporalTable;
