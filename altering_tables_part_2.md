
# Ater Table.
## Altering Keys and Indexes on Columns
### Add Keys and Indexes:
```bash 
mysql> ALTER TABLE tbl_name ADD PRIMARY KEY (col_name);
mysql> ALTER TABLE tbl_name ADD [symbol] FOREIGN KEY (col name) ref definition;
mysql> ALTER TABLE tbl_name ADD UNIQUE (col_name) ; mysql> ALTER TABLE tbl_name ADD INDEX index_name (col_name) ;
```
### Add Keys and Indexes using CHANGE and MODIFY: mysql> ALTER TABLE tbl_name CHANGE col_name col_name col_definition;
```bash
mysql> ALTER TABLE tb1_name MODIFY col_name col_definition;
```
### Rename indexes:
```bash
mysql> ALTER TABLE tbl_name RENAME INDEX old_ _index_name TO new_index_name
```
#### Command line examples.
The folowing step, It is to _ALTER_ the tables customers and orders _ADD_ing a _PRIMARY KEY_
```bash
mysql> ALTER TABLE customers ADD PRIMARY KEY (cust_id);
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> ALTER TABLE orders ADD PRIMARY KEY (order_id);
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESCRIBE customers;
+--------------+-------------+------+-----+---------+-------+
| Field        | Type        | Null | Key | Default | Extra |
+--------------+-------------+------+-----+---------+-------+
| cust_id      | int         | NO   | PRI | 0       |       |
| username     | char(100)   | NO   |     | NULL    |       |
| first_name   | varchar(50) | YES  |     | NULL    |       |
| last_name    | varchar(50) | YES  |     | NULL    |       |
| phone_number | varchar(25) | YES  |     | NULL    |       |
+--------------+-------------+------+-----+---------+-------+
5 rows in set (0.00 sec)


mysql> DESCRIBE orders;
+--------------+--------------+------+-----+---------+-------+
| Field        | Type         | Null | Key | Default | Extra |
+--------------+--------------+------+-----+---------+-------+
| order_id     | int          | YES  |     | NULL    |       |
| cust_id      | int          | YES  |     | NULL    |       |
| product_type | varchar(255) | YES  |     | NULL    |       |
| quantity     | int          | YES  |     | NULL    |       |
| order_date   | date         | YES  |     | NULL    |       |
+--------------+--------------+------+-----+---------+-------+

# echo "Adding a foreign key to orders table and unique and index, and to customers table..."

mysql> ALTER TABLE orders ADD FOREIGN KEY fk_cust_id (cust_id) REFERENCES customers(cust_id);
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> ALTER TABLE customers ADD UNIQUE (username);
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> ALTER TABLE customers ADD INDEX last_name (last_name);
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

# echo "The next step, it is showing the indexes...

mysql> SHOW INDEX FROM customers\G
*************************** 1. row ***************************
        Table: customers
   Non_unique: 0
     Key_name: PRIMARY
 Seq_in_index: 1
  Column_name: cust_id
    Collation: A
  Cardinality: 0
     Sub_part: NULL
       Packed: NULL
         Null: 
   Index_type: BTREE
      Comment: 
Index_comment: 
      Visible: YES
   Expression: NULL
*************************** 2. row ***************************
        Table: customers
   Non_unique: 0
     Key_name: username
 Seq_in_index: 1
  Column_name: username
    Collation: A
  Cardinality: 0
     Sub_part: NULL
       Packed: NULL
         Null: 
   Index_type: BTREE
      Comment: 
Index_comment: 
      Visible: YES
   Expression: NULL
*************************** 3. row ***************************
        Table: customers
   Non_unique: 1
     Key_name: last_name
 Seq_in_index: 1
  Column_name: last_name
    Collation: A
  Cardinality: 0
     Sub_part: NULL
       Packed: NULL
         Null: YES
   Index_type: BTREE
      Comment: 
Index_comment: 
      Visible: YES
   Expression: NULL
3 rows in set (0.00 sec)

mysql> SHOW INDEX FROM orders\G
*************************** 1. row ***************************
        Table: orders
   Non_unique: 0
     Key_name: PRIMARY
 Seq_in_index: 1
  Column_name: order_id
    Collation: A
  Cardinality: 0
     Sub_part: NULL
       Packed: NULL
         Null: 
   Index_type: BTREE
      Comment: 
Index_comment: 
      Visible: YES
   Expression: NULL
*************************** 2. row ***************************
        Table: orders
   Non_unique: 1
     Key_name: fk_cust_id
 Seq_in_index: 1
  Column_name: cust_id
    Collation: A
  Cardinality: 0
     Sub_part: NULL
       Packed: NULL
         Null: YES
   Index_type: BTREE
      Comment: 
Index_comment: 
      Visible: YES
   Expression: NULL
2 rows in set (0.01 sec)

mysql> SELECT * FROM INFORMATION_SCHEMA.TABLE_COSTRAINTS WHERE CONSTRAINT_SCHEMA = 'tes'\G
ERROR 1109 (42S02): Unknown table 'TABLE_COSTRAINTS' in information_schema
mysql> SELECT * FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS WHERE CONSTRAINT_SCHEMA = 'tes'\G
Empty set (0.00 sec)

mysql> DESCRIBE orders;
+--------------+--------------+------+-----+---------+-------+
| Field        | Type         | Null | Key | Default | Extra |
+--------------+--------------+------+-----+---------+-------+
| order_id     | int          | NO   | PRI | NULL    |       |
| cust_id      | int          | YES  | MUL | NULL    |       |
| product_type | varchar(255) | YES  |     | NULL    |       |
| quantity     | int          | YES  |     | NULL    |       |
| order_date   | date         | YES  |     | NULL    |       |
+--------------+--------------+------+-----+---------+-------+
5 rows in set (0.00 sec)

mysql> ALTER TABLE orders MODIFY quantity INT DEFAULT 1;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESCRIBE orders;
+--------------+--------------+------+-----+---------+-------+
| Field        | Type         | Null | Key | Default | Extra |
+--------------+--------------+------+-----+---------+-------+
| order_id     | int          | NO   | PRI | NULL    |       |
| cust_id      | int          | YES  | MUL | NULL    |       |
| product_type | varchar(255) | YES  |     | NULL    |       |
| quantity     | int          | YES  |     | 1       |       |
| order_date   | date         | YES  |     | NULL    |       |
+--------------+--------------+------+-----+---------+-------+
5 rows in set (0.00 sec)

mysql> SHOW INDEX FROM customers\G
*************************** 1. row ***************************
        Table: customers
   Non_unique: 0
     Key_name: PRIMARY
 Seq_in_index: 1
  Column_name: cust_id
    Collation: A
  Cardinality: 0
     Sub_part: NULL
       Packed: NULL
         Null: 
   Index_type: BTREE
      Comment: 
Index_comment: 
      Visible: YES
   Expression: NULL
*************************** 2. row ***************************
        Table: customers
   Non_unique: 0
     Key_name: username
 Seq_in_index: 1
  Column_name: username
    Collation: A
  Cardinality: 0
     Sub_part: NULL
       Packed: NULL
         Null: 
   Index_type: BTREE
      Comment: 
Index_comment: 
      Visible: YES
   Expression: NULL
*************************** 3. row ***************************
        Table: customers
   Non_unique: 1
     Key_name: last_name # <-- Renaming INDEX
 Seq_in_index: 1
  Column_name: last_name # <-- Renaming INDEX
    Collation: A
  Cardinality: 0
     Sub_part: NULL
       Packed: NULL
         Null: YES
   Index_type: BTREE
      Comment: 
Index_comment: 
      Visible: YES
   Expression: NULL
3 rows in set (0.01 sec)

mysql> ALTER TABLE customers RENAME INDEX last_name TO test;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> SHOW INDEX FROM customers\G
*************************** 1. row ***************************
        Table: customers
   Non_unique: 0
     Key_name: PRIMARY
 Seq_in_index: 1
  Column_name: cust_id
    Collation: A
  Cardinality: 0
     Sub_part: NULL
       Packed: NULL
         Null: 
   Index_type: BTREE
      Comment: 
Index_comment: 
      Visible: YES
   Expression: NULL
*************************** 2. row ***************************
        Table: customers
   Non_unique: 0
     Key_name: username
 Seq_in_index: 1
  Column_name: username
    Collation: A
  Cardinality: 0
     Sub_part: NULL
       Packed: NULL
         Null: 
   Index_type: BTREE
      Comment: 
Index_comment: 
      Visible: YES
   Expression: NULL
*************************** 3. row ***************************
        Table: customers
   Non_unique: 1
     Key_name: test # <-- It has been updated>
 Seq_in_index: 1
  Column_name: last_name # <-- See the change
    Collation: A
  Cardinality: 0
     Sub_part: NULL
       Packed: NULL
         Null: YES
   Index_type: BTREE
      Comment: 
Index_comment: 
      Visible: YES
   Expression: NULL
3 rows in set (0.01 sec)
```
### Drop keys and indexes:
```bash
mysql> ALTER TABLE tb1_name DROP PRIMARY KEY mysql> ALTER TABLE tbl_ name DROP FOREIGN KEY fk name;
mysql> ALTER TABLE tbl_name DROP INDEX index_name;
```

Continue with [Deleting](deleting.md)