# GROUP BY and ORDER BY
```bash
SELECT Syntax
SELECT
select_expr I, select_expr ...)
[FROM table_references
(WHERE where_condition)
[GROUP BY (col_name | expr I position),
[WITH ROLLUP)]
(HAVING where_condition)
(ORDER BY {col _name | expr | position)
[ASC I DESCI, ...
[WITH ROLLUP]]
```

## SELECT statement with GROUP BY:
```bash
mysql> SELECT select_expr WHERE where_condition
GROUP BY col_name (WITH ROLLUP);

####################################################

mysql> SELECT product_type FROM products GROUP BY product_type;
+--------------+
| product_type |
+--------------+
| desktop      |
| laptop       |
| server       |
+--------------+
3 rows in set (0.00 sec)

mysql> SELECT product_type, AVG(price) FROM products GROUP BY product_type;
+--------------+-------------+
| product_type | AVG(price)  |
+--------------+-------------+
| desktop      | 1500.000000 |
| laptop       |  999.990000 |
| server       | 2000.000000 |
+--------------+-------------+
3 rows in set (0.00 sec)

mysql> SELECT product_type, SUM(quantity) AS total FROM orders GROUP BY product_type;

```
## SELECT statement with GROUP BY ….. HAVING:
```bash
mysql> SELECT select_expr WHERE where_condition
GROUP BY col_name HAVING where_condition;

################################################################

mysql> SELECT product_type SUM(quantity) AS total FROM products GROUP BY product_type HAVING product_type = 'laptop';

mysql> SELECT product_type SUM(quantity) AS total FROM products GROUP BY product_type HAVING total > 50;

```
## SELECT statement with ORDER BY:
```bash
mysql> SELECT select_expr WHERE where_condition
ORDER BY col _name;

#################################################################

mysql> SELECT  * FROM customers_test
    -> ;
+---------+----------+------------+-----------+--------------+
| cust_id | username | first_name | last_name | phone_number |
+---------+----------+------------+-----------+--------------+
|       1 | pparker  | peter      | parker    | 1212121212   |
|       2 | bwayne   | bruce      | wayne     | 2222222222   |
|       3 | alanp    | alan       | pope      | 9999999999   |
|       4 | mwatney  | mark       | watney    | 2222222222   |
+---------+----------+------------+-----------+--------------+
4 rows in set (0.00 sec)

mysql> SELECT * FROM customers_test ORDER BY first_name;
+---------+----------+------------+-----------+--------------+
| cust_id | username | first_name | last_name | phone_number |
+---------+----------+------------+-----------+--------------+
|       3 | alanp    | alan       | pope      | 9999999999   |
|       2 | bwayne   | bruce      | wayne     | 2222222222   |
|       4 | mwatney  | mark       | watney    | 2222222222   |
|       1 | pparker  | peter      | parker    | 1212121212   |
+---------+----------+------------+-----------+--------------+
4 rows in set (0.00 sec)


```
## SELECT statement with GROUP BY and ORDER BY:
```bash
mysql> SELECT select_expr WHERE where_ condition
GROUP BY col name (HAVING where_condition) ORDER BY col_name;

#################################################################

mysql> SELECT product_type, price FROM products WHERE product_type = 'laptop' AND price >= 999 ORDER BY price DESC;
+--------------+--------+
| product_type | price  |
+--------------+--------+
| laptop       | 999.99 |
+--------------+--------+
1 row in set (0.00 sec)

mysql> SELECT product_type, AVG(price) AS average FROM products GROUP BY product_type HAVING average > 900 ORDER BY average;
+--------------+-------------+
| product_type | average     |
+--------------+-------------+
| laptop       |  999.990000 |
| desktop      | 1500.000000 |
| server       | 2000.000000 |
+--------------+-------------+
3 rows in set (0.00 sec)

mysql> SELECT product_type, AVG(price) AS average FROM products GROUP BY product_type HAVING average > 1000 ORDER BY average;
+--------------+-------------+
| product_type | average     |
+--------------+-------------+
| desktop      | 1500.000000 |
| server       | 2000.000000 |
+--------------+-------------+
2 rows in set (0.00 sec)

mysql> SELECT product_type, AVG(price) AS average FROM products GROUP BY product_type HAVING average > 900 ORDER BY average DESC;
+--------------+-------------+
| product_type | average     |
+--------------+-------------+
| server       | 2000.000000 |
| desktop      | 1500.000000 |
| laptop       |  999.990000 |
+--------------+-------------+
3 rows in set (0.00 sec)
```

Next [Unions.](unions.md)