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
### Create an event:
```
mysql> CREATE EVENT event_name ON SHCEDULE schedule DO
event_body;
```
### Show events:
```
mysql> SHOW EVENTS [FROM db_name];
```
### Modify an existing event:
```
mysql> ALTER EVENT event_name [ON SCHEDULE schedule] [DO event_body];
```
### Delete an event:
```
mysql> DROP EVENT event_name;
```
