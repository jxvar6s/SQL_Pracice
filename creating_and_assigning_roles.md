# Creating and Assigning Roles.
## Working with Roles
A role is a collection of privileges.

### Create roles:
```
mysql> CREATE ROLE role1 [, role2]...
```
### Assign privilege to roles:
```
mysql> GRANT priv_type ON priv_level to role;
```
### Assign roles to users:
```
mysql> GRANT role TO 'user'@'host';
```
### Show roles for a user:
```
mysql> SHOW GRANTS FOR 'user'@'host';
mysql> SHOW GRANTS FOR 'user'@'host' USING role;
```
### Display roles using the current_role() function:
```
mysql> SELECT current_role();
```
### Set default roles for user:
```
mysql> SET DEFAULT ROLE ALL TO 'user'@'host';
```
### Remove a role from user:
```
mysql> REVOKE role FROM 'user'@'host';
```
### Delete a role:
```
mysql> DROP ROLE role [, role];
```
## SQL Examples.
```bash
mysql> CREATE ROLE prod_read;
Query OK, 0 rows affected (0.02 sec)

mysql> CREATE ROLE prod_write, prod_all;
Query OK, 0 rows affected (0.00 sec)

mysql> GRANT SELECT ON prod.* TO prod_read;
Query OK, 0 rows affected (0.00 sec)

mysql> GRANT INSERT, UPDATE, DELETE ON prod.* TO prod_write;
Query OK, 0 rows affected (0.01 sec)

mysql> GRANT ALL ON prod.* TO prod_all;
Query OK, 0 rows affected (0.01 sec)

# echo "let's grant the role to user bwayne"
mysql> GRANT prod_read TO 'bwayne'@'localhost';
Query OK, 0 rows affected (0.00 sec)

mysql> GRANT prod_all TO 'kenny'@'localhost';
Query OK, 0 rows affected (0.00 sec)

mysql> SHOW GRANTS FOR 'stosh'@'localhost';
+---------------------------------------------------------------------------------------+
| Grants for stosh@localhost                                                            |
+---------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO `stosh`@`localhost`                                             |
| GRANT SELECT (`first_name`, `last_name`) ON `prod`.`customers` TO `stosh`@`localhost` |
| GRANT `prod_read`@`%`,`prod_write`@`%` TO `stosh`@`localhost`                         |
+---------------------------------------------------------------------------------------+
3 rows in set (0.01 sec)

mysql> SHOW GRANTS FOR 'stosh'@'localhost' USING prod_write;
+---------------------------------------------------------------------------------------+
| Grants for stosh@localhost                                                            |
+---------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO `stosh`@`localhost`                                             |
| GRANT INSERT, UPDATE, DELETE ON `prod`.* TO `stosh`@`localhost`                       |
| GRANT SELECT (`first_name`, `last_name`) ON `prod`.`customers` TO `stosh`@`localhost` |
| GRANT `prod_read`@`%`,`prod_write`@`%` TO `stosh`@`localhost`                         |
+---------------------------------------------------------------------------------------+
4 rows in set (0.01 sec)

mysql> SHOW GRANTS FOR 'stosh'@'localhost' USING prod_write;
+---------------------------------------------------------------------------------------+
| Grants for stosh@localhost                                                            |
+---------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO `stosh`@`localhost`                                             |
| GRANT INSERT, UPDATE, DELETE ON `prod`.* TO `stosh`@`localhost`                       |
| GRANT SELECT (`first_name`, `last_name`) ON `prod`.`customers` TO `stosh`@`localhost` |
| GRANT `prod_read`@`%`,`prod_write`@`%` TO `stosh`@`localhost`                         |
+---------------------------------------------------------------------------------------+
4 rows in set (0.01 sec)


# echo "Don't forget to set the roles..."
mysql> SET DEFAULT ROLE ALL TO 'kenny'@'localhost';
Query OK, 0 rows affected (0.00 sec)

mysql> SET DEFAULT ROLE ALL TO 'stosh'@'localhost';
Query OK, 0 rows affected (0.00 sec)

mysql> SET DEFAULT ROLE ALL TO 'bwayne'@'localhost';
Query OK, 0 rows affected (0.00 sec)

mysql> exit

# Let's login as user kenny

# mysql -u kenny -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 9
Server version: 8.0.30 MySQL Community Server - GPL

Copyright (c) 2000, 2022, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> SELECT current_role();
+----------------+
| current_role() |
+----------------+
| `prod_all`@`%` |
+----------------+
1 row in set (0.01 sec)

mysql> USE prod
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> SELECT * FROM customers;
+---------+----------+------------+-----------+--------------+
| cust_id | username | first_name | last_name | phone_number |
+---------+----------+------------+-----------+--------------+
|       1 | bwayne   | bruce      | wayne     | 4444444444   |
|       2 | brucew   | peter      | parker    | 3333333333   |
|       3 | tstark   | tony       | stark     | 3333333333   |
|       4 | ptrbread | peter      | pan       | 2222345678   |
|       5 | wwwilson | deadpool   | wilson    | 3239998765   |
+---------+----------+------------+-----------+--------------+
5 rows in set (0.00 sec)

mysql> UPDATE customers SET phone_number = '1111111111' WHERE cust_id = 1;
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM customers;
+---------+----------+------------+-----------+--------------+
| cust_id | username | first_name | last_name | phone_number |
+---------+----------+------------+-----------+--------------+
|       1 | bwayne   | bruce      | wayne     | 1111111111   |
|       2 | brucew   | peter      | parker    | 3333333333   |
|       3 | tstark   | tony       | stark     | 3333333333   |
|       4 | ptrbread | peter      | pan       | 2222345678   |
|       5 | wwwilson | deadpool   | wilson    | 3239998765   |
+---------+----------+------------+-----------+--------------+
5 rows in set (0.00 sec)

# Let's remove roles

mysql> REVOKE prod_write FROM 'stosh'@'localhost';
Query OK, 0 rows affected (0.01 sec)

mysql> SHOW GRANTS FOR 'stosh'@'localhost';
+---------------------------------------------------------------------------------------+
| Grants for stosh@localhost                                                            |
+---------------------------------------------------------------------------------------+
| GRANT USAGE ON *.* TO `stosh`@`localhost`                                             |
| GRANT SELECT (`first_name`, `last_name`) ON `prod`.`customers` TO `stosh`@`localhost` |
| GRANT `prod_read`@`%` TO `stosh`@`localhost`                                          |
+---------------------------------------------------------------------------------------+
3 rows in set (0.00 sec)

mysql> DROP ROLE prod_all;
Query OK, 0 rows affected (0.00 sec)
```
This is all about assigning roles for now.

[Creating tables with constraints](tables_with_constraints.md)