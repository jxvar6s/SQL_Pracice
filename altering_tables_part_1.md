# Alter Tables
## ALTER TABLE Syntax
```bash
ALTER TABLE tbl_name
    [alter_option [, alter_option] ...]
```
## Altering Columns
### Adding column:
```bash
mysql> ALTER TABLE tbl_name ADD COLUMN col_name
datatype attribute AFTER col_name;
```
### Droppping column:
```bash
mysql> ALTER TABLE tbl_name DROP COLUMN col_name;
```
### Rename a column or table:
```bash
mysql> ALTER TABLE t1 RENAME t2;

mysql> ALTER TABLE tbl_name RENAME COLUMN
old_col_name TO new_col_name;

mysql> ALTER TABLE tbl_name CHANGE [COLUMN]
old_col_name new_col_name col_definition;

mysql> ALTER TABLE tbl_name MODIFY [COLUMN]
col_name col_definition;
```
### Modify column definition:
```bash
mysql> ALTER TABLE tbl_name MODIFY [COLUMN] col_name col_definition;
```
### Examples - command line.
```bash
mysql> USE test;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> SHOW TABLES;
+----------------+
| Tables_in_test |
+----------------+
| customers      |
+----------------+
1 row in set (0.00 sec)

mysql> DESCRIBE customers;
+--------------+-------------+------+-----+---------+-------+
| Field        | Type        | Null | Key | Default | Extra |
+--------------+-------------+------+-----+---------+-------+
| cust_id      | int         | NO   |     | 0       |       |
| username     | varchar(50) | NO   |     | NULL    |       |
| first_name   | varchar(50) | YES  |     | NULL    |       |
| last_name    | varchar(50) | YES  |     | NULL    |       |
| phone_number | varchar(25) | YES  |     | NULL    |       |
+--------------+-------------+------+-----+---------+-------+
5 rows in set (0.01 sec)


# Altering a table by adding a column

mysql> ALTER TABLE customers ADD COLUMN address VARCHAR(255) AFTER phone_number;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESCRIBE customers;
+--------------+--------------+------+-----+---------+-------+
| Field        | Type         | Null | Key | Default | Extra |
+--------------+--------------+------+-----+---------+-------+
| cust_id      | int          | NO   |     | 0       |       |
| username     | varchar(50)  | NO   |     | NULL    |       |
| first_name   | varchar(50)  | YES  |     | NULL    |       |
| last_name    | varchar(50)  | YES  |     | NULL    |       |
| phone_number | varchar(25)  | YES  |     | NULL    |       |
| address      | varchar(255) | YES  |     | NULL    |       |
+--------------+--------------+------+-----+---------+-------+
6 rows in set (0.00 sec)


# Dropping / deleting a coolumn

mysql> ALTER TABLE customers DROP COLUMN address;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESCRIBE customers;
+--------------+-------------+------+-----+---------+-------+
| Field        | Type        | Null | Key | Default | Extra |
+--------------+-------------+------+-----+---------+-------+
| cust_id      | int         | NO   |     | 0       |       |
| username     | varchar(50) | NO   |     | NULL    |       |
| first_name   | varchar(50) | YES  |     | NULL    |       |
| last_name    | varchar(50) | YES  |     | NULL    |       |
| phone_number | varchar(25) | YES  |     | NULL    |       |
+--------------+-------------+------+-----+---------+-------+
5 rows in set (0.00 sec)


# echo "Renaming a column in 2 different ways."

# echo "1 -"

mysql> ALTER TABLE customers RENAME COLUMN phone_number TO phoneNumber;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESCRIBE customers;
+-------------+-------------+------+-----+---------+-------+
| Field       | Type        | Null | Key | Default | Extra |
+-------------+-------------+------+-----+---------+-------+
| cust_id     | int         | NO   |     | 0       |       |
| username    | varchar(50) | NO   |     | NULL    |       |
| first_name  | varchar(50) | YES  |     | NULL    |       |
| last_name   | varchar(50) | YES  |     | NULL    |       |
| phoneNumber | varchar(25) | YES  |     | NULL    |       |
+-------------+-------------+------+-----+---------+-------+
5 rows in set (0.00 sec)

# echo "2 -"
mysql> ALTER TABLE customers CHANGE COLUMN phoneNumber phone_number VARCHAR(25);
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESCRIBE customers;
+--------------+-------------+------+-----+---------+-------+
| Field        | Type        | Null | Key | Default | Extra |
+--------------+-------------+------+-----+---------+-------+
| cust_id      | int         | NO   |     | 0       |       |
| username     | varchar(50) | NO   |     | NULL    |       |
| first_name   | varchar(50) | YES  |     | NULL    |       |
| last_name    | varchar(50) | YES  |     | NULL    |       |
| phone_number | varchar(25) | YES  |     | NULL    |       |
+--------------+-------------+------+-----+---------+-------+
5 rows in set (0.01 sec)


# echo "Renaming a table..."

mysql> ALTER TABLE customers RENAME TO test;
Query OK, 0 rows affected (0.01 sec)

mysql> SHOW TABLES;
+----------------+
| Tables_in_test |
+----------------+
| test           |
+----------------+
1 row in set (0.01 sec)


# Renaming back to the original name by using the RENAME statement instead
# of ALTER TABLE

mysql> RENAME TABLE test TO customers;
Query OK, 0 rows affected (0.01 sec)

mysql> SHOW TABLES;
+----------------+
| Tables_in_test |
+----------------+
| customers      |
+----------------+
1 row in set (0.01 sec)

mysql> DESCRIBE customers;
+--------------+-------------+------+-----+---------+-------+
| Field        | Type        | Null | Key | Default | Extra |
+--------------+-------------+------+-----+---------+-------+
| cust_id      | int         | NO   |     | 0       |       |
| username     | varchar(50) | NO   |     | NULL    |       |
| first_name   | varchar(50) | YES  |     | NULL    |       |
| last_name    | varchar(50) | YES  |     | NULL    |       |
| phone_number | varchar(25) | YES  |     | NULL    |       |
+--------------+-------------+------+-----+---------+-------+
5 rows in set (0.01 sec)


# echo "Modify a column..."

mysql> ALTER TABLE customers MODIFY username CHAR(100) NOT NULL;
Query OK, 0 rows affected (0.03 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESCRIBE customers;
+--------------+-------------+------+-----+---------+-------+
| Field        | Type        | Null | Key | Default | Extra |
+--------------+-------------+------+-----+---------+-------+
| cust_id      | int         | NO   |     | 0       |       |
| username     | char(100)   | NO   |     | NULL    |       |
| first_name   | varchar(50) | YES  |     | NULL    |       |
| last_name    | varchar(50) | YES  |     | NULL    |       |
| phone_number | varchar(25) | YES  |     | NULL    |       |
+--------------+-------------+------+-----+---------+-------+
5 rows in set (0.01 sec)
```
### Reordering columns:
``` bash
mysql> ALTER TABLE tbl name CHANGE [COLUMN] col_name col_name col_definition [FIRST Al AFTER col name];
mysql> ALTER TABLE tbl_name MODIFY [COLUMN] col_name col_definition [FIRST | AFTER col_name]; mysql> ALTER TABLE tbl_name ORDER BY col_name [, col name]
```
#### Example - code -
```bash
mysql> ALTER TABLE customers CHANGE username username CHAR(100) NOT NULL AFTER last_name;
Query OK, 0 rows affected (0.03 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESCRIBE customers;
+--------------+-------------+------+-----+---------+-------+
| Field        | Type        | Null | Key | Default | Extra |
+--------------+-------------+------+-----+---------+-------+
| cust_id      | int         | NO   |     | 0       |       |
| first_name   | varchar(50) | YES  |     | NULL    |       |
| last_name    | varchar(50) | YES  |     | NULL    |       |
| username     | char(100)   | NO   |     | NULL    |       |
| phone_number | varchar(25) | YES  |     | NULL    |       |
+--------------+-------------+------+-----+---------+-------+
5 rows in set (0.00 sec)

mysql> ALTER TABLE customers MODIFY username CHAR(100) NOT NULL AFTER cust_id;
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESCRIBE CUSTOMERS;
+--------------+-------------+------+-----+---------+-------+
| Field        | Type        | Null | Key | Default | Extra |
+--------------+-------------+------+-----+---------+-------+
| cust_id      | int         | NO   |     | 0       |       |
| username     | char(100)   | NO   |     | NULL    |       |
| first_name   | varchar(50) | YES  |     | NULL    |       |
| last_name    | varchar(50) | YES  |     | NULL    |       |
| phone_number | varchar(25) | YES  |     | NULL    |       |
+--------------+-------------+------+-----+---------+-------+
5 rows in set (0.00 sec)
```

Continue with [Altering Tables part 2](altering_tables_part_2.md)