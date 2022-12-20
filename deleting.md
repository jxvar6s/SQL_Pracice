# DELETE
## DELETE Syntax
```bash
DELETE FROM tbl_name [WHERE where_cond] [ORDER BY ...] [LIMIT row_count]
```
### Multiple-Table Syntax
```bash
DELETE tbl_name [.*] [, tbl_name l.*JJ ...
FROM table references
[WHERE where_ condition]
DELETE FROM tbl_name [.*] [, tbl_name [.*])
USING table_references
[WHERE where_condition]
```
### Delete rows from a table:
```bash
mysql> DELETE FROM tbl_name WHERE where_cond
```
### Delete rows from multiple tables:
```bash
mysql> DELETE tb1, tb2 FROM tb1 INNER JOIN tb2 ON
tb2.id = tb1. id WHERE tb1.id = value;
```
### Truncate a table:
```bash
mysql> TRUNCATE [TABLE] tb1_name;
```
#### Command line examples.
```bash
mysql> USE prod;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> SHOW TABLES;
+----------------+
| Tables_in_prod |
+----------------+
| audit          |
| customers      |
| customers_test |
+----------------+
3 rows in set (0.00 sec)

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
9 rows in set (0.01 sec)

mysql> SELECT * FROM customers_test
    -> ;
Empty set (0.00 sec)

mysql> SELECT * FROM audit;
+----------+--------------+---------------------+
| username | phone_number | change_date         |
+----------+--------------+---------------------+
| pparker  | 3333333333   | 2022-10-13 20:56:31 |
| bwayne   | 2222222222   | 2022-10-13 20:58:15 |
+----------+--------------+---------------------+
2 rows in set (0.01 sec)

mysql> DELETE FROM audit WHERE username = bwayne;
ERROR 1054 (42S22): Unknown column 'bwayne' in 'where clause'
mysql> DELETE FROM audit WHERE username = 'bwayne';
Query OK, 1 row affected (0.01 sec)

mysql> SELECT * FROM audit;
+----------+--------------+---------------------+
| username | phone_number | change_date         |
+----------+--------------+---------------------+
| pparker  | 3333333333   | 2022-10-13 20:56:31 |
+----------+--------------+---------------------+
1 row in set (0.00 sec)

mysql> DELETE FROM customers WHERE cust_id = 4;
Query OK, 1 row affected (0.00 sec)

mysql> SELECT * FROM customers;
+---------+----------+------------+-----------+--------------+
| cust_id | username | first_name | last_name | phone_number |
+---------+----------+------------+-----------+--------------+
|       1 | bwayne   | bat        | man       | 1111111111   |
|       2 | brucew   | peter      | parker    | 3333333333   |
|       3 | tstark   | tony       | stark     | 3333333333   |
|       5 | wwwilson | deadpool   | wilson    | 3239998765   |
|       6 | spidey   | peter      | parker    | 1212121212   |
|       7 | bwayne   | bruce      | wayne     | 2222222222   |
|       8 | alanp    | alan       | pope      | 9999999999   |
|       9 | mwatney  | mark       | watney    | 2222222222   |
+---------+----------+------------+-----------+--------------+
8 rows in set (0.00 sec)

mysql> DELETE customers, orders FROM customers INNER JOIN orders ON orders.cust_id = customers.cust_id WHERE customers.cust_id = 2;
Query OK, 0 rows affected (0.01 sec)
```
#### Truncate and Delete.
```bash
mysql> TRUNCATE TABLE orders;
Query OK, 0 rows affected (0.02 sec)

mysql> SELECT * FROM orders;
Empty set (0.01 sec)

mysql> DELETE FROM customers;
Query OK, 4 rows affected (0.01 sec)

mysql> SELECT * FROM customers;
Empty set (0.00 sec)
```

Next [Dropping](dropping.md)