# Creating and Deleting Users

## CREATE USER Syntax
```bash
CREATE USER [IF NOT EXISTS]
    user [auth_option] [, user [auth_option]] ...
    DEFAULT ROLE role [, role ] ...
    [REQUIRE {NONE | tls_option [[AND] tls_option] ...}]
    [WITH resource_option [resource_option] ...]
    [password_option | lock_option] ...
```
## About Create User
- The _CREATE USER_ statement creates new [MySQL](https://www.mysql.com) accounts.
- To _CREATE USER_ you must have global privilege.

## Create User Overview.
For each account, CREATE USER creates a new row in the mysql.user system table. The account row reflects the properties specified in the statement. Unspecified properties are set to their default values:

- Authentication: The default authentication plugin (determined as described in The Default Authentication Plugin), and empty credentials
- Default role: NONE
- SSL/TLS: NONE
- Resource limits: Unlimited
- Password management: PASSWORD EXPIRE DEFAULT PASSWORD HISTORY DEFAULT PASSWORD REUSE INTERVAL DEFAULT PASSWORD REQUIRE CURRENT DEFAULT; failed-login tracking and temporary account locking are disabled
- Account locking: ACCOUNT UNLOCK

## Creating a new user.
```bash
mysql> CREATE USER 'jeffrey'@'localhost' IDENTIFIED BY 'password';
```
```bash
# echo "Let's create a few users"

mysql> CREATE USER 'bwayne'@'localhost' IDENTIFIED BY 'Linux4me';
Query OK, 0 rows affected (0.03 sec)

mysql> CREATE USER 'ckent'@'localhost' IDENTIFIED BY 'Linux4me';
Query OK, 0 rows affected (0.01 sec)

mysql> CREATE USER 'pparker'@'localhost' IDENTIFIED BY 'Linux4me';
Query OK, 0 rows affected (0.01 sec)

mysql> SELECT User FROM mysql.user;
+------------------+
| User             |
+------------------+
| bwayne           |
| ckent            |
| mysql.infoschema |
| mysql.session    |
| mysql.sys        |
| pparker          |
| root             |
+------------------+
7 rows in set (0.00 sec)

# echo "log in as different user"

# mysql -u bwayne -p
Enter password: <-- Enter password.
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 11
Server version: 8.0.30 MySQL Community Server - GPL

Copyright (c) 2000, 2022, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 

```

## DROP USER Syntax
```bash
DROP USER [IF EXISTS] user [, user] ...
```
## About Drop User.
The _DROP USER_ statement removes one or more [MySQL](https://www.mysql.com) accounts and their privileges.
To use _DROP USER_ you need to have privileges to use it.
### Delete an existing user:
```bash
mysql> DROP USER 'brucewayne'@'localhost';
```

```bash
mysql> DROP USER 'bwayne'@'localhost';
Query OK, 0 rows affected (0.01 sec)

mysql> DROP USER 'ckent'@'localhost';
Query OK, 0 rows affected (0.01 sec)

mysql> DROP USER 'pparker'@'localhost';
Query OK, 0 rows affected (0.00 sec)

mysql> SELECT User FROM mysql.user;
+------------------+
| User             |
+------------------+
| mysql.infoschema |
| mysql.session    |
| mysql.sys        |
| root             |
+------------------+
4 rows in set (0.00 sec)
```

[Granting privileges](granting_privileges.md)