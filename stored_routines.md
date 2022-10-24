# Stored Routines

## About Stored Routines
- Procedure or function can be a stored routine.
- If stored routine is needed then it has to be associated with a database.
- To create, alter or execute a stored routine a user must have the _CREATE ROUTINE, ALTER ROUTINE, and EXECUTE_ privileges.
- The _CALL_ statement is used to invoke a stored routine.
- Referencing in an expression is needed to invoke sotered functions.

## Procudures

### Create a procedure:
```
mysql> CREATE PROCEDURE proc_name ([proc_param]) routine_body;
```
e.g, Creating a simple SELECT procedure and define the DELIMITER.
```bash
mysql> DELIMITER //
mysql> CREATE PROCEDURE getCustomers()
    -> BEGIN
    -> SELECT * FROM customers;
    -> END//
Query OK, 0 rows affected (0.01 sec)

# # Let's go back to our original DELIMITER (;)
mysql> DELIMITER ;

# # Let's call the PROCEDURE
# #--------------------------------

mysql> CALL getCustomers();
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

Query OK, 0 rows affected (0.00 sec)
```

### List Procedures:
```
mysql> SHOW PROCEDURE STATUS LIKE 'proc_name';
```
```bash
# # e.g, 
mysql> SHOW PROCEDURE STATUS LIKE 'getCustomers'\G
*************************** 1. row ***************************
                  Db: prod
                Name: getCustomers
                Type: PROCEDURE
             Definer: root@localhost
            Modified: 2022-10-23 18:22:09
             Created: 2022-10-23 18:22:09
       Security_type: DEFINER
             Comment: 
character_set_client: utf8mb4
collation_connection: utf8mb4_0900_ai_ci
  Database Collation: utf8mb4_0900_ai_ci
1 row in set (0.00 sec)

# # Let's CALL the PROCEDURE

# # Let's call the PROCEDURE
# #--------------------------------

mysql> CALL getCustomers();
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

Query OK, 0 rows affected (0.00 sec)
```

### Delete a procedure:
```
mysql> DROP PROCEDURE proc_name;
```
```bash
mysql> DROP PROCEDURE getCustomers;
Query OK, 0 rows affected (0.00 sec)

mysql> SHOW PROCEDURE STATUS LIKE 'getCustomers'\G
Empty set (0.00 sec)

```
---
## Working with Functions.

### Create a function
```
mysql> CREATE FUNCTION func_name
([func_param]) RETURN datatype routine_body;
```
```bash
mysql> CREATE FUNCTION hello (s CHAR(20))
    -> RETURNS CHAR(50) DETERMINISTIC
    -> RETURN CONCAT('hello, ',s,'!');
Query OK, 0 rows affected (0.00 sec)

# # Let's use the created function
# #-------------------------------------
mysql> SELECT hello('world');
+----------------+
| hello('world') |
+----------------+
| hello, world!  |
+----------------+
1 row in set (0.00 sec)

# # The string we enter was concatenated with the string parameter define in the function.
# # Let's enter another example.

mysql> SELECT hello('universe')
    -> ;
+-------------------+
| hello('universe') |
+-------------------+
| hello, universe!  |
+-------------------+
1 row in set (0.00 sec)

```

### List functions
```
mysql> SHOW FUNCTION STATUS LIKE 'func_name';
```
```bash
mysql> SHOW FUNCTION STATUS LIKE 'hello'\G
*************************** 1. row ***************************
                  Db: prod
                Name: hello
                Type: FUNCTION
             Definer: root@localhost
            Modified: 2022-10-23 18:47:59
             Created: 2022-10-23 18:47:59
       Security_type: DEFINER
             Comment: 
character_set_client: utf8mb4
collation_connection: utf8mb4_0900_ai_ci
  Database Collation: utf8mb4_0900_ai_ci
1 row in set (0.00 sec)
```

### Delete function:
```
mysql> DROP FUNCTION func_name;
```
```bash
# # Now, Let's DROP (delete) the function and validate there is/are no more function(s).
mysql> DROP FUNCTION hello;
Query OK, 0 rows affected (0.00 sec)

# # Validating

mysql> SHOW FUNCTION STATUS LIKE 'hello'\G
Empty set (0.00 sec)
```

[Continue with EVENTS](events.md)