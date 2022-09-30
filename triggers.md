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