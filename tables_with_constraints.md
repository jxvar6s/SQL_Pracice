# Creating Tables with Constraints.
## Create Table Syntax
```bash
CREATE [TEMPORARY] TABLE [IF NOT EXISTS] tbl_name (create_definition,...) [table_options]
[partition_options]
```
### Creating Tables
#### Column information for customers tables:
- cust_id INT PRIMARY KEY AUTO_INCREMENT
- username VARCHAR(50) NOT NULL UNIQUE
- first_name VARCHAR(50)
- last_name VARCHAR(50)
- phone_number VARCHAR(25)
#### Culumn information for products table:
- product_id INT PRIMARY KEY AUTO_INCREMENT
- product_type VARCHAR(255) NOT NULL UNIQUE
- price DECIMAL(10.2)

Let's create the database and the tables.
```bash
mysql> CREATE DATABASE prod_test;
Query OK, 1 row affected (0.01 sec)

mysql> USE prod_test;
Database changed
mysql> CREATE TABLE customers (cust_id INT PRIMARY KEY AUTO_INCREMENT, username VARCHAR(50) NOT NULL UNIQUE, first_name VARCHAR(50), last_name VARCHAR(50), phone_number VARCHAR(25));
Query OK, 0 rows affected (0.01 sec)

mysql> SHOW TABLES;
+---------------------+
| Tables_in_prod_test |
+---------------------+
| customers           |
+---------------------+
1 row in set (0.00 sec)

mysql> DESCRIBE customers;
+--------------+-------------+------+-----+---------+----------------+
| Field        | Type        | Null | Key | Default | Extra          |
+--------------+-------------+------+-----+---------+----------------+
| cust_id      | int         | NO   | PRI | NULL    | auto_increment |
| username     | varchar(50) | NO   | UNI | NULL    |                |
| first_name   | varchar(50) | YES  |     | NULL    |                |
| last_name    | varchar(50) | YES  |     | NULL    |                |
| phone_number | varchar(25) | YES  |     | NULL    |                |
+--------------+-------------+------+-----+---------+----------------+
5 rows in set (0.01 sec)

mysql> CREATE TABLE products (product_id INT PRIMARY KEY AUTO_INCREMENT, product_type VARCHAR(255) NOT NULL UNIQUE, price DECIMAL(10,2));
Query OK, 0 rows affected (0.02 sec)

mysql> DESCRIBE products;
+--------------+---------------+------+-----+---------+----------------+
| Field        | Type          | Null | Key | Default | Extra          |
+--------------+---------------+------+-----+---------+----------------+
| product_id   | int           | NO   | PRI | NULL    | auto_increment |
| product_type | varchar(255)  | NO   | UNI | NULL    |                |
| price        | decimal(10,2) | YES  |     | NULL    |                |
+--------------+---------------+------+-----+---------+----------------+
3 rows in set (0.00 sec)

mysql> 
```
Now, We need one more table call orders.
```bash
mysql> CREATE TABLE orders (order_id INT PRIMARY KEY AUTO_INCREMENT, cust_id INT, product_type
VARCHAR(255) NOT NULL, quantity INT DEFAULT 1, order_date DATE, FOREIGN KEY (cust_id) REFERENCES customers(cust_id),FOREIGN KEY (product_type) REFERENCES products(product_type));
Query OK, 0 rows affected (0.02 sec)

mysql> DESCRIBE orders;
+--------------+--------------+------+-----+---------+----------------+
| Field        | Type         | Null | Key | Default | Extra          |
+--------------+--------------+------+-----+---------+----------------+
| order_id     | int          | NO   | PRI | NULL    | auto_increment |
| cust_id      | int          | YES  | MUL | NULL    |                |
| product_type | varchar(255) | NO   | MUL | NULL    |                |
| quantity     | int          | YES  |     | 1       |                |
| order_date   | date         | YES  |     | NULL    |                |
+--------------+--------------+------+-----+---------+----------------+
5 rows in set (0.01 sec)

mysql> SHOW TABLES;
+---------------------+
| Tables_in_prod_test |
+---------------------+
| customers           |
| orders              |
| products            |
+---------------------+
3 rows in set (0.00 sec)
```
### Create New Table Based on an Existing Table.
```bash
mysql> CREATE TABLE test.customers AS SELECT * FROM customers;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> SHOW TABLES;
+---------------------+
| Tables_in_prod_test |
+---------------------+
| customers           |
| orders              |
| products            |
+---------------------+
3 rows in set (0.01 sec)

mysql> SHOW TABLES FROM test;
+----------------+
| Tables_in_test |
+----------------+
| customers      |
+----------------+
1 row in set (0.01 sec)

mysql> DESCRIBE test.customers;
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

mysql> CREATE TABLE customers_test LIKE customers;
Query OK, 0 rows affected (0.01 sec)

mysql> SHOW TABLES;
+---------------------+
| Tables_in_prod_test |
+---------------------+
| customers           |
| customers_test      |
| orders              |
| products            |
+---------------------+
4 rows in set (0.01 sec)

mysql> DESCRIBE customers_test;
+--------------+-------------+------+-----+---------+----------------+
| Field        | Type        | Null | Key | Default | Extra          |
+--------------+-------------+------+-----+---------+----------------+
| cust_id      | int         | NO   | PRI | NULL    | auto_increment |
| username     | varchar(50) | NO   | UNI | NULL    |                |
| first_name   | varchar(50) | YES  |     | NULL    |                |
| last_name    | varchar(50) | YES  |     | NULL    |                |
| phone_number | varchar(25) | YES  |     | NULL    |                |
+--------------+-------------+------+-----+---------+----------------+
5 rows in set (0.01 sec)

mysql> 
```

Next - [Insert Into](inserting.md)