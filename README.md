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

Q: What does the term sargeable describe?

- Root of the term is an acroynm  for "search arguments." SARG
- A thorough answer is complicated.  [Good explanation](https://dba.stackexchange.com/questions/162263/what-does-the-word-sargable-really-mean)
- A simple answer: When a query uses index features/properties in the WHERE clause.  WHERE UPPER(FIRST_NAME) like 'R%' vs WHERE FIRST_NAME like 'r%'. The former has to UPPER(FIRST_NAME) all rows before deciding, unable to use an index.  The latter uses the index and seeks. 


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

Q: Define replication lag.

- The difference between the timestamps of the relay log most recently executed on the secondary, versus the relay log entry most recently downloaded by the IO_THREAD on the secondary.

Q: Are there other ways replication can be blocked?

Yes.  

- If the replica behind a whole binlog, the lag isn't shown. Not really a "block" but more unreported lag.
- If the primary table is exclusively locked for a long period of time.  An example is DDL on a giant table.
- Statement based replication can be slower on busy servers, but, be careful with blindly switching to mixed. Your Kafka admin might have words!
- Networking issues.

Q: How to show database uptime?

- SHOW GLOBAL STATUS LIKE 'Uptime'; (in seconds)
- SELECT ROUND(@d:=VARIABLE_VALUE/60/60/24) AS days, ROUND(@d/30.5) AS months FROM performance_schema.global_status WHERE VARIABLE_NAME = 'Uptime';
  I like rounding. Stolen from stackoverflow.

Q: Can minor version updates break an application.

Yes. Absolutely.

Q: Describe ways to tune a mysql database.

- Turn on slow_query_log = 1 and log_output=TABLE.  Remember to set long_query_time = $WHATEVER
- Dealing with many connections, open_files_limit may need to be increased.
- Increase the number of client connections allowed with max_connections.
- VERY reluctant to tune innodb defaults. (YMMV)
- Alter Buffer_pool size to be a little more than the total size of database in RAM.  The 80% rule used to work.  Now it's more like 95%. Cgroups is your friend!
- join_buffer size. Change during session for large joins.
- sort_buffer size. Change during session and experiment, heavily.
- tmp_dir. Not a huge optimization. Very handy for large table operations.

Q: What's a fast way to fix too many connections error?

- TRUNCATE TABLE performance_schema.host_cache; Or, in the old days, FLUSH HOSTS.

Q: Find longest running query and kill it.

- SHOW PROCESS LIST
- Typically looking for "SELECT * FROM.." type queries.
- Get the process number.
- KILL the process id. 

Q: Is AWS Aurora a real MySQL database?

- Yes, because it acts almost exactly like a MySQL database.  Interviewer disagreed with me.  It isn't "real."  

- Yes, that really happened.  The interview did not get better.



## Microsoft_SQL


## PostgreSQL
Q: Interviewer wants two PostgreSQL servers in active/passive configuration in geographically distant data centers, and without VRRP, to failover in less than a second and not lose transactions.  How would you do that?

- I said client connection pooling and client health checks.  They didn't want that. 

Q: Interviewer wants two PostgreSQL servers in active/active configuration in geographically distant data centers to double the amount of transactions the database can process.

- Yes, that really happened.

