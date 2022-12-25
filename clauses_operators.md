# Clauses and Operators
## SELECT Syntax
```bash
SELECT
select_expr [, select_expr ...]
[FROM table_references
[WHERE where condition)
[GROUP BY {col_name | expr | position),
[WITH ROLLUP]]
[HAVING where_condition]
[ORDER BY {col_name | expr | position}
[ASC | DESC), ... (WITH ROLLUP1) 
```
### SELECT statement with WHERE clause:
```bash
mysql> SELECT select_expr FROM tbl_name WHERE where_condition

###############################################################

mysql> SELECT * FROM audit WHERE username = 'pparker';
+----------+--------------+---------------------+
| username | phone_number | change_date         |
+----------+--------------+---------------------+
| pparker  | 3333333333   | 2022-10-13 20:56:31 |
+----------+--------------+---------------------+
1 row in set (0.00 sec)

```
## Comparison Functions and Operators
### Using LIKE and=:
```bash
mysql> SELECT select_expr FROM tbl_name WHERE col ='value';

mysql> SELECT select_expr FROM tbl_name WHERE col LIKE 'value';

###################################################################

mysql> SELECT * FROM customers_test WHERE phone_number = '2222222222';
+---------+----------+------------+-----------+--------------+
| cust_id | username | first_name | last_name | phone_number |
+---------+----------+------------+-----------+--------------+
|       2 | bwayne   | bruce      | wayne     | 2222222222   |
|       4 | mwatney  | mark       | watney    | 2222222222   |
+---------+----------+------------+-----------+--------------+
2 rows in set (0.00 sec)

mysql> SELECT * FROM audit WHERE username LIKE 'pparker';
+----------+--------------+---------------------+
| username | phone_number | change_date         |
+----------+--------------+---------------------+
| pparker  | 3333333333   | 2022-10-13 20:56:31 |
+----------+--------------+---------------------+
1 row in set (0.00 sec)

################## Wildcard ####################################
mysql> SELECT * FROM customers_test WHERE phone_number LIKE '222%';
+---------+----------+------------+-----------+--------------+
| cust_id | username | first_name | last_name | phone_number |
+---------+----------+------------+-----------+--------------+
|       2 | bwayne   | bruce      | wayne     | 2222222222   |
|       4 | mwatney  | mark       | watney    | 2222222222   |
+---------+----------+------------+-----------+--------------+
```
### Using NOT LIKE and !=;
```bash
mysql> SELECT select_expr FROM tbl_name WHERE col != 'value';
mysql> SELECT select_expr FROM tbl_name WHERE col NOT LIKE 'value';

#############################################################################

mysql> SELECT * FROM customers_test WHERE phone_number != '2222222222';
+---------+----------+------------+-----------+--------------+
| cust_id | username | first_name | last_name | phone_number |
+---------+----------+------------+-----------+--------------+
|       1 | pparker  | peter      | parker    | 1212121212   |
|       3 | alanp    | alan       | pope      | 9999999999   |
+---------+----------+------------+-----------+--------------+
2 rows in set (0.00 sec)

mysql> SELECT * FROM customers_test WHERE phone_number NOT LiKE '2222222222';
+---------+----------+------------+-----------+--------------+
| cust_id | username | first_name | last_name | phone_number |
+---------+----------+------------+-----------+--------------+
|       1 | pparker  | peter      | parker    | 1212121212   |
|       3 | alanp    | alan       | pope      | 9999999999   |
+---------+----------+------------+-----------+--------------+
2 rows in set (0.00 sec)

```
## Comparison Functions and Operators
### Using>, <, >=, and <=:
```bash
mysql> SELECT select_expr FROM tbl_name WHERE col >
'value';

mysql> SELECT select_expr FROM tbl_name WHERE col <
'value';

mysql> SELECT select expr FROM tb1 name WHERE col
'value':

mysql> SELECT select_expr FROM tbl_name WHERE col
<= 'value';

##########################################################

mysql> SELECT * FROM products;
+------------+--------------+---------+
| product_id | product_type | price   |
+------------+--------------+---------+
|          1 | desktop      | 1500.00 |
|          2 | laptop       |  999.99 |
|          3 | server       | 2000.00 |
+------------+--------------+---------+
3 rows in set (0.00 sec)

mysql> SELECT * FROM products WHERE price > 999.99;
+------------+--------------+---------+
| product_id | product_type | price   |
+------------+--------------+---------+
|          1 | desktop      | 1500.00 |
|          3 | server       | 2000.00 |
+------------+--------------+---------+
2 rows in set (0.00 sec)

mysql> SELECT * FROM products WHERE price < 2000.00;
+------------+--------------+---------+
| product_id | product_type | price   |
+------------+--------------+---------+
|          1 | desktop      | 1500.00 |
|          2 | laptop       |  999.99 |
+------------+--------------+---------+
2 rows in set (0.00 sec)

mysql> SELECT * FROM products WHERE price <= 2000.00;
+------------+--------------+---------+
| product_id | product_type | price   |
+------------+--------------+---------+
|          1 | desktop      | 1500.00 |
|          2 | laptop       |  999.99 |
|          3 | server       | 2000.00 |
+------------+--------------+---------+
3 rows in set (0.00 sec)

mysql> SELECT * FROM products WHERE price >= 999.99;
+------------+--------------+---------+
| product_id | product_type | price   |
+------------+--------------+---------+
|          1 | desktop      | 1500.00 |
|          2 | laptop       |  999.99 |
|          3 | server       | 2000.00 |
+------------+--------------+---------+
3 rows in set (0.00 sec)

mysql> 

```
## Logical Operators
### Using the AND operator:
```bash
mysql> SELECT select_expr FROM tb1_name WHERE
condition1 AND condtion2;

#################################################################

mysql> SELECT * FROM products WHERE product_type = 'laptop' AND price = 999.99;
+------------+--------------+--------+
| product_id | product_type | price  |
+------------+--------------+--------+
|          2 | laptop       | 999.99 |
+------------+--------------+--------+
1 row in set (0.00 sec)
```
### Using the OR operator:
```bash
mysql> SELECT select_expr FROM tbl_name WHERE
condition1 OR condtion2;

################################################################

mysql> SELECT * FROM products WHERE product_type = 'desktop' OR product_type = 'server';
+------------+--------------+---------+
| product_id | product_type | price   |
+------------+--------------+---------+
|          1 | desktop      | 1500.00 |
|          3 | server       | 2000.00 |
+------------+--------------+---------+
2 rows in set (0.00 sec)

mysql> SELECT * FROM products WHERE product_type = 'desktop' OR product_type = 'raspberry_pi';
+------------+--------------+---------+
| product_id | product_type | price   |
+------------+--------------+---------+
|          1 | desktop      | 1500.00 |
+------------+--------------+---------+
1 row in set (0.00 sec)

```
### Using the NOT operator:
```bash
mysql> SELECT select expr FROM tbl name WHERE NOT condition;

#################################################################

mysql> SELECT * FROM products WHERE NOT product_type = 'laptop';
+------------+--------------+---------+
| product_id | product_type | price   |
+------------+--------------+---------+
|          1 | desktop      | 1500.00 |
|          3 | server       | 2000.00 |
+------------+--------------+---------+
2 rows in set (0.00 sec)
```
Let's continue with [ORDER BY and GROUP BY](orderby_groupby.md)