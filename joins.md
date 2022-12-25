# Joins
## Perform a CROSS JOIN:
```bash
mysql> SELECT tb1.col_name, tb2.col_name
FROM tb1 CROSS JOIN tb2;

################# Let's show what we have in the tables we are using.#############

mysql> SELECT * FROM customers;
+---------+----------+------------+-----------+--------------+
| cust_id | username | first_name | last_name | phone_number |
+---------+----------+------------+-----------+--------------+
|       5 | pparker  | peter      | parker    | 1212121212   |
|       6 | bwayne   | bruce      | wayne     | 1212121212   |
|       7 | alanp    | alan       | pope      | 1111111111   |
|       8 | mwatney  | mark       | watney    | 2222222222   |
|       9 | ppan     | peter      | pan       | 3333333333   |
+---------+----------+------------+-----------+--------------+
5 rows in set (0.00 sec)

mysql> SELECT * FROM products;
+------------+--------------+---------+
| product_id | product_type | price   |
+------------+--------------+---------+
|          1 | desktop      | 1500.00 |
|          2 | laptop       |  999.99 |
|          3 | server       | 2000.00 |
+------------+--------------+---------+
3 rows in set (0.01 sec)

mysql> SELECT * FROM orders;
+----------+---------+--------------+----------+------------+
| order_id | cust_id | product_type | quantity | order_date |
+----------+---------+--------------+----------+------------+
|        3 |       5 | server       |       30 | 2019-05-23 |
|        4 |       9 | server       |       30 | 2019-05-23 |
|        5 |       9 | laptop       |       30 | 2019-05-23 |
|        6 |       8 | desktop      |       10 | 2020-05-01 |
|        7 |       5 | laptop       |        3 | 2020-12-01 |
+----------+---------+--------------+----------+------------+
5 rows in set (0.00 sec)

mysql> SELECT orders.order_id, customers.cust_id FROM orders CROSS JOiN customers;
+----------+---------+
| order_id | cust_id |
+----------+---------+
|        5 |       7 |
|        4 |       7 |
|        6 |       7 |
|        7 |       7 |
|        3 |       7 |
|        5 |       5 |
|        4 |       5 |
|        6 |       5 |
|        7 |       5 |
|        3 |       5 |
|        5 |       6 |
|        4 |       6 |
|        6 |       6 |
|        7 |       6 |
|        3 |       6 |
|        5 |       8 |
|        4 |       8 |
|        6 |       8 |
|        7 |       8 |
|        3 |       8 |
|        5 |       9 |
|        4 |       9 |
|        6 |       9 |
|        7 |       9 |
|        3 |       9 |
+----------+---------+
25 rows in set (0.00 sec)

############ Notice we are not using CROSS, the result will be the same ################

mysql> SELECT orders.order_id, customers.cust_id FROM orders JOiN customers;
+----------+---------+
| order_id | cust_id |
+----------+---------+
|        5 |       7 |
|        4 |       7 |
|        6 |       7 |
|        7 |       7 |
|        3 |       7 |
|        5 |       5 |
|        4 |       5 |
|        6 |       5 |
|        7 |       5 |
|        3 |       5 |
|        5 |       6 |
|        4 |       6 |
|        6 |       6 |
|        7 |       6 |
|        3 |       6 |
|        5 |       8 |
|        4 |       8 |
|        6 |       8 |
|        7 |       8 |
|        3 |       8 |
|        5 |       9 |
|        4 |       9 |
|        6 |       9 |
|        7 |       9 |
|        3 |       9 |
+----------+---------+
25 rows in set (0.00 sec

```
## Perform an INNER JOIN:
```bash
mysql> SELECT col_name, col_name, ...
FROM tb1 INNER JOIN tb2 ON tb1.col_name = tb2.col_name;

#### In the following example, we'll see the foreign key relationship with 2 tables ##########

mysql> SELECT last_name,product_type,quantity FROM customers INNER JOIN orders ON customers.cust_id = orders.cust_id;
+-----------+--------------+----------+
| last_name | product_type | quantity |
+-----------+--------------+----------+
| pope      | laptop       |        2 |
| wayne     | laptop       |        3 |
| wayne     | desktop      |        1 |
| watney    | desktop      |       10 |
| pan       | server       |       30 |
| pan       | laptop       |       30 |
| parker    | server       |       30 |
| parker    | laptop       |        3 |
+-----------+--------------+----------+
8 rows in set (0.00 sec)

mysql> SELECT last_name, orders.product_type, quantity * price FROM customers INNER JOIN orders INNER JOiN products ON customers.cust_id = orders.cust_id AND orders.product_type = products.product_type;
+-----------+--------------+------------------+
| last_name | product_type | quantity * price |
+-----------+--------------+------------------+
| parker    | server       |         60000.00 |
| parker    | laptop       |          2999.97 |
| wayne     | laptop       |          2999.97 |
| wayne     | desktop      |          1500.00 |
| pope      | laptop       |          1999.98 |
| watney    | desktop      |         15000.00 |
| pan       | server       |         60000.00 |
| pan       | laptop       |         29999.70 |
+-----------+--------------+------------------+
8 rows in set (0.00 sec)

######################## Using an alias #######################################################

mysql> SELECT last_name, orders.product_type, quantity * price AS Total FROM customers INNER JOIN orders INNER JOiN products O
N customers.cust_id = orders.cust_id AND orders.product_type = products.product_type;
+-----------+--------------+----------+
| last_name | product_type | Total    |
+-----------+--------------+----------+
| parker    | server       | 60000.00 |
| parker    | laptop       |  2999.97 |
| wayne     | laptop       |  2999.97 |
| wayne     | desktop      |  1500.00 |
| pope      | laptop       |  1999.98 |
| watney    | desktop      | 15000.00 |
| pan       | server       | 60000.00 |
| pan       | laptop       | 29999.70 |
+-----------+--------------+----------+
8 rows in set (0.00 sec)

```
## Perform a LEFT JOIN:
```bash
mysql> SELECT tb1.coll, tb1.col2, tb2.col1, tb2.col2 FROM tb1 LEFT JOIN tb2
ON tb1.col1 = tb2.col2;

###########################################################################

mysql> SELECT last_name,product_type, quantity FROM customers LEFT JOiN orders USING (cust_id);
+-----------+--------------+----------+
| last_name | product_type | quantity |
+-----------+--------------+----------+
| pope      | laptop       |        2 |
| wayne     | laptop       |        3 |
| wayne     | desktop      |        1 |
| watney    | desktop      |       10 |
| pan       | server       |       30 |
| pan       | laptop       |       30 |
| parker    | server       |       30 |
| parker    | laptop       |        3 |
+-----------+--------------+----------+
8 rows in set (0.00 sec)

```
## Perform a RIGHT JOIN:
```bash
mysql> SELECT tb1.coll, , tb1.col2, tb2.coll, tb2.col2 FROM tb1 LEFT RIGHT tb2
ON tb1.col1 = tb2.col2;

######################################################################################

mysql> SELECT last_name,product_type, quantity FROM customers RIGHT JOiN orders USING (cust_id);
+-----------+--------------+----------+
| last_name | product_type | quantity |
+-----------+--------------+----------+
| parker    | server       |       30 |
| pan       | server       |       30 |
| pan       | laptop       |       30 |
| watney    | desktop      |       10 |
| parker    | laptop       |        3 |
| wayne     | laptop       |        3 |
| wayne     | desktop      |        1 |
| pope      | laptop       |        2 |
+-----------+--------------+----------+
8 rows in set (0.00 sec)

##### We can change the order of the tables in the LEFT JOIN, as follows ##########

mysql> SELECT last_name,product_type, quantity FROM orders LEFT JOIN customers USING (cust_id);
+-----------+--------------+----------+
| last_name | product_type | quantity |
+-----------+--------------+----------+
| parker    | server       |       30 |
| pan       | server       |       30 |
| pan       | laptop       |       30 |
| watney    | desktop      |       10 |
| parker    | laptop       |        3 |
| wayne     | laptop       |        3 |
| wayne     | desktop      |        1 |
| pope      | laptop       |        2 |
+-----------+--------------+----------+
8 rows in set (0.00 sec)

```

> **NOTE:** Once again, this repo is based on what I have learned about the basic [MySQL](https://www.mysql.com) / databases understading. This repository is merely educational and the expansion of the previous lectures files is up to the reader. enjoy your journey and _keep fostering your curiosity_.