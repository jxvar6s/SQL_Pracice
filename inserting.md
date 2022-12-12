# INSERT INTO
## INSERT Syntax
```bash
INSERT
    [INTO] tbl_name
    [(col_name [, col_name] ...)]
    { {VALUES | VALUE} (value_list) [, (value_list)] ... }
```
## Insert data into a table.
```bash
mysql> INSERT INTO tbl_name (col1, col2, col3)
VALUES (VAL1, val2, val3);
```
## List records in a table:
```bash
mysql> SELECT * FROM tbl_name;
```
## Insert data into table using __INSERT...SELECT__
```bash
mysql> INSERT INTO tbl_name SELECT * FROM tbl_name;
```
### Example Statements.
```bash
mysql -u root -p   
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 12
Server version: 8.0.30 MySQL Community Server - GPL

Copyright (c) 2000, 2022, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> USE prod_test;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
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

mysql> INSERT INTO customers (username, first_name, last_name, phone_number) VALUES ('pparker','peter', 'parker', '1212121212');
Query OK, 1 row affected (0.01 sec)

mysql> INSERT INTO customers (username, first_name, last_name, phone_number) VALUES ('bwayne','bruce','wayne','2222222222'), ('alanp', 'alan', 'pope','9999999999'), ('mwatney', 'mark','watney','2222222222');
Query OK, 3 rows affected (0.01 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM customers;
+---------+----------+------------+-----------+--------------+
| cust_id | username | first_name | last_name | phone_number |
+---------+----------+------------+-----------+--------------+
|       1 | pparker  | peter      | parker    | 1212121212   |
|       2 | bwayne   | bruce      | wayne     | 2222222222   |
|       3 | alanp    | alan       | pope      | 9999999999   |
|       4 | mwatney  | mark       | watney    | 2222222222   |
+---------+----------+------------+-----------+--------------+
4 rows in set (0.00 sec)


# echo "Let's insert into products table.

mysql> DESCRIBE products;
+--------------+---------------+------+-----+---------+----------------+
| Field        | Type          | Null | Key | Default | Extra          |
+--------------+---------------+------+-----+---------+----------------+
| product_id   | int           | NO   | PRI | NULL    | auto_increment |
| product_type | varchar(255)  | NO   | UNI | NULL    |                |
| price        | decimal(10,2) | YES  |     | NULL    |                |
+--------------+---------------+------+-----+---------+----------------+
3 rows in set (0.01 sec)

mysql> INSERT INTO products (product_type, price) VALUES ('desktop', '1500'),('laptop','999.99'), ('server','2000');
Query OK, 3 rows affected (0.00 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM products;
+------------+--------------+---------+
| product_id | product_type | price   |
+------------+--------------+---------+
|          1 | desktop      | 1500.00 |
|          2 | laptop       |  999.99 |
|          3 | server       | 2000.00 |
+------------+--------------+---------+
3 rows in set (0.01 sec)


# echo "Now, we will insert into a table selecting from another table.

mysql> SELECT * FROM customers_test;
Empty set (0.00 sec)

mysql> INSERT INTO customers_test SELECT * FROM prod_test.customers;
Query OK, 4 rows affected (0.00 sec)
Records: 4  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM customers_test;
+---------+----------+------------+-----------+--------------+
| cust_id | username | first_name | last_name | phone_number |
+---------+----------+------------+-----------+--------------+
|       1 | pparker  | peter      | parker    | 1212121212   |
|       2 | bwayne   | bruce      | wayne     | 2222222222   |
|       3 | alanp    | alan       | pope      | 9999999999   |
|       4 | mwatney  | mark       | watney    | 2222222222   |
+---------+----------+------------+-----------+--------------+
4 rows in set (0.00 sec)

mysql> 
```

we'll continue with [Updating](updating.md)