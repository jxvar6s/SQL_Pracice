# MySQL Syntax

## Creating Databases Part 1.
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
> '%' is a wildcard in [MySQL](https://www.mysql.com)
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
Create 3 new databases, dev, test, random:
> **Note:** All _Unix_ systems are case sensitive.
```
msql> CREATE DATABASE random;
Query OK, 1 row affected (0.01 sec)

mysql> CREATE DATABASE dev;
Query OK, 1 row affected (0.00 sec)

mysql> CREATE DATABASE test;
Query OK, 1 row affected (0.00 sec)
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

> Let's exit [MySQL DB](https://www.mysql.com)

```
mysql> exit
```

When logging in to **MySQL**, a database can be selected.
```
mysql> mysql -u [user] -p db_name;
```

The following syntax is for dropping a DATABASE.
```
DROP {DATABASE | SCHEMA} [IF EXISTS] db_name
```

Delete a database Syntax.
```
mysql> DROP DATABASE db_name;
```
Let's create a database to demotrate _DROP DATABASE_ command
```
mysql> mysql> CREATE DATABASE bad_data;
Query OK, 1 row affected (0.01 sec)

mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| bad_data           |
| dev                |
| information_schema |
| mysql              |
| performance_schema |
| prod               |
| random             |
| sys                |
| test               |
+--------------------+
9 rows in set (0.00 sec)
```

By listing the available tables, we can notice that
the dropped table no longer exists.
```
mysql> DROP DATABASE bad_data;
Query OK, 0 rows affected (0.00 sec)

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

## Creating Databases Part 2.

From *Command Line*, We can use _mysqladmin_ and _mysqlshow_.

- mysqladmin Syntax.

$ mysql [options] command [command-arg] [command [command-arg]]

- mysqlshow Syntax.

$ mysqlshow [options] [db_name [table_name [column_name]]]

- Drop a database:

$ mysqladmin -u root -p drop db_name

> Note: Remember the following flags.
- -u flag -> user
- -p flag -> It will prompt you for password.

```bash
# mysqladmin -u root -p create good_demo
Enter password:
# mysqlshow -u root -p
Enter password:
+--------------------+
|     Databases      |
+--------------------+
| dev                |
| good_demo          |
| information_schema |
| mysql              |
| performance_schema |
| prod               |
| random             |
| sys                |
| test               |
+--------------------+
# mysqladmin -u root -p drop good_demo
Enter password:
Dropping the database is potentially a very bad thing to do.
Any data stored in the database will be destroyed.

Do you really want to drop the 'good_demo' database [y/N] y
Database "good_demo" dropped

# mysqlshow -u root -p
Enter password:
+--------------------+
|     Databases      |
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
```
As we can see, good_demo database no longer exist.

---


> Note: Continue with [creating tables](creating_tables.md) file...
