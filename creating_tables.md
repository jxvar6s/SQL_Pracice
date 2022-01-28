# Creating Tables

## CREATE TABLE <span style="color:green">**Syntax**</span>

![](Images/database.png)

CREATE [TEMPORARY] TABLE [IF NOT EXISTS] table_name
(create_definition,...) [table_options]
[partition_options]

> <span style="color:red">**NOTE:**</span> [TEMPORARY] TABLE can be created to test table structure.
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
#### Commands Demonstration.

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
- PRIMARY KEY -> unique key, it is used to index the table.
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

Let's go back to [MySQL](http://www.mysql.com) server.

```bash
# mysql -u root -p
Enter password

mysql>
```
> **NOTE:** '\G' display the information verticaly rather than horizontally
```
 mysql> SHOW TABLE STATUS\G
*************************** 1. row ***************************
           Name: customers
         Engine: InnoDB
        Version: 10
     Row_format: Dynamic
           Rows: 0
 Avg_row_length: 0
    Data_length: 16384
Max_data_length: 0
   Index_length: 0
      Data_free: 0
 Auto_increment: 1
    Create_time: 2022-01-26 23:07:21
    Update_time: NULL
     Check_time: NULL
      Collation: utf8mb4_0900_ai_ci
       Checksum: NULL
 Create_options: 
        Comment: 
1 row in set (0.01 sec)
```

We can display information about how the table was created.

```
mysql> SHOW CREATE TABLE customers;
+-----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Table     | Create Table                                                                                                                                                                                                                                                                                                                        |
+-----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| customers | CREATE TABLE `customers` (
  `cust_id` int NOT NULL AUTO_INCREMENT,
  `username` varchar(50) DEFAULT NULL,
  `first_name` varchar(50) DEFAULT NULL,
  `last_name` varchar(50) DEFAULT NULL,
  `phone_number` varchar(25) DEFAULT NULL,
  PRIMARY KEY (`cust_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci |
+-----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
1 row in set (0.00 sec)
```


### <span style="color:green">Copying and Cloning Tables</span>
![](Images/content.png)
- CREATE TABLE...LIKE:

CREATE TABLE new_table LIKE origin_table;

```
mysql> CREATE TABLE customers_test LIKE customers;
Query OK, 0 rows affected (0.03 sec)

mysql> SHOW TABLES
    -> ;
+----------------+
| Tables_in_prod |
+----------------+
| customers      |
| customers_test |
+----------------+
2 rows in set (0.00 sec)

mysql> DESCRIBE customers_test;
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
In the previous lines, we can see that both tables are identical.


- CREATE TABLE...SELECT:

```
mysql> CREATE TABLE customers_bkup SELECT * FROM customers;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> SHOW TABLES
    -> ;
+----------------+
| Tables_in_prod |
+----------------+
| customers      |
| customers_bkup |
| customers_test |
+----------------+
3 rows in set (0.00 sec)

mysql> 

```

### DROP TABLE <span style="color:green">Syntax</span> 

DROP (TEMPORARY] TABLE (IF EXISTS] tbl_name l,
tbl_name] ... [RESTRICT | CASCADE]

<span style="color:green">Drop an existing table:</span>

```
mysql> SHOW TABLES
    -> ;
+----------------+
| Tables_in_prod |
+----------------+
| customers      |
| customers_bkup |
| customers_test |
+----------------+
3 rows in set (0.00 sec)
```

DROP TABLE tbl_name;
```
mysql> DROP TABLE customers_test;
Query OK, 0 rows affected (0.02 sec)
```
DROP TABLE db_name.tbl_name;

```
mysql> DROP TABLE prod.customers_bkup;
Query OK, 0 rows affected (0.01 sec)

mysql> SHOW TABLES;
+----------------+
| Tables_in_prod |
+----------------+
| customers      |
+----------------+
1 row in set (0.01 sec)
```
