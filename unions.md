# UNION
Unions are the result of combining multiple select statements.

## UNION Syntax
```bash
SELECT o o
UNION (ALL | DISTINCT] SELECT
[UNION [ALL | DISTINCT) SELECT ..]
```
### Performing a UNION:
```bash
mysql> SELECT select_expr FROM tbl_name WHERE where_condition UNION SELECT select_expr FROM tbl_name WHERE where_condition;

################# Desmonstration #####################################################
mysql> SHOW TABLES;
+---------------------+
| Tables_in_prod_test |
+---------------------+
| customers           |
| customers_test      |
| employees1          |
| employees2          |
| orders              |
| products            |
+---------------------+
6 rows in set (0.01 sec)

mysql> SELECT * FROM employees1;
+--------+------+
| name   | age  |
+--------+------+
| pedro  |   39 |
| julio  |   36 |
| jesus  |   28 |
| josev  |   48 |
| josem  |   45 |
| betico |   37 |
| mitch  |   29 |
| rob    |   32 |
| ben    |   28 |
| luis   |   42 |
| david  |   35 |
| elber  |   50 |
+--------+------+
12 rows in set (0.00 sec)

mysql> INSERT INTO employees2 (name, age) VALUES('lisa',59), ('monica',49),('sue',28),('chrity',42),('emily',35),('wendy',50);
Query OK, 6 rows affected (0.00 sec)
Records: 6  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM employees2;
+--------+------+
| name   | age  |
+--------+------+
| lisa   |   59 |
| monica |   49 |
| sue    |   28 |
| chrity |   42 |
| emily  |   35 |
| wendy  |   50 |
+--------+------+
6 rows in set (0.00 sec)

mysql> SELECT * from employees1 UNION SELECT * FROM employees2;
+--------+------+
| name   | age  |
+--------+------+
| pedro  |   39 |
| julio  |   36 |
| jesus  |   28 |
| josev  |   48 |
| josem  |   45 |
| betico |   37 |
| mitch  |   29 |
| rob    |   32 |
| ben    |   28 |
| luis   |   42 |
| david  |   35 |
| elber  |   50 |
| lisa   |   59 |
| monica |   49 |
| sue    |   28 |
| chrity |   42 |
| emily  |   35 |
| wendy  |   50 |
+--------+------+
18 rows in set (0.00 sec)

mysql> INSERT INTO employees2 (name, age) VALUES('luis',59);
Query OK, 1 row affected (0.00 sec)

mysql> SELECT * from employees1 UNION SELECT * FROM employees2;
+--------+------+
| name   | age  |
+--------+------+
| pedro  |   39 |
| julio  |   36 |
| jesus  |   28 |
| josev  |   48 |
| josem  |   45 |
| betico |   37 |
| mitch  |   29 |
| rob    |   32 |
| ben    |   28 |
| luis   |   42 | <-- Look
| david  |   35 |
| elber  |   50 |
| lisa   |   59 |
| monica |   49 |
| sue    |   28 |
| chrity |   42 |
| emily  |   35 |
| wendy  |   50 |
| luis   |   59 | <-- Look
+--------+------+
19 rows in set (0.00 sec)

mysql> SELECT name FROM employees1 UNION SELECT name FROM employees2;
+--------+
| name   |
+--------+
| pedro  |
| julio  |
| jesus  |
| josev  |
| josem  |
| betico |
| mitch  |
| rob    |
| ben    |
| luis   | <-- It only shows 1 name
| david  |
| elber  |
| lisa   |
| monica |
| sue    |
| chrity |
| emily  |
| wendy  |
+--------+
18 rows in set (0.00 sec)

mysql> SELECT name FROM employees1 UNION ALL SELECT name FROM employees2;
+--------+
| name   |
+--------+
| pedro  |
| julio  |
| jesus  |
| josev  |
| josem  |
| betico |
| mitch  |
| rob    |
| ben    |
| luis   |
| david  |
| elber  |
| lisa   |
| monica |
| sue    |
| chrity |
| emily  |
| wendy  |
| luis   |
+--------+
19 rows in set (0.00 sec)

mysql> SELECT * FROM employees1 WHERE age < 50 UNION SELECT * FROM employees2 WHERE name LIKE '
s%';
+--------+------+
| name   | age  |
+--------+------+
| pedro  |   39 |
| julio  |   36 |
| jesus  |   28 |
| josev  |   48 |
| josem  |   45 |
| betico |   37 |
| mitch  |   29 |
| rob    |   32 |
| ben    |   28 |
| luis   |   42 |
| david  |   35 |
| sue    |   28 |
+--------+------+
12 rows in set (0.00 sec)
```
### Using UNION with ORDER BY:
```bash
mysql> SELECT select_expr FROM tbl_name UNION
SELECT select_expr FROM tbl_name ORDER BY col_name:

########################################################

mysql> SELECT * FROM employees1 UNION SELECT * FROM employees2 ORDER BY age;
+--------+------+
| name   | age  |
+--------+------+
| jesus  |   28 |
| ben    |   28 |
| sue    |   28 |
| mitch  |   29 |
| rob    |   32 |
| david  |   35 |
| emily  |   35 |
| julio  |   36 |
| betico |   37 |
| pedro  |   39 |
| luis   |   42 |
| chrity |   42 |
| josem  |   45 |
| josev  |   48 |
| monica |   49 |
| elber  |   50 |
| wendy  |   50 |
| lisa   |   59 |
| luis   |   59 |
+--------+------+
19 rows in set (0.00 sec)
```
### Using additional columns for sorting results:
```bash
mysql> SELECT 1, select_expr FROM tbl_name UNION SELECT 2, select_expr FROM tbl_name ORDER BY col_name;

############# Specify from where the data is coming ############################

mysql> SELECT 1 AS origin, name, age FROM employees1 UNION SELECT 2, name, age FROM employees2
ORDER BY origin, age;
+--------+--------+------+
| origin | name   | age  |
+--------+--------+------+
|      1 | jesus  |   28 |
|      1 | ben    |   28 |
|      1 | mitch  |   29 |
|      1 | rob    |   32 |
|      1 | david  |   35 |
|      1 | julio  |   36 |
|      1 | betico |   37 |
|      1 | pedro  |   39 |
|      1 | luis   |   42 |
|      1 | josem  |   45 |
|      1 | josev  |   48 |
|      1 | elber  |   50 |
|      2 | sue    |   28 |
|      2 | emily  |   35 |
|      2 | chrity |   42 |
|      2 | monica |   49 |
|      2 | wendy  |   50 |
|      2 | lisa   |   59 |
|      2 | luis   |   59 |
+--------+--------+------+
19 rows in set (0.00 sec)

```

Coming up next [Joins](joins.md)