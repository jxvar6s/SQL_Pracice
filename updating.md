# UPDATE

## UPDATE Syntax
```bash
UPDATE [LOW_PRIORITY] [IGNORE] table_reference
    SET assignment_list
    [WHERE where_condition]
    [ORDER BY ...]
    [LIMIT row_count]
```
### Update a single row:
```bash
mysql> UPDATE tbl_name SET col = value WHERE col = value
```
### Update multiple columns:
```bash
mysql> UPDATE tbl_name SET col = value, col = value WHERE col = value
```
### Update a role using expression:
```bash
mysql> UPDATE tbl_name SET col = expression WHERE col = value
```

### Examples in command line
```bash
mysql> SELECT * FROM customers;
+---------+----------+------------+-----------+--------------+
| cust_id | username | first_name | last_name | phone_number |
+---------+----------+------------+-----------+--------------+
|       1 | bwayne   | bruce      | wayne     | 1111111111   |
|       2 | brucew   | peter      | parker    | 3333333333   |
|       3 | tstark   | tony       | stark     | 3333333333   |
|       4 | ptrbread | peter      | pan       | 2222345678   |
|       5 | wwwilson | deadpool   | wilson    | 3239998765   |
|       6 | pparker  | peter      | parker    | 1212121212   |
|       7 | bwayne   | bruce      | wayne     | 2222222222   |
|       8 | alanp    | alan       | pope      | 9999999999   |
|       9 | mwatney  | mark       | watney    | 2222222222   |
+---------+----------+------------+-----------+--------------+
9 rows in set (0.01 sec)

mysql> UPDATE customers SET username = 'spidey' WHERE cust_id = 1;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM customers;
+---------+----------+------------+-----------+--------------+
| cust_id | username | first_name | last_name | phone_number |
+---------+----------+------------+-----------+--------------+
|       1 | spidey   | bruce      | wayne     | 1111111111   |
|       2 | brucew   | peter      | parker    | 3333333333   |
|       3 | tstark   | tony       | stark     | 3333333333   |
|       4 | ptrbread | peter      | pan       | 2222345678   |
|       5 | wwwilson | deadpool   | wilson    | 3239998765   |
|       6 | pparker  | peter      | parker    | 1212121212   |
|       7 | bwayne   | bruce      | wayne     | 2222222222   |
|       8 | alanp    | alan       | pope      | 9999999999   |
|       9 | mwatney  | mark       | watney    | 2222222222   |
+---------+----------+------------+-----------+--------------+
9 rows in set (0.01 sec)

mysql> UPDATE customers SET username = 'bwayne' WHERE cust_id = 1;
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> UPDATE customers SET username = 'spidey' WHERE cust_id = 6;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM customers;
+---------+----------+------------+-----------+--------------+
| cust_id | username | first_name | last_name | phone_number |
+---------+----------+------------+-----------+--------------+
|       1 | bwayne   | bruce      | wayne     | 1111111111   |
|       2 | brucew   | peter      | parker    | 3333333333   |
|       3 | tstark   | tony       | stark     | 3333333333   |
|       4 | ptrbread | peter      | pan       | 2222345678   |
|       5 | wwwilson | deadpool   | wilson    | 3239998765   |
|       6 | spidey   | peter      | parker    | 1212121212   |
|       7 | bwayne   | bruce      | wayne     | 2222222222   |
|       8 | alanp    | alan       | pope      | 9999999999   |
|       9 | mwatney  | mark       | watney    | 2222222222   |
+---------+----------+------------+-----------+--------------+
9 rows in set (0.00 sec)

mysql> UPDATE customers SET first_name = 'bat', last_name = 'man' WHERE cust_id = 1;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM customers;
+---------+----------+------------+-----------+--------------+
| cust_id | username | first_name | last_name | phone_number |
+---------+----------+------------+-----------+--------------+
|       1 | bwayne   | bat        | man       | 1111111111   |
|       2 | brucew   | peter      | parker    | 3333333333   |
|       3 | tstark   | tony       | stark     | 3333333333   |
|       4 | ptrbread | peter      | pan       | 2222345678   |
|       5 | wwwilson | deadpool   | wilson    | 3239998765   |
|       6 | spidey   | peter      | parker    | 1212121212   |
|       7 | bwayne   | bruce      | wayne     | 2222222222   |
|       8 | alanp    | alan       | pope      | 9999999999   |
|       9 | mwatney  | mark       | watney    | 2222222222   |
+---------+----------+------------+-----------+--------------+
9 rows in set (0.00 sec)

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


mysql> SELECT * FROM orders;
+----------+---------+--------------+----------+------------+
| order_id | cust_id | product_type | quantity | order_date |
+----------+---------+--------------+----------+------------+
|        1 |       1 | laptop       |        2 | 2019-05-31 |
+----------+---------+--------------+----------+------------+
1 row in set (0.00 sec)


# Updating using an expression.

mysql> UPDATE orders SET quantity = quantity + 1 WHERE order_id = 1;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM orders;
+----------+---------+--------------+----------+------------+
| order_id | cust_id | product_type | quantity | order_date |
+----------+---------+--------------+----------+------------+
|        1 |       1 | laptop       |        3 | 2019-05-31 |
+----------+---------+--------------+----------+------------+
1 row in set (0.01 sec)

mysql> 
```

[Altering tables](altering_tables_part_1.md) is next.