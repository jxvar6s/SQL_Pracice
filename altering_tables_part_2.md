
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