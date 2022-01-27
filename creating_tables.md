# Creating Tables

## CREATE TABLE <span style="color:green">**Syntax**</span>

![](Images/database.png)

CREATE [TEMPORARY] TABLE [IF NOT EXISTS] table_name
(create_definition,...) [table_options]
[partition_options]

> **NOTE:** [TEMPORARY] TABLE can be created to test table structure.
Once the session is over, the temporary table will be dropped. 

### <span style="color:green">Create  a new table:</span>

mysql> SHOW TABLE table_name (col_name col_def);

### <span style="color:green">List tables:</span>

mysql> SHOW TABLES [FROM db_name];

### <span style="color:green">List columns in a table:</span>

mysql> DESCRIBE table_name [db_name.table_name];
mysql> SHOW COLUMNS FROM table_name [FROM db_name];

### <span style="color:green">List tables and columns using the</span>
mysqlshow <span style="color:green">**command:**</span>
```bash
# mysqlshow -u [USER_NAME] -p db_name
# mysqlshow -u [USER_NAME] -p db_name table_name
```

### <span style="color:green">List additional information about a table:</span>

mysql> SHOW TABLE STATUS [FROM db_name];

### <span style="color:green">Show statement that created a table:</span>

mysql> SHOW CREATE TABLE tbl_name;

---
#### Commands Demostration.

```bash
# mysql -u root -p
Enter password:
```
```
mysql> USE prod;
Database changed
```
In the following lines, we need to specify the datatypes for the columns:
- INT -> integer.
- PRIMARY KEY -> unique key.
- AUTO_INCREMENT -> It explains itself.
- VARCHAR(50) -> length of the variable character.

```
mysql> CREATE TABLE customers (cust_id INT PRIMARY KEY AUTO_INCREMENT, username VARCHAR(50), first_name VARCHAR(50), last_name VARCHAR(50), phone_number VARCHAR(25));
Query OK, 0 rows affected (0.04 sec)

mysql> SHOW TABLES;
+----------------+
| Tables_in_prod |
+----------------+
| customers      |
+----------------+
1 row in set (0.01 sec)

mysql> DESCRIBE customers;
+--------------+-------------+------+-----+---------+----------------+
| Field        | Type        | Null | Key | Default | Extra          |
+--------------+-------------+------+-----+---------+----------------+
| cust_id      | int         | NO   | PRI | NULL    | auto_increment |
| username     | varchar(50) | YES  |     | NULL    |                |
| first_name   | varchar(50) | YES  |     | NULL    |                |
| last_name    | varchar(50) | YES  |     | NULL    |                |
| phone_number | varchar(25) | YES  |     | NULL    |                |
+--------------+-------------+------+-----+---------+----------------+
5 rows in set (0.00 sec)
```
Let's show the table's column in a different way.
> **NOTE:** I left the semicolon out on purpose because it is useful to demostrate
how the terminal behaves.

```
mysql> SHOW COLUMNS FROM customers
    -> ;
+--------------+-------------+------+-----+---------+----------------+
| Field        | Type        | Null | Key | Default | Extra          |
+--------------+-------------+------+-----+---------+----------------+
| cust_id      | int         | NO   | PRI | NULL    | auto_increment |
| username     | varchar(50) | YES  |     | NULL    |                |
| first_name   | varchar(50) | YES  |     | NULL    |                |
| last_name    | varchar(50) | YES  |     | NULL    |                |
| phone_number | varchar(25) | YES  |     | NULL    |                |
+--------------+-------------+------+-----+---------+----------------+
5 rows in set (0.00 sec)

```
Let's show database and its table using _mysqlshow_ command.

```bash
# mysqlshow -u root -p prod
Enter password: 
Database: prod
+-----------+
|  Tables   |
+-----------+
| customers |
+-----------+

# mysqlshow -u root -p prod customers
Enter password: 
Database: prod  Table: customers
+--------------+-------------+--------------------+------+-----+---------+----------------+---------------------------------+---------+
| Field        | Type        | Collation          | Null | Key | Default | Extra          | Privileges                      | Comment |
+--------------+-------------+--------------------+------+-----+---------+----------------+---------------------------------+---------+
| cust_id      | int         |                    | NO   | PRI |         | auto_increment | select,insert,update,references |         |
| username     | varchar(50) | utf8mb4_0900_ai_ci | YES  |     |         |                | select,insert,update,references |         |
| first_name   | varchar(50) | utf8mb4_0900_ai_ci | YES  |     |         |                | select,insert,update,references |         |
| last_name    | varchar(50) | utf8mb4_0900_ai_ci | YES  |     |         |                | select,insert,update,references |         |
| phone_number | varchar(25) | utf8mb4_0900_ai_ci | YES  |     |         |                | select,insert,update,references |         |
+--------------+-------------+--------------------+------+-----+---------+----------------+---------------------------------+---------+

```

