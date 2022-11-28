# Granting Privileges

## GRANT Syntax
```
GRANT
    priv_type [(column_list)]
      [, priv_type [(column_list)]] ...
    ON [object_type] priv_level
    TO user_or_role [, user_or_role] ...
    [WITH GRANT OPTION]
```
## Privileg Levels.
The GRANT statement enables system administrators to grant privileges and roles, which can be granted to user accounts and roles. These syntax restrictions apply:
- GRANT cannot mix granting both privileges and roles in the same statement. A given GRANT statement must grant either privileges or roles.
- The ON clause distinguishes whether the statement grants privileges or roles:
- With ON, the statement grants privileges.
- Without ON, the statement grants roles.
- It is permitted to assign both privileges and roles to an account, but you must use separate GRANT statements, each with syntax appropriate to what is to be granted.

Database privileges - Applies to objects in database.
- Usage ON db_name
- Examples CREATE, DROP, etc.
- Store in the mysql.db system table.

Table privileges - Applies to all columns in a table.
- Usage ON db_name tbl_name
- Examples: ALTER, CREATE, DELETE, DROP, INSERT, UPDATE, etc.
- Store in the mysql tables_priv system tables. 

Column privileges - Applies to specific column within a table.
- Usage GRANT priv_type (col1[,col2]) on 
db_name.tbl_name TO 'user'@'host';
- Examples: INSERT, UPDATE, SELECT, etc.
- Stored in the mysql.column_priv system table.

Stored privileges - Applies to store routines such as procedures and functions.
- Usage ON db_name.* or ON db_name.routine_name
- Examples: ALTER ROUTINE, EXECUTE, etc.
- Stored in the mysql: procs.priv system table

Proxy user privileges - Allows a user to be a proxy for another user.
- Usage GRANT PROXY ON
'localuser'@'localhost' TO
'externaluser'@'externalhost'; <-- user impersonating another user
- The only privilege allowed in the grant proxy statement is PROXY.
- Stored in the mysql proxies_priv system table.

## Working with GRANTS

### Grant privileges to users:
```bash
mysql> GRANT priv_type [(col_list)] ON priv_level
TO 'user'@'host';
```
### Show privileges for a user:
```bash
mysql> SHOW GRANTS FOR 'ser'@'host';
```
### Revoke privileges from user:
```bash
mysql> REVOKE priv_type [(col_list)] ON priv_level
FROM 'user'@'host';
```

### [MySQL](https://www.mysql.com) Statements Examples

#### Let's create some users and grant them different privileges to each of the users.
```bash
# echo 'User Kenny has access to the entire database prod.'
mysql> CREATE USER 'kenny'@'localhost' IDENTIFIED BY 'Linux4me';
Query OK, 0 rows affected (0.02 sec)

mysql> GRANT ALL ON prod.* TO 'kenny'@'localhost';
Query OK, 0 rows affected (0.00 sec)

# echo 'User bwayne has access to table customer in database prod.
mysql> CREATE USER 'bwayne'@'localhost' IDENTIFIED BY 'Linux4me';
Query OK, 0 rows affected (0.01 sec)

mysql> GRANT SELECT ON prod.customers TO 'bwayne'@'localhost';
Query OK, 0 rows affected (0.00 sec)
```

Next case user will have access to specific columns, as follows:
```bash
mysql> CREATE USER 'stosh'@'localhost' IDENTIFIED BY 'Linux4me';
Query OK, 0 rows affected (0.00 sec)

mysql> GRANT SELECT (first_name, last_name), UPDATE (first_name, last_name) ON prod.customers TO 'stosh'@'localhost';
Query OK, 0 rows affected (0.00 sec)

# echo 'Let's show stosh's user privileges.
mysql> SHOW GRANTS FOR 'stosh'@'localhost';
+---------------------------------------------------------------------------------------------------------------------------+
| Grants for stosh@localhost                                                                                                |
+---------------------------------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO `stosh`@`localhost`                                                                                 |
| GRANT SELECT (`first_name`, `last_name`), UPDATE (`first_name`, `last_name`) ON `prod`.`customers` TO `stosh`@`localhost` |
+---------------------------------------------------------------------------------------------------------------------------+
2 rows in set (0.00 sec)

# echo "Let's show the rest of the users privileges.
mysql> SHOW GRANTS FOR 'kenny'@'localhost';
+---------------------------------------------------------+
| Grants for kenny@localhost                              |
+---------------------------------------------------------+
| GRANT USAGE ON *.* TO `kenny`@`localhost`               |
| GRANT ALL PRIVILEGES ON `prod`.* TO `kenny`@`localhost` |
+---------------------------------------------------------+
2 rows in set (0.00 sec)

mysql> SHOW GRANTS FOR 'bwayne'@'localhost'
    -> ;
+------------------------------------------------------------+
| Grants for bwayne@localhost                                |
+------------------------------------------------------------+
| GRANT USAGE ON *.* TO `bwayne`@`localhost`                 |
| GRANT SELECT ON `prod`.`customers` TO `bwayne`@`localhost` |
+------------------------------------------------------------+
2 rows in set (0.00 sec)
```
#### Testing user access.
```bash
# mysql -u kenny -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 10
Server version: 8.0.30 MySQL Community Server - GPL

Copyright (c) 2000, 2022, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> USE prod;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> SHOW TABLES
    -> ;
+----------------+
| Tables_in_prod |
+----------------+
| audit          |
| customers      |
| customers_test |
+----------------+
3 rows in set (0.00 sec)

mysql> SELECT * FROM customers_test;
Empty set (0.01 sec)

mysql> SELECT * FROM customers;
+---------+----------+------------+-----------+--------------+
| cust_id | username | first_name | last_name | phone_number |
+---------+----------+------------+-----------+--------------+
|       1 | bwayne   | bruce      | wayne     | 4444444444   |
|       2 | brucew   | peter      | parker    | 3333333333   |
|       3 | tstark   | tony       | stark     | 3333333333   |
|       4 | ptrbread | peter      | pan       | 2222345678   |
|       5 | wwwilson | wade       | wilson    | 3239998765   |
+---------+----------+------------+-----------+--------------+
5 rows in set (0.00 sec)

mysql> SELECT * FROM audit;
+----------+--------------+---------------------+
| username | phone_number | change_date         |
+----------+--------------+---------------------+
| pparker  | 3333333333   | 2022-10-13 20:56:31 |
| bwayne   | 2222222222   | 2022-10-13 20:58:15 |
+----------+--------------+---------------------+
2 rows in set (0.00 sec)


# echo 'In the following example, we will see that user kenny does not have access to test database.'
mysql> USE test;
ERROR 1044 (42000): Access denied for user 'kenny'@'localhost' to database 'test'
mysql> SELECT * FROM test.customers;
ERROR 1142 (42000): SELECT command denied to user 'kenny'@'localhost' for table 'customers'
```

