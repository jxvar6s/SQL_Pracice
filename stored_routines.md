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

### List Procedures:
```
mysql> SHOW PROCEDURE STATUS LIKE 'proc_name';
```

### Delete a procedure:
```
mysql> DROP PROCEDURE proc_name;
```

## Working with Functions.

### Create a function
```
mysql> CREATE FUNCTION func_name
([func_param]) RETURN datatype routine_body;
```

### List functions
```
mysql> SHOW FUNCTION STATUS LIKE 'func_name';
```

### Delete function:
```
mysql> DROP FUNCTION func_name;
```