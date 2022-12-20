# DROP
## Dropping Objects in MySQL
### Drop a database:
```bash
mysql> DROP DATABASE (IF EXISTS) db_name;
```
### Drop a table:
```bash
mysql> DROP (TEMPORARY) TABLE (IF EXISTS) tbl_name (, tbL_name):
```
### Drop an index:
```bash
mysql> DROP INDEX index_name ON tb1_name;
```
### Drop a stored procedure or function: 
```bash
mysql> DROP (PROCEDURE | FUNCTION) sp_name:
```
### Drop triggers and views:
```bash
mysql> DROP VIEW view_name (, view_name): mysql> DROP TRIGGER (db_name. Itrigger_name;
```
#### Dropping command line examples:
```bash
mysql> 
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| dev                |
| dev1               |
| information_schema |
| mysql              |
| performance_schema |
| prod               |
| prod_test          |
| sys                |
| test               |
+--------------------+
9 rows in set (0.00 sec)

mysql> DROP DATABASE dev1;
Query OK, 0 rows affected (0.02 sec)

mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| dev                |
| information_schema |
| mysql              |
| performance_schema |
| prod               |
| prod_test          |
| sys                |
| test               |
+--------------------+
8 rows in set (0.00 sec)

mysql> USE test;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> SHOW TABLES;
+----------------+
| Tables_in_test |
+----------------+
| customer_test  |
| customers      |
| orders         |
+----------------+
3 rows in set (0.00 sec)

mysql> DROP TABLE customer_test;
Query OK, 0 rows affected (0.02 sec)

mysql> SHOW TABLES;
+----------------+
| Tables_in_test |
+----------------+
| customers      |
| orders         |
+----------------+
2 rows in set (0.01 sec)

mysql> SHOW INDEX FROM customers\G
*************************** 1. row ***************************
        Table: customers
   Non_unique: 0
     Key_name: PRIMARY
 Seq_in_index: 1
  Column_name: cust_id
    Collation: A
  Cardinality: 0
     Sub_part: NULL
       Packed: NULL
         Null: 
   Index_type: BTREE
      Comment: 
Index_comment: 
      Visible: YES
   Expression: NULL
*************************** 2. row ***************************
        Table: customers
   Non_unique: 0
     Key_name: username
 Seq_in_index: 1
  Column_name: username
    Collation: A
  Cardinality: 0
     Sub_part: NULL
       Packed: NULL
         Null: 
   Index_type: BTREE
      Comment: 
Index_comment: 
      Visible: YES
   Expression: NULL
*************************** 3. row ***************************
        Table: customers
   Non_unique: 1
     Key_name: test
 Seq_in_index: 1
  Column_name: last_name
    Collation: A
  Cardinality: 0
     Sub_part: NULL
       Packed: NULL
         Null: YES
   Index_type: BTREE
      Comment: 
Index_comment: 
      Visible: YES
   Expression: NULL
3 rows in set (0.01 sec)

mysql> DROP INDEX test ON customers;
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> SHOW INDEX FROM customers\G
*************************** 1. row ***************************
        Table: customers
   Non_unique: 0
     Key_name: PRIMARY
 Seq_in_index: 1
  Column_name: cust_id
    Collation: A
  Cardinality: 0
     Sub_part: NULL
       Packed: NULL
         Null: 
   Index_type: BTREE
      Comment: 
Index_comment: 
      Visible: YES
   Expression: NULL
*************************** 2. row ***************************
        Table: customers
   Non_unique: 0
     Key_name: username
 Seq_in_index: 1
  Column_name: username
    Collation: A
  Cardinality: 0
     Sub_part: NULL
       Packed: NULL
         Null: 
   Index_type: BTREE
      Comment: 
Index_comment: 
      Visible: YES
   Expression: NULL
2 rows in set (0.00 sec)

mysql> CREATE VIEW cust_phone AS SELECT last_name, first_name, phone_number
    -> FROM customers ORDER BY last_name;
Query OK, 0 rows affected (0.01 sec)

mysql> SHOW TABLES;
+----------------+
| Tables_in_prod |
+----------------+
| audit          |
| cust_phone     |
| customers      |
| customers_test |
+----------------+
4 rows in set (0.01 sec)

mysql> DROP VIEW cust_phone;
Query OK, 0 rows affected (0.00 sec)

mysql> SHOW TABLES;
+----------------+
| Tables_in_prod |
+----------------+
| audit          |
| customers      |
| customers_test |
+----------------+
3 rows in set (0.01 sec)
```