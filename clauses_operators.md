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
```
## Comparison Functions and Operators
### Using LIKE and=:
```bash
mysql> SELECT select_expr FROM tbl_name WHERE col ='value';

mysql> SELECT select_expr FROM tbl_name WHERE col LIKE 'value';
```
### Using NOT LIKE and !=;
```bash
mysql> SELECT select_expr FROM tbl_name WHERE col != 'value';
mysql> SELECT select_expr FROM tbl_name WHERE col NOT LIKE 'value';
```