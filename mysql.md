# mysql

## 在Mac环境使用homebrew安装mysql

* **安装mysql**

```mysql
$ brew install mysql

==> Downloading https://homebrew.bintray.com/bottles/mysql-5.7.21.high_sierra.bottle.tar.gz
Already downloaded: /Users/Jimmy/Library/Caches/Homebrew/mysql-5.7.21.high_sierra.bottle.tar.gz
==> Pouring mysql-5.7.21.high_sierra.bottle.tar.gz
==> Caveats
We've installed your MySQL database without a root password. To secure it run:
    mysql_secure_installation

MySQL is configured to only allow connections from localhost by default

To connect run:
    mysql -uroot

To have launchd start mysql now and restart at login:
  brew services start mysql
Or, if you don't want/need a background service you can just run:
  mysql.server start
==> Summary
🍺  /usr/local/Cellar/mysql/5.7.21: 323 files, 233.9MB
```

* **启动mysql服务**

```mysql
$ mysql.server start

Starting MySQL
  SUCCESS! 
```

* **mysql安装基本配置**

```mysql
$ mysql_secure_installation

Securing the MySQL server deployment.

Connecting to MySQL using a blank password.

VALIDATE PASSWORD PLUGIN can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD plugin?
// 提示是否设置密码
Press y|Y for Yes, any other key for No: y
// 提示选择密码强度等级
There are three levels of password validation policy:

LOW    Length >= 8
MEDIUM Length >= 8, numeric, mixed case, and special characters
STRONG Length >= 8, numeric, mixed case, special characters and dictionary                  file

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 1
Please set the password for root here.
// 按照所选的密码强度要求设定密码
New password: 

Re-enter new password: 

// 提示密码强度50,不符合要求重新设置密码
Estimated strength of the password: 50 
Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : y
 ... Failed! Error: Your password does not satisfy the current policy requirements

New password: 

Re-enter new password: 
// 提示密码强度100,符合要求继续进行
Estimated strength of the password: 100 
Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : y
By default, a MySQL installation has an anonymous user,
allowing anyone to log into MySQL without having to have
a user account created for them. This is intended only for
testing, and to make the installation go a bit smoother.
You should remove them before moving into a production
environment.
// 提示删除默认无密码用户
Remove anonymous users? (Press y|Y for Yes, any other key for No) : y
Success.


Normally, root should only be allowed to connect from
'localhost'. This ensures that someone cannot guess at
the root password from the network.
// 提示禁止远程root登录
Disallow root login remotely? (Press y|Y for Yes, any other key for No) : no

 ... skipping.
By default, MySQL comes with a database named 'test' that
anyone can access. This is also intended only for testing,
and should be removed before moving into a production
environment.

// 提示删除默认自带的test数据库
Remove test database and access to it? (Press y|Y for Yes, any other key for No) : y
 - Dropping test database...
Success.

 - Removing privileges on test database...
Success.

Reloading the privilege tables will ensure that all changes
made so far will take effect immediately.
// 提示是否重新加载privilege tables
Reload privilege tables now? (Press y|Y for Yes, any other key for No) : y
Success.

All done! 
```

* **测试登陆mysql**

``` mysql
$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 4
Server version: 5.7.25 Homebrew

Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 
```



* **退出mysql**

``` mysql
mysql> quit
Bye
```

* **查看MySQL提供的所有存储引擎**

``` mysql
mysql> show engines;
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
| Engine             | Support | Comment                                                        | Transactions | XA   | Savepoints |
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
| InnoDB             | DEFAULT | Supports transactions, row-level locking, and foreign keys     | YES          | YES  | YES        |
| MRG_MYISAM         | YES     | Collection of identical MyISAM tables                          | NO           | NO   | NO         |
| MEMORY             | YES     | Hash based, stored in memory, useful for temporary tables      | NO           | NO   | NO         |
| BLACKHOLE          | YES     | /dev/null storage engine (anything you write to it disappears) | NO           | NO   | NO         |
| MyISAM             | YES     | MyISAM storage engine                                          | NO           | NO   | NO         |
| CSV                | YES     | CSV storage engine                                             | NO           | NO   | NO         |
| ARCHIVE            | YES     | Archive storage engine                                         | NO           | NO   | NO         |
| PERFORMANCE_SCHEMA | YES     | Performance Schema                                             | NO           | NO   | NO         |
| FEDERATED          | NO      | Federated MySQL storage engine                                 | NULL         | NULL | NULL       |
+--------------------+---------+----------------------------------------------------------------+--------------+------+------------+
9 rows in set (0.00 sec)
```

