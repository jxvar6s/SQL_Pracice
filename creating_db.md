# MySQL Syntax

## Creating Databases.
```mysql
CREATE {DATABASE | SCHEMA} [IF NOT EXISTS] db_name [create_spacification]...
```
create_specification:
```mysql
  [DEFAULT] CHARACTER SET [=] charset_name
  | [DEFAULT] COLLATE [=] collation_name
  | DAFAULT ENCRYPTION [=] {'Y' | 'N'}
```
Let's  see the default Character set in our database.
```
mysql> SHOW VARIABLES LIKE 'char%';
+--------------------------+--------------------------------+
| Variable_name            | Value                          |
+--------------------------+--------------------------------+
| character_set_client     | utf8mb4                        |
| character_set_connection | utf8mb4                        |
| character_set_database   | utf8mb4                        |
| character_set_filesystem | binary                         |
| character_set_results    | utf8mb4                        |
| character_set_server     | utf8mb4                        |
| character_set_system     | utf8mb3                        |
| character_sets_dir       | /usr/share/mysql-8.0/charsets/ |
+--------------------------+--------------------------------+
8 rows in set (0.01 sec)
```
Create a new database:
```
msql> CREATE DATABASE random;
Query OK, 1 row affected (0.01 sec)
```
List available databases:
```
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| dev                |
| information_schema |
| mysql              |
| performance_schema |
| prod               |
| random             |
| sys                |
| test               |
+--------------------+
8 rows in set (0.00 sec)
```
Select database for use:
```
mysql> USE prod;
Database changed
```
Show current selected database:
```
mysql> SELECT DATABASE();
+------------+
| DATABASE() |
+------------+
| prod       |
+------------+
1 row in set (0.00 sec)
```
