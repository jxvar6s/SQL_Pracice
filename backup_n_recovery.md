# Backup and Recovery

## Physical Backups

1. This type of backup is a copy of the database, directories and 
files (data files, data controls, and archived logs)

2. They can be faster than logical backups.

3. It is more compact than a logical backup.

4. It can be a single file or the entire directory.

5. If [MySQL sever](https://www.mysql.com) is shutdown then
a backup can be performed.

6. System level command can be used:

    - cp, tar, rsync
    - mysqlbackup tool

## Logical Backups

1. The data of a table is also exported using SQL syntax and this is 
stored in binary format.

2. It is a good option to restore or move the database to another
environment.

3. It is larger than physical backup in size.

4. Backups must be performed while the server is running.

5. It can be performed using the following:

    - mysqldump tool
    - SELECT...INTO OUTFILE statement.


### MySQL Statements and System Commands.


> Let's show our databases.

```bash
# mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 16
Server version: 8.0.26 MySQL Community Server - GPL

Copyright (c) 2000, 2021, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> SHOW DATABASES ;
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
8 rows in set (0.01 sec)

mysql> SHOW TABLES FROM prod;
+----------------+
| Tables_in_prod |
+----------------+
| customers      |
| customers_test |
+----------------+
2 rows in set (0.01 sec)

mysql> SHOW TABLES FROM test;
Empty set (0.00 sec)

mysql> SHOW TABLES FROM dev;
Empty set (0.00 sec)

mysql> USE test;

mysql> CREATE TABLE customers SELECT * FROM prod.customers;
Query OK, 3 rows affected (0.04 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> SHOW TABLES FROM test
    -> ;
+----------------+
| Tables_in_test |
+----------------+
| customers      |
+----------------+
1 row in set (0.02 sec)

mysql> SHOW TABLES FROM dev;
+---------------+
| Tables_in_dev |
+---------------+
| customers     |
+---------------+
1 row in set (0.00 sec)
```

Let's go to the command line prompt, we will backup the entire
database with the following command.

---

```bash
# mysqldump -u root -p --all-databases > full_bkp.sql
Enter password: 
#
# echo "Enter the next line to see the content of the file..."
#
# vim full_bkp.sql
```

Backup specific databases:

---
```bash
# mysqldump -u root -p --databases dev test > devtest_bkp.sql
Enter password: 
```

Backup specific tables from a database:

---
```bash
# mysqldump -u root -p test customers > test_cust_bkp.sql
Enter password: 
```

To restore a backup, we can do it use either one of the following
commands but firstable we need to show the databases and drop some
of the for demonstration purposes.

---
```bash
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

mysql> DROP DATABASE dev;
Query OK, 1 row affected (0.06 sec)

mysql> DROP DATABASE test;
Query OK, 1 row affected (0.01 sec)

mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| prod               |
| random             |
| sys                |
+--------------------+
6 rows in set (0.00 sec)
```

Let's restore it/them.

---

```bash
mysql> source devtest_bkp.sql
Query OK, 0 rows affected (0.01 sec)

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

mysql> SHOW TABLE FROM dev;

mysql> SHOW TABLES FROM dev;
+---------------+
| Tables_in_dev |
+---------------+
| customers     |
+---------------+
1 row in set (0.00 sec)

mysql> SELECT * FROM dev.customers;
+---------+----------+------------+-----------+--------------+
| cust_id | username | first_name | last_name | phone_number |
+---------+----------+------------+-----------+--------------+
|       1 | bwayne   | bruce      | wayne     | 2222222222   |
|       2 | pparker  | peter      | parker    | 3333333333   |
|       3 | tstark   | tony       | stark     | 3333333333   |
+---------+----------+------------+-----------+--------------+
3 rows in set (0.00 sec)

mysql> 
```

### Creating Backups in Delimited-Text Format.

Let's see what is the secure priv-option dir to restrict the import/export backups, by using 
the following:

1. Using SELECT...INTO OUTFILE:

> Sintax:
```
mysql> SELECT * FROM dd_name.tbl_name INTO OUTFILE
'/var/lib/mysql-files/dump.txt'
```

```
mysql> SHOW VARIABLES LIKE 'secure_file_priv';
+------------------+-----------------------+
| Variable_name    | Value                 |
+------------------+-----------------------+
| secure_file_priv | /var/lib/mysql-files/ |
+------------------+-----------------------+
1 row in set (0.01 sec)

mysql> SELECT * FROM test.customers INTO OUTFILE '/var/lib/mysql-files/test_cust_bkp.txt';
Query OK, 3 rows affected (0.00 sec)
```

Let's see if the file was save in the secure_file_priv dir:

```bash
# sudo ls -al /var/lib/mysql-files/
total 12
drwxr-x---   2 mysql mysql 4096 Mar 20 21:49 .
drwxr-xr-x. 32 root  root  4096 Dec 15 22:52 ..
-rw-r-----   1 mysql mysql   97 Mar 20 21:49 test_cust_bkp.txt
```

> Sintax - **mysqldump:**

$ sudo mysqldump -u root -p --tab=/var/lib/mysql-files/ db_name [table_name]

```bash
# sudo mysqldump -u root -p --tab=/var/lib/mysql-files/ dev
Enter password: 
[vagrant@localhost ~]$ sudo ls -al /var/lib/mysql-files/
total 20
drwxr-x---   2 mysql mysql 4096 Mar 20 21:54 .
drwxr-xr-x. 32 root  root  4096 Dec 15 22:52 ..
-rw-r--r--   1 root  root  1510 Mar 20 21:54 customers.sql
-rw-r-----   1 mysql mysql   97 Mar 20 21:54 customers.txt
-rw-r-----   1 mysql mysql   97 Mar 20 21:49 test_cust_bkp.txt
```

2. Restore using delimited-text backups:

```bash
# mysql -u root -p db_name < table_name.sql

# mysqlimport -u root -p db_name table_name.txt
```

Let's do it the folowing way otherwise it will throw an error.

```bash
# sudo sh -c 'mysql -u root -p test < /var/lib/mysql-files/customers.sql'
Enter password: 
#
# sudo mysqlimport -u root -p test /var/lib/mysql-files/customers.txt
Enter password: 
test.customers: Records: 3  Deleted: 0  Skipped: 0  Warnings: 0
#
```

> Continue to [Numeric Types](numeric_types.md) file...
