# MySQL Basics

SQL is used to manage data and database systems futermore it is a widely used programing language.

**Note:** _The following steps are merely for educational purposes and they do not intent to be the only way to approach to SQL Language, as result; there are one to many forms to solve a problem._

Fileds where SQL can be used:
   - Mapping Neurons.
   - Science Researcher
   - Data Analytics
   - etc...

SQL (It was SEQUEL in 1974) can also help anybody to tell his/her/their interesting stories in data.
  
The following terms can be beneficial for managing data.  
   1. summarize.
   2. explore.
   3. collect.
   4. modify.
   5. etc...

## Installation

### CentOS 7

Software tools used in this journey and an assumption has been made that the reader knows how to use _*vagrant*_

 - [Vagrant](https://www.vagrantup.com)
 - [centOS/7 box](https://app.vagrantup.com/jasonc/boxes/centos7)
 - MySQL community edition (links on description)
     - mysql-8.0.26-1.el7.x86_64.rpm-bundle.tar (file)
     - [MySQL-8](https://downloads.mysql.com/archives/get/p/23/file/mysql-8.0.26-1.el7.x86_64.rpm-bundle.tar)

[MySQL Downloads](https://www.mysql.com/downloads/)

Click on _MySQL Community (GPL) Downloads_.
![](/Images/mysql_download.png)

It will take you to a list of links and make sure you click on _Download
Archives_.
![](/Images/archive.png)

On MySQL Product Archives page, click on _MySQL Community Server_.
![](/Images/mysql_server.png)

On this page, choose the version you want to use en click _download_
![](/Images/product_archive.png)

Once your download is clompleted, change to your default download directory 
to extract the _.tar_ file.

In my case is a budle file _mysql-8.0.26-1.el7.x86_64.rpm-bundle.tar_
base on my selection in the previous image.

1. Extract the _RPM_ file from [MySQL](https://www.mysql.com)
```bash
# tar -vxf mysql-8.0.26-1.el7.x86_64.rpm-bundle.tar
```
> After the extraction:
```bash
# ls
mysql-community-client-8.0.26-1.el7.x86_64.rpm
mysql-community-client-plugins-8.0.26-1.el7.x86_64.rpm
mysql-community-common-8.0.26-1.el7.x86_64.rpm
mysql-community-devel-8.0.26-1.el7.x86_64.rpm
mysql-community-embedded-compat-8.0.26-1.el7.x86_64.rpm
mysql-community-libs-8.0.26-1.el7.x86_64.rpm
mysql-community-libs-compat-8.0.26-1.el7.x86_64.rpm
mysql-community-server-8.0.26-1.el7.x86_64.rpm
mysql-community-test-8.0.26-1.el7.x86_64.rpm
```
2. The following command will install the _RPM_ dependencies needed
for _MySQL_ server installation.

```bash
# sudo rpm -Uvh mysql-community-{server,client,common,libs}-*
```
4. Do not forget to start and enable [MySQL](https://www.mysql.com) server.
```bash
# sudo systemctl start mysqld
# sudo systemctl status mysqld
# sudo systemctl enable mysqld
```
5. Do not forget to change/update default root password in MySQL
server.
> We can look for _password_ line in the following file.

```bash
# sudo less /var/log/mysqld.log
```
> Or look for it as follows:

```bash
#sudo grep "temporary password" /var/log/mysqld.log
```
> output
```bash
 51 2021-12-16T03:53:39.289950Z 6 [Note] [MY-010454] [Server] A temporary password is generated 
 for root@local    host: 7tq_d&%:dg*Y
```

6. Let's change the default _password_.
```bash
# sudo -i
# mysql -u root -p
Enter password        <- "Enter default password"

Welcome to the MySQL monitor.  Commands end with ; or \g.
lessYour MySQL connection id is 8
Server version: 8.0.26
 
Copyright (c) 2000, 2021, Oracle and/or its affiliates. 

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>   "This is mysql prompt"

mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'your_new_password';
Query OK, 0 rows affected (0.04 sec)

mysql> exit
Bye
```
7. Let's test our new passwor and secure our installation.
```bash
# mysql_secure_installation

Securing the MySQL server deployment.

Enter password for user root:  <- "Enter your password"
The 'validate_password' component is installed on the server.The subsequent steps will run with the existing configuration
of the component.
Using existing password for root.

Estimated strength of the password: 100
Change the password for root ? ((Press y|Y for Yes, any other key for No) :

... skipping.
By default, a MySQL installation has an anonymous user,
allowing anyone to log into MySQL without having to have
a user account created for them. This is intended only for
testing, and to make the installation go a bit smoother.
You should remove them before moving into a production
environment.

Remove anonymous users? (Press y|Y for Yes, any other key for No) : y
Success.
Normally, root should only be allowed to connect from
'localhost'. This ensures that someone cannot guess at
the root password from the network.

Disallow root login remotely? (Press y|Y for Yes, any other key for No) : y
Success.
 
By default, MySQL comes with a database named 'test' that
anyone can access. This is also intended only for testing,
and should be removed before moving into a production
environment.


Remove test database and access to it? (Press y|Y for Yes, any other key for No) : y
- Dropping test database...
Success.

- Removing privileges on test database...
Success.

Reloading the privilege tables will ensure that all changes
made so far will take effect immediately.

Reload privilege tables now? (Press y|Y for Yes, any other key for No) : y
Success.
 
All done!
```


> Note: To be continnued -- update expected.