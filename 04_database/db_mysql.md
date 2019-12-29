
# 玩转MySQL

## 管理类

更改root的默认密码：

	1. open CMD
	2. SET PASSWORD FOR 'root'@'localhost' = PASSWORD('root');
	3. stop mysql process

## 导入和导出

登录MySQL：

	mysql -u root -p
	Welcome to the MySQL monitor.  Commands end with ; or \g.
	Your MySQL connection id is 1
	Server version: 5.6.32 MySQL Community Server (GPL)
	Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

	mysql> show databases;
	+--------------------+
	| Database           |
	+--------------------+
	| information_schema |
	| mysql              |
	| performance_schema |
	| test               |
	+--------------------+
	4 rows in set (0.00 sec)

	mysql>
	mysql> source d:\sakila-db\sakila-schema.sql
	mysql> source d:\sakila-db\sakila-data.sql
    mysql>
