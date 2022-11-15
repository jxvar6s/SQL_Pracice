# Events

## Events Requirements.
The minimum requirements for a valid CREATE EVENT statement are as follows:

- The keywords CREATE EVENT plus an event name, which uniquely identifies the event in a database schema.
- An ON SCHEDULE clause, which determines when and how often the event executes.
- A DO clause, which contains the SQL statement to be executed by an event.

### Turning Event Scheduler on or off:
```
mysql> SET GLOBAL event_scheduler = ON|OFF;
```
### Show Events
```
mysql> SHOW PROCESSLIST\G
*************************** 1. row ***************************
     Id: 5
   User: event_scheduler
   Host: localhost
     db: NULL
Command: Daemon
   Time: 118083
  State: Waiting on empty queue
   Info: NULL
*************************** 2. row ***************************
     Id: 9
   User: root
   Host: localhost
     db: NULL
Command: Query
   Time: 0
  State: init
   Info: SHOW PROCESSLIST
2 rows in set (0.00 sec)

mysql> 
```
### Create an event:
```
mysql> CREATE EVENT event_name ON SHCEDULE schedule DO
event_body;
```
```
CREATE EVENT test ON SCHEDULE AT '2022-11-15 02:00:00' DO SELECT * FROM customers;
```
### Show events:
```
mysql> SHOW EVENTS [FROM db_name];
```
```
mysql> SHOW EVENTS FROM prod\G
*************************** 1. row ***************************
                  Db: prod
                Name: test
             Definer: root@localhost
           Time zone: SYSTEM
                Type: ONE TIME
          Execute at: 2022-11-15 02:00:00
      Interval value: NULL
      Interval field: NULL
              Starts: NULL
                Ends: NULL
              Status: ENABLED
          Originator: 1
character_set_client: utf8mb4
collation_connection: utf8mb4_0900_ai_ci
  Database Collation: utf8mb4_0900_ai_ci
1 row in set (0.00 sec)
```

### Modify an existing event:
```
mysql> ALTER EVENT event_name [ON SCHEDULE schedule] [DO event_body];
```
```bash
# echo "Altering the event and showing its alteration.
mysql> ALTER EVENT test DO SELECT * FROM customers_test;
Query OK, 0 rows affected (0.01 sec)

mysql> SHOW CREATE EVENT test\G
*************************** 1. row ***************************
               Event: test
            sql_mode: ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION
           time_zone: SYSTEM
        Create Event: CREATE DEFINER=`root`@`localhost` EVENT `test` ON SCHEDULE AT '2022-11-15 02:00:00' ON COMPLETION NOT PRESERVE ENABLE DO SELECT * FROM customers_test
character_set_client: utf8mb4
collation_connection: utf8mb4_0900_ai_ci
  Database Collation: utf8mb4_0900_ai_ci
1 row in set (0.00 sec)
```
### Delete an event:
```
mysql> DROP EVENT event_name;
```
```bash
mysql> DROP EVENT test;
Query OK, 0 rows affected (0.00 sec)

# echo 'Showing that events have been dropped
mysql> SHOW EVENTS FROM prod;
Empty set (0.01 sec)
```

[Creating and Deleting Users](create_delete_users.md)