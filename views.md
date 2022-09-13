# CREATE VIEW Syntax

- Statement
```
CREATE
    [OR REPLACE]
    [ALGORITHM = {UNDEFINED | MERGE | TEMPTABLE}]
    [DEFINER = user]
    [SQL SECURITY { DEFINER | INVOKER }]
    VIEW view_name [(column_list)]
    AS select_statement
    [WITH [CASCADED | LOCAL] CHECK OPTION]
```

The _CREATE VIEW_ statement creates a new view, or replaces an existing view if the _OR REPLACE_ clause is given. If the view does not exist, _CREATE OR REPLACE VIEW_ is the same as _CREATE VIEW_. If the view does exist, _CREATE OR REPLACE VIEW_ replaces it.

## Restrictions

- The SELECT statement cannot refer to system variables or user-defined variables.

- Within a stored program, the SELECT statement cannot refer to program parameters or local variables.

- The SELECT statement cannot refer to prepared statement parameters.

- Any table or view referred to in the definition must exist. If, after the view has been created, a table or view that the definition refers to is dropped, use of the view results in an error. To check a view definition for problems of this kind, use the CHECK TABLE statement.

- The definition cannot refer to a TEMPORARY table, and you cannot create a TEMPORARY view.

- You cannot associate a trigger with a view.

- Aliases for column names in the SELECT statement are checked against the maximum column length of 64 characters (not the maximum alias length of 256 characters).

## Views

### Creating and Deleting Views

#### Create a view.

```
CREATE VIEW view_name AS select_statement;
```
---
```
CREATE VIEW cust_phone AS SELECT last_name, first_name, phone_number
FROM customers ORDER BY last_name;

SHOW TABLES;

# Tables_in_platziblog
'categorias'
'char_varchar'
'comentarios'
'cust_phone'        <--- view (created table)
'customers'
'date_time'
'etiquetas'
'posts'
'posts_etiquetas'
'usuarios'
```

### Run SELECT on a view
---
```
SELET * FROM cust_phone;

# last_name	first_name	phone_number
Balwin	Alec	2345678901
Kent	Clark	9992323233
Penn	Sean	3214567890
Perez	Juan	2344560987
Walter	Pancho	3239876543
Wayne	Bruce	3333333333

SELECT * FROM cust_phone WHERE last_name = 'Wayne';

# last_name	first_name	phone_number
Wayne	Bruce	3333333333
```

### Deleting a view (created view)

```
DROP VIEW view_name;
```
---
```
DROP VIEW cust_phone;

SHOW TABLES;

# Tables_in_platziblog
categorias
char_varchar
comentarios
customers
date_time
etiquetas
posts
posts_etiquetas
usuarios
```

As shown in the code section, the view that it was created is not longer displayed because it was DROP in the last statement.
Views can be more complicated but this is just a demonstration on how views behave.