## mysql常用命令

* 查看数据库

```mysql
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| RUNOOB             |
| java               |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
7 rows in set (0.07 sec)
```



* 创建数据库并导入数据

```mysql
mysql> CREATE DATABASE IF NOT EXISTS yiibaidb DEFAULT CHARSET utf8 COLLATE utf8_general_ci;

mysql> use yiibaidb;

mysql> source /Users/lilei/Desktop/yiibaidb.sql;
```

* 测试导入结果

```mysql
mysql> use yiibaidb;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> select city,phone,country from `offices`;
+---------------+------------------+-----------+
| city          | phone            | country   |
+---------------+------------------+-----------+
| San Francisco | +1 650 219 4782  | USA       |
| Boston        | +1 215 837 0825  | USA       |
| NYC           | +1 212 555 3000  | USA       |
| Paris         | +33 14 723 4404  | France    |
| Beijing       | +86 33 224 5000  | China     |
| Sydney        | +61 2 9264 2451  | Australia |
| London        | +44 20 7877 2041 | UK        |
+---------------+------------------+-----------+
7 rows in set (0.03 sec)
```



### ### select 查询语句

```mysql
SELECT 
    column_1, column_2, ...
FROM
    table_1
[INNER | LEFT |RIGHT] JOIN table_2 ON conditions
WHERE
    conditions
GROUP BY column_1
HAVING group_conditions
ORDER BY column_1
LIMIT offset, length;
```

`SELECT`语句由以下列表中所述的几个子句组成：

- `SELECT`之后是逗号分隔列或星号(`*`)的列表，表示要返回所有列。
- `FROM`指定要查询数据的表或视图。
- `JOIN`根据某些连接条件从其他表中获取数据。
- `WHERE`过滤结果集中的行。
- `GROUP BY`将一组行组合成小分组，并对每个小分组应用聚合函数。
- `HAVING`过滤器基于`GROUP BY`子句定义的小分组。
- `ORDER BY`指定用于排序的列的列表。
- `LIMIT`限制返回行的数量。

语句中的`SELECT`和`FROM`语句是必须的，其他部分是可选的。

```mysql
mysql> SELECT lastname, firstname, jobtitle FROM employees;
+-----------+-----------+----------------------+
| lastname  | firstname | jobtitle             |
+-----------+-----------+----------------------+
| Murphy    | Diane     | President            |
| Patterson | Mary      | VP Sales             |
| Firrelli  | Jeff      | VP Marketing         |
| Patterson | William   | Sales Manager (APAC) |
| Bondur    | Gerard    | Sale Manager (EMEA)  |
| Bow       | Anthony   | Sales Manager (NA)   |
| Jennings  | Leslie    | Sales Rep            |
| Thompson  | Leslie    | Sales Rep            |
| Firrelli  | Julie     | Sales Rep            |
| Patterson | Steve     | Sales Rep            |
| Tseng     | Foon Yue  | Sales Rep            |
| Vanauf    | George    | Sales Rep            |
| Bondur    | Loui      | Sales Rep            |
| Hernandez | Gerard    | Sales Rep            |
| Castillo  | Pamela    | Sales Rep            |
| Bott      | Larry     | Sales Rep            |
| Jones     | Barry     | Sales Rep            |
| Fixter    | Andy      | Sales Rep            |
| Marsh     | Peter     | Sales Rep            |
| King      | Tom       | Sales Rep            |
| Nishi     | Mami      | Sales Rep            |
| Kato      | Yoshimi   | Sales Rep            |
| Gerard    | Martin    | Sales Rep            |
+-----------+-----------+----------------------+
23 rows in set (0.01 sec)
```

