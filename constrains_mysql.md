# Constrains in [MySQL](https://www.mysql.com)

1 - **NOt NULL** prevents values null values from being entered into a column.
This enforces a field to always containt a value.
    
    column_name data_type NOT NULL

2 - **UNIQUE** ensures that all the values in a column are different.
_UNIQUE_ and _PRIMARY KEY_ are examples of uniqueness.

    column_name data_type UNIQUE

3 - **PRIMARY KEY** constraint uniquely identifies each record in a table.

    column_name data_type PRIMARY KEY

4 - **FOREIGN KEY** constraint is used to prevent actions that would destroy links between tables.
A FOREIGN KEY is a field (or collection of fields) in one table, that refers to the PRIMARY KEY in another table.
This allows related data to be cross-referenced in order to keep it consistent.

    FOREIGN KEY [index_name] (column_name,...)
    REFERENCES table_name(column_name,...)

5 - **CHECK** Determines whether a value is valid based on specific conditions.

    column_name data_type CHECK(expression)

6 - **DEFAULT** constraint is used to set a default value for a column.
The default value will be added to all new records, if no other value is specified.

    column_name data_type DEFAULT value.

> Continue on [Backup and Recovery](backup_n_recovery.md) file ...