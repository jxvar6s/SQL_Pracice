# Create Index
- It enables you to add indexes to existing tables.
- CREATE INDEX is mapped to an ALTER TABLE statement to create indexes.
- It cannot be used to to create PRIMARY KEY. Use ALTER TABLE instead.
## CREATE INDEX Syntax
```bash
CREATE (UNIQUE) INDEX index_name ON tb1_name (key.
part....)
```
### Creating Indexes
#### Create an index using a single column: 
```bash
mysql> CREATE INDEX index_name ON tbl_name (col1);
```
#### Show indexes on a table:
```bash
mysql> SHOW INDEXES FROM (db_name. Itbl_name:
```
#### Create an index using multiple columns: 
```bash 
mysql> CREATE INDEX Index_name ON tbI_name (coll, col2);
```
#### Create a unique index:
```bash
mysql> CREATE UNIQUE INDEX index_name ON tbil_name (coll);
```
#### Create an index using a column prefix: 
```bash
mysql> CREATE INDEX index_name ON tbl_name (col1(10));
```
# Command line examples:
```bash
mysql> EXPLAIN SELECT * FROM customers WHERE phone_number = '1212121212'\G
*************************** 1. row ***************************
           id: 1
  select_type: SIMPLE
        table: customers
   partitions: NULL
         type: ALL
possible_keys: NULL
          key: NULL
      key_len: NULL
          ref: NULL
         rows: 1
     filtered: 100.00
        Extra: Using where
1 row in set, 1 warning (0.01 sec)


mysql> CREATE INDEX phone_number ON customers (phone_number);
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> CREATE INDEX first_last ON customers (first_name, last_name);
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

Next [Selecting](selecting.md)