```mysql
mysql> SELECT * FROM employees;
+----------------+-----------+-----------+-----------+-----------------------+------------+-----------+----------------------+
| employeeNumber | lastName  | firstName | extension | email                 | officeCode | reportsTo | jobTitle             |
+----------------+-----------+-----------+-----------+-----------------------+------------+-----------+----------------------+
|           1002 | Murphy    | Diane     | x5800     | dmurphy@yiibai.com    | 1          |      NULL | President            |
|           1056 | Patterson | Mary      | x4611     | mpatterso@yiibai.com  | 1          |      1002 | VP Sales             |
|           1076 | Firrelli  | Jeff      | x9273     | jfirrelli@yiibai.com  | 1          |      1002 | VP Marketing         |
|           1088 | Patterson | William   | x4871     | wpatterson@yiibai.com | 6          |      1056 | Sales Manager (APAC) |
|           1102 | Bondur    | Gerard    | x5408     | gbondur@gmail.com     | 4          |      1056 | Sale Manager (EMEA)  |
|           1143 | Bow       | Anthony   | x5428     | abow@gmail.com        | 1          |      1056 | Sales Manager (NA)   |
|           1165 | Jennings  | Leslie    | x3291     | ljennings@yiibai.com  | 1          |      1143 | Sales Rep            |
|           1166 | Thompson  | Leslie    | x4065     | lthompson@yiibai.com  | 1          |      1143 | Sales Rep            |
|           1188 | Firrelli  | Julie     | x2173     | jfirrelli@yiibai.com  | 2          |      1143 | Sales Rep            |
|           1216 | Patterson | Steve     | x4334     | spatterson@yiibai.com | 2          |      1143 | Sales Rep            |
|           1286 | Tseng     | Foon Yue  | x2248     | ftseng@yiibai.com     | 3          |      1143 | Sales Rep            |
|           1323 | Vanauf    | George    | x4102     | gvanauf@yiibai.com    | 3          |      1143 | Sales Rep            |
|           1337 | Bondur    | Loui      | x6493     | lbondur@yiibai.com    | 4          |      1102 | Sales Rep            |
|           1370 | Hernandez | Gerard    | x2028     | ghernande@gmail.com   | 4          |      1102 | Sales Rep            |
|           1401 | Castillo  | Pamela    | x2759     | pcastillo@gmail.com   | 4          |      1102 | Sales Rep            |
|           1501 | Bott      | Larry     | x2311     | lbott@yiibai.com      | 7          |      1102 | Sales Rep            |
|           1504 | Jones     | Barry     | x102      | bjones@gmail.com      | 7          |      1102 | Sales Rep            |
|           1611 | Fixter    | Andy      | x101      | afixter@yiibai.com    | 6          |      1088 | Sales Rep            |
|           1612 | Marsh     | Peter     | x102      | pmarsh@yiibai.com     | 6          |      1088 | Sales Rep            |
|           1619 | King      | Tom       | x103      | tking@gmail.com       | 6          |      1088 | Sales Rep            |
|           1621 | Nishi     | Mami      | x101      | mnishi@gmail.com      | 5          |      1056 | Sales Rep            |
|           1625 | Kato      | Yoshimi   | x102      | ykato@gmail.com       | 5          |      1621 | Sales Rep            |
|           1702 | Gerard    | Martin    | x2312     | mgerard@gmail.com     | 4          |      1102 | Sales Rep            |
+----------------+-----------+-----------+-----------+-----------------------+------------+-----------+----------------------+
23 rows in set (0.01 sec)
```



建议显式获取数据的列，原因如下：

- 使用星号(`*`)可能会返回不使用的列的数据。 它在MySQL数据库服务器和应用程序之间产生不必要的*I/O*磁盘和网络流量。
- 如果明确指定列，则结果集更可预测并且更易于管理。 想象一下，当您使用星号(`*`)并且有人通过添加更多列来更改表格数据时，将会得到一个与预期不同的结果集。
- 使用星号(`*`)可能会将敏感信息暴露给未经授权的用户。

