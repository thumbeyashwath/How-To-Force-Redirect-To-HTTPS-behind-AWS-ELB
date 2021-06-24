
# Mysql User creation, Permission, Backup
To Create Mysql User:
```shell
CREATE USER ‘new_user’@’localhost’ IDENTIFIED BY ‘new_password’;

CREATE USER ‘jeffrey’@’localhost’ IDENTIFIED BY ‘mypass’;

CREATE USER ‘ashwath’@‘localhost’ IDENTIFIED BY ‘newpass’;

CREATE USER ‘admin’@’localhost’ IDENTIFIED BY ‘admin123′;

CREATE USER ‘cacti’@‘localhost’ IDENTIFIED BY ‘cacti’;

To provide full access to all database:( user will get here permsission similar to root)

GRANT ALL ON *.* TO ‘ashwath’@‘localhost’; (Here *.* is any_database.any_table)
```
 

## To List users:
```shell
SELECT User FROM mysql.user;

select User,Host from mysql.user;

create database [databasename];

show database;
```

## To Provide permission only to particular database:

Syntax: GRANT [type of permission] ON [database name].[table name] TO ‘[username]’@’localhost’;
```shell
GRANT ALL ON test.* TO ‘ashwath’@‘localhost’;
```
 

## To remove permission,

```shell
REVOKE ALL PRIVILEGES on *.* FROM ‘admin’@’localhost’;
```

 

## To check some of the variables on Mysql:

`SHOW VARIABLES WHERE Variable_name = ‘hostname’;`

OR

`SHOW VARIABLES like ‘hostname’;`

to check Mysql version

```shell
show variables like ‘version’;
SHOW VARIABLES LIKE ‘max_allowed_packet’;
```
 (it will show current value )

To set
```shell
SET GLOBAL max_allowed_packet=16777216; (16MB) its in 16777216kb
```
 

Allow the user “bob” to connect to the server from localhost (localhost or ip from which he is accessing) using the password “passwd”. Login as root. Switch to the MySQL db. Give privs. Update privs.
```shell
# mysql -u root -p
mysql> use mysql;
mysql> grant usage on *.* to bob@localhost identified by ‘passwd’;
mysql> flush privileges;
```
—————————————Backup-Restore————————————-

To Backup
```shell
mysqldump -uroot -p database_name > database_name.sql
To Restore:
mysql -uroot -p database_name < database_name.sql
```
——————————End——————————–

——————————–Database creation——————————–
```shell
mysql> Create database Test;

mysql>drop database Test;

create table(authors) into Test database using below command

mysql> CREATE TABLE authors (id INT, name VARCHAR(20), email VARCHAR(20));

mysql> show tables;

Insert data into tables using below command:

mysql> INSERT INTO authors (id,name,email) VALUES(1,”Vivek”,”xuz@abc.com”);

To check contents of table authors:

mysql> SELECT * FROM authors;
```

—————————————————————

To Drop table;


```shell
mysql> drop table authors;

To Backup(Export) tables;

mysqldump my_database authors > /tmp/authors.sql
To Restore tables:

mysql my_database < /tmp/authors.sql
OR
mysql> use my_database;

mysql> source /tmp/testnow.sql;
```
—————————————————————

To Replicate mysql db from one db to another;

Existing db = mydb; wants to copy db to mydbbackup;

First Create db “mydbbackup” and then run below syntax  to achieve;
```shell
mysql> Create database mydbbackup;

mysqldump -uroot -pPASSWD mydb | mysql mydbbackup -uroot -pPASSWD
```
—————————————————————

Starting MYSQL in recovery mode:

cat /etc/my.cnf
```shell
add the below line
innodb_force_recovery = 1
```

and start mysql
—————————————————————

