# select
The following examples will show a basic fuctionality of _SELECT_ statement; furthermore, it help us to retrieve data from tables and columns.
## SELECT Syntax
```bash
SELECT
select_expr I, select_expr ...)
[FROM table references
[WHERE where _condition]
[GROUP BY (col _name | expr I position),
[WITH ROLLUP11
THAVING where.
condition1
[ORDER BY {col_name I expr I position)
[ASC I DESCI, ... [WITH ROLLUP1]
```
### Select from dual:
```bash
mysql> SELECT 1 FROM DUAL; 
mysql> SELECT 1 + 1 FROM DUAL;

# echo "Command line example..."
mysql> SELECT 1 FROM DUAL;
+---+
| 1 |
+---+
| 1 |
+---+
1 row in set (0.00 sec)

mysql> SELECT 1 + FROM DUAL;

mysql> SELECT 1 + 1 FROM DUAL;
+-------+
| 1 + 1 |
+-------+
|     2 |
+-------+
1 row in set (0.00 sec)
```
### Select all columns in a table: 
```bash
mysql> SELECT * FROM tbl_name;
```
### Select a single column in a table: 
```bash
mysql> SELECT col_name FROM tbl_name;

###################################################
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

mysql> SELECT first_name, last_name, phone_number FROM customers;
+------------+-----------+--------------+
| first_name | last_name | phone_number |
+------------+-----------+--------------+
| bat        | man       | 1111111111   |
| peter      | parker    | 3333333333   |
| tony       | stark     | 3333333333   |
| deadpool   | wilson    | 3239998765   |
| peter      | parker    | 1212121212   |
| bruce      | wayne     | 2222222222   |
| alan       | pope      | 9999999999   |
| mark       | watney    | 2222222222   |
+------------+-----------+--------------+
8 rows in set (0.00 sec)

```
### Select multiple columns in a table: 
```bash
mysql> SELECT coll, col2 FROM tbl_name;

##################################################################

mysql> SELECT username FROM customers;
+----------+
| username |
+----------+
| bwayne   |
| brucew   |
| tstark   |
| wwwilson |
| spidey   |
| bwayne   |
| alanp    |
| mwatney  |
+----------+
8 rows in set (0.00 sec)

mysql> SELECT last_name, first_name FROM customers;
+-----------+------------+
| last_name | first_name |
+-----------+------------+
| man       | bat        |
| parker    | peter      |
| stark     | tony       |
| wilson    | deadpool   |
| parker    | peter      |
| wayne     | bruce      |
| pope      | alan       |
| watney    | mark       |
+-----------+------------+
8 rows in set (0.00 sec)


```
### Using a function in a select statement 
```bash
mysql> SELECT function (col_name) FROM tbl_name;

####### Let's show the COUNT() function #######################

mysql> SELECT COUNT(phone_number) FROM customers;
+---------------------+
| COUNT(phone_number) |
+---------------------+
|                   8 |
+---------------------+
1 row in set (0.00 sec)

#### CONCAT() function demonstration ##########################

mysql> SELECT CONCAT(last_name, ', ', first_name) FROM customers;
+-------------------------------------+
| CONCAT(last_name, ', ', first_name) |
+-------------------------------------+
| man, bat                            |
| parker, peter                       |
| stark, tony                         |
| wilson, deadpool                    |
| parker, peter                       |
| wayne, bruce                        |
| pope, alan                          |
| watney, mark                        |
+-------------------------------------+
8 rows in set (0.00 sec)
```

Let's continue with [Clauses and Operators](clauses_operators.md)