Let's check the other users access.
```bash
# mysql -u bwayne -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 11
Server version: 8.0.30 MySQL Community Server - GPL

Copyright (c) 2000, 2022, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> USE prod;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed

mysql> SELECT * FROM customers
    -> ;
+---------+----------+------------+-----------+--------------+
| cust_id | username | first_name | last_name | phone_number |
+---------+----------+------------+-----------+--------------+
|       1 | bwayne   | bruce      | wayne     | 4444444444   |
|       2 | brucew   | peter      | parker    | 3333333333   |
|       3 | tstark   | tony       | stark     | 3333333333   |
|       4 | ptrbread | peter      | pan       | 2222345678   |
|       5 | wwwilson | wade       | wilson    | 3239998765   |
+---------+----------+------------+-----------+--------------+
5 rows in set (0.00 sec)

mysql> SELECT * FROM customers_test;
ERROR 1142 (42000): SELECT command denied to user 'bwayne'@'localhost' for table 'customers_test'

mysql> exit

# mysql -u stosh -p 
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 12
Server version: 8.0.30 MySQL Community Server - GPL

Copyright (c) 2000, 2022, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> USE prod;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changedmysql> SELECT * FROM customers;
ERROR 1143 (42000): SELECT command denied to user 'stosh'@'localhost' for column 'cust_id' in table 'customers'

mysql> SELECT last_name FROM customers;
+-----------+
| last_name |
+-----------+
| wayne     |
| parker    |
| stark     |
| pan       |
| wilson    |
+-----------+
5 rows in set (0.00 sec)

mysql> SELECT first_name FROM customers;
+------------+
| first_name |
+------------+
| bruce      |
| peter      |
| tony       |
| peter      |
| wade       |
+------------+
5 rows in set (0.01 sec)

mysql> SELECT first_name, last_name FROM customers;
+------------+-----------+
| first_name | last_name |
+------------+-----------+
| bruce      | wayne     |
| peter      | parker    |
| tony       | stark     |
| peter      | pan       |
| wade       | wilson    |
+------------+-----------+
5 rows in set (0.00 sec)

mysql> UPDATE customers SET first_name = 'deadpool' WHERE last_name = 'wilson';
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT first_name, last_name FROM customers;
+------------+-----------+
| first_name | last_name |
+------------+-----------+
| bruce      | wayne     |
| peter      | parker    |
| tony       | stark     |
| peter      | pan       |
| deadpool   | wilson    |
+------------+-----------+
5 rows in set (0.00 sec)

# echo 'As we can see stosh user has only accsess to last_name, first_name columns.
```
#### Revoking grants Example.
Let's login as root.
```bash
# mysql -u root -p  
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 13
Server version: 8.0.30 MySQL Community Server - GPL

Copyright (c) 2000, 2022, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> SHOW GRANTS FOR 'stosh'@'localhost';
+---------------------------------------------------------------------------------------------------------------------------+
| Grants for stosh@localhost                                                                                                |
+---------------------------------------------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO `stosh`@`localhost`                                                                                 |
| GRANT SELECT (`first_name`, `last_name`), UPDATE (`first_name`, `last_name`) ON `prod`.`customers` TO `stosh`@`localhost` |
+---------------------------------------------------------------------------------------------------------------------------+
2 rows in set (0.00 sec)

mysql> REVOKE UPDATE ON prod.customers FROM 'stosh'@'localhost';
Query OK, 0 rows affected (0.01 sec)

mysql> SHOW GRANTS FOR 'stosh'@'localhost';
+---------------------------------------------------------------------------------------+
| Grants for stosh@localhost                                                            |
+---------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO `stosh`@`localhost`                                             |
| GRANT SELECT (`first_name`, `last_name`) ON `prod`.`customers` TO `stosh`@`localhost` |
+---------------------------------------------------------------------------------------+
2 rows in set (0.00 sec)
```
> **NOTE:** Notice that stosh's user __UPDATE__ privileges have been revoke but stosh user can be able to __SELECT__ first_name and last_name columns from prod.customers table.
---
[Creating and assigning roles](creating_and_assigning_roles.md)