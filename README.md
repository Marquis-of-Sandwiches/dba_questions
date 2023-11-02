# dba_questions
A list of interview question and answers I have had to answer.

## General 
Not platform specific.

Q: Explain ACID acronym?

   - Atomicity: Either the entire statement is executed, or none of it is executed
   - Consistency: Transactions only make changes to tables in predefined, predictable ways. 
   - Isolation:  Concurrent transactions don't interfere with or affect one another. 
   - Durability: Guarantee that changes to your data made by successfully executed transactions will be saved
     
Q: What are the SQL isolation levels?

- Read Committed: SELECT only returns committed rows.
- Read Uncommitted: SELECT returns rows from uncommitted transactions.
- Repeatable Read: Both writes and reads transactions are locked to prevent reading by other transactions.
- Serializable: Transactions are performed sequentially
     
Q: Explain clustered indexes.

- A unique index stored in a sequential order.  Data is stored in the index.  
    Non-clustered index stores a pointer to the data.
    
   [Nice explanation](https://www.geeksforgeeks.org/difference-between-clustered-and-non-clustered-index/)
   
Q: Name the common SQL data types.  (I was thrown by this one. What they wanted was the simplest answer. I was thinking about unix epoch, timestamp, uuid, cidr, money, json...)

- Numeric. Decimal, integer, float, etc.
- Date and time. unix timestamp, time, date, etc.
- String/Character.  ASCII characters, Json included.
- Unicode. The wild west!
- Binary blob. Potentially includes geography types!
     
[Decent explanation](https://www.digitalocean.com/community/tutorials/sql-data-types)

## MySQL
Q: How do you install MySQL? (Not a kubernetes shop.  Also not automated)

- Boot the VM/machine into the installer.
- Install Debian, customize disk mounts, secrets, whatever.
- Reboot
- Promote yourself to root and perhaps install a Mariadb repo, Oracle repo, whatever.
- Apt update
- Apt install packages.
- Modify /etc/mysql/conf.d/mysqld.cnf to use external storage, tune as needed.
- Make sure the service is enabled to start on boot.
- Start mysql.
- Check to see if it's running.  Fix any syntax issues.
 
## Microsoft_SQL


## PostgreSQL
Q: I want two PostgreSQL servers in active/passive configuration in geographically distant data centers, and without VRRP, to failover in less than a second and not lose transactions.  How would you do that?

Q: I want two PostgreSQL servers in active/active configuration in geographically distant data centers to double the amount of transactions the database can process.

- Yes, that really happened.

