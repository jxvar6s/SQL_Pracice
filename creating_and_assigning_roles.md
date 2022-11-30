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