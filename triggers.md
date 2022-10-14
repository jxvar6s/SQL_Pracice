# Triggers

## CREATE TRIGGER _Syntax_
```
CREATE
    [DEFINER = user]
    TRIGGER trigger_name
    trigger_time trigger_event
    ON tbl_name FOR EACH ROW
    [trigger_order]
    trigger_body
```

## About Triggers

- Triggers can be set to activate before or after a tigger event occurs.
- You cannot associate a trigger with a TEMPORARY table or a view.
- Triggers activate whenever a statement inserts, updates, or deletes row s in associated table. These are known as trigger events.

Let's see what we have in our customers table.
```
mysql> SELECT * FROM customers;
+---------+----------+------------+-----------+--------------+
| cust_id | username | first_name | last_name | phone_number |
+---------+----------+------------+-----------+--------------+
|       1 | bwayne   | bruce      | wayne     | 2222222222   |
|       2 | pparker  | peter      | parker    | 3333333333   |
|       3 | tstark   | tony       | stark     | 3333333333   |
|       4 | ptrbread | peter      | pan       | 2222345678   |
|       5 | wwwilson | wade       | wilson    | 3239998765   |
+---------+----------+------------+-----------+--------------+
5 rows in set (0.00 sec)
```
By creating an _EVENT_, it will update the following _table_.
```
DESCRIBE audit;
+--------------+-------------+------+-----+---------+-------+
| Field        | Type        | Null | Key | Default | Extra |
+--------------+-------------+------+-----+---------+-------+
| username     | varchar(25) | YES  |     | NULL    |       |
| phone_number | varchar(25) | YES  |     | NULL    |       |
| change_date  | datetime    | YES  |     | NULL    |       |
+--------------+-------------+------+-----+---------+-------+
3 rows in set (0.01 sec)
```


## Create Trigger:
```
mysql> CREATE TRIGGER trigger_name trigger_time
trigger_event ON table_name FOR EACH ROW trigger_body;
```

## Show Triggers:
```
mysql> SHOW TRIGGER [FROM db_name];
```

## Drop Trigger:
```
mysql> DROP TRIGGER [db_name.]trigger_name;
```
---
### Code Samples
---
Let's see what we have in our customers table.
```
mysql> SELECT * FROM customers;
+---------+----------+------------+-----------+--------------+
| cust_id | username | first_name | last_name | phone_number |
+---------+----------+------------+-----------+--------------+
|       1 | bwayne   | bruce      | wayne     | 2222222222   |
|       2 | pparker  | peter      | parker    | 3333333333   |
|       3 | tstark   | tony       | stark     | 3333333333   |
|       4 | ptrbread | peter      | pan       | 2222345678   |
|       5 | wwwilson | wade       | wilson    | 3239998765   |
+---------+----------+------------+-----------+--------------+
5 rows in set (0.00 sec)
```
By creating an _EVENT_, it will update the following _table_.
```
DESCRIBE audit;
+--------------+-------------+------+-----+---------+-------+
| Field        | Type        | Null | Key | Default | Extra |
+--------------+-------------+------+-----+---------+-------+
| username     | varchar(25) | YES  |     | NULL    |       |
| phone_number | varchar(25) | YES  |     | NULL    |       |
| change_date  | datetime    | YES  |     | NULL    |       |
+--------------+-------------+------+-----+---------+-------+
3 rows in set (0.01 sec)
```

The _trigger_ will be as follows 'simple example':

```
mysql> CREATE TRIGGER update_trigger BEFORE UPDATE on customers FOR EACH ROW INSERT INTO audit
(username,phone_number,change_date) VALUES (OLD.username,OLD.phone_number,NOW());
Query OK, 0 rows affected (0.01 sec)

mysql> SHOW TRIGGERS\G
*************************** 1. row ***************************
             Trigger: update_trigger
               Event: UPDATE
               Table: customers
           Statement: INSERT INTO audit (username,phone_number,change_date) VALUES (OLD.username,OLD.phone_number,NOW())
              Timing: BEFORE
             Created: 2022-10-13 20:47:10.51
            sql_mode: ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION
             Definer: root@localhost
character_set_client: utf8mb4
collation_connection: utf8mb4_0900_ai_ci
  Database Collation: utf8mb4_0900_ai_ci
1 row in set (0.01 sec)
```
Let's create a couple new update and display the tables before the update and after the update.
```
mysql> UPDATE customers SET username = 'brucew' WHERE cust_id = '2';
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> UPDATE customers SET phone_number = '4444444444' WHERE cust_id = '1';
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```
```bash
# Before the - UPDATE -

mysql> SELECT * FROM audit;
+----------+--------------+---------------------+
| username | phone_number | change_date         |
+----------+--------------+---------------------+
| pparker  | 3333333333   | 2022-10-13 20:56:31 |
| bwayne   | 2222222222   | 2022-10-13 20:58:15 |
+----------+--------------+---------------------+
2 rows in set (0.00 sec)


# After the  - UPDATE - 
mysql> SELECT * FROM customers;
+---------+----------+------------+-----------+--------------+
| cust_id | username | first_name | last_name | phone_number |
+---------+----------+------------+-----------+--------------+
|       1 | bwayne   | bruce      | wayne     | 4444444444   | # <-- Updated record
|       2 | brucew   | peter      | parker    | 3333333333   | # <-- Updated record
|       3 | tstark   | tony       | stark     | 3333333333   |
|       4 | ptrbread | peter      | pan       | 2222345678   |
|       5 | wwwilson | wade       | wilson    | 3239998765   |
+---------+----------+------------+-----------+--------------+
5 rows in set (0.00 sec)


# Let's delete / drop the TRIGGER
mysql> DROP TRIGGER prod.update_trigger;
Query OK, 0 rows affected (0.00 sec)

mysql> SHOW TRIGGERS\G
Empty set (0.01 sec)
```

[Store Routines](stored_routines.md)