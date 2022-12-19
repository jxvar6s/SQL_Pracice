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