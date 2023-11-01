# dba_questions
A list of interview question and answers I have had to answer.

## General 
Not platform specific.

Q: Explain ACID acronym?

A: - Atomicity: Either the entire statement is executed, or none of it is executed
   - Consistency: Transactions only make changes to tables in predefined, predictable ways. 
   - Isolation:  Concurrent transactions don't interfere with or affect one another. 
   - Durability: Guarantee that changes to your data made by successfully executed transactions will be saved
     
Q: What are the SQL isolation levels?

A: - Read Committed: SELECT only returns committed rows.
   - Read Uncommitted: SELECT returns rows from uncommitted transactions.
   - Repeatable Read: Both writes and reads transactions are locked to prevent reading by other transactions.
   - Serializable: Transactions are performed sequentially
     
Q: Explain clustered indexes.

A: A unique index stored in a sequential order.  Data is stored in the index.  Non-clustered index stores a pointer to the data.
   [Nice explanation](https://www.geeksforgeeks.org/difference-between-clustered-and-non-clustered-index/)
   
Q: Name the common SQL data types.  (I was thrown by this one. What they wanted was the simplest answer. I was thinking about unix epoch, timestamp, uuid, cidr, money, json...)

A: - Numeric. Decimal, integer, float, etc.
   - Date and time. unix timestamp, time, date, etc.
   - String/Character.  ASCII characters, Json included.
   - Unicode. The wild west!
   - Binary blob. Potentially includes geography types!
[Decent explanation](https://www.digitalocean.com/community/tutorials/sql-data-types)

## MySQL

## Microsoft_SQL


## PostgreSQL


