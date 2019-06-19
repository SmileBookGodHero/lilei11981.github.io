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
| yiibaidb           |
+--------------------+
7 rows in set (0.03 sec)
```

* 查看库中的表格

```mysql
mysql> use yiibaidb;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> show tables;
+--------------------+
| Tables_in_yiibaidb |
+--------------------+
| customers          |
| customers_bak      |
| employees          |
| items              |
| offices            |
| orderdetails       |
| orders             |
| payments           |
| productlines       |
| products           |
| tasks              |
| tasks_bak          |
| tokens             |
+--------------------+
13 rows in set (0.00 sec)
```

* 查看表结构

```mysql
mysql> describe products;
mysql> show columns from products;
mysql> show create table products;
mysql> desc products;
+--------------------+---------------+------+-----+---------+-------+
| Field              | Type          | Null | Key | Default | Extra |
+--------------------+---------------+------+-----+---------+-------+
| productCode        | varchar(15)   | NO   | PRI |         |       |
| productName        | varchar(70)   | NO   |     | NULL    |       |
| productLine        | varchar(50)   | NO   | MUL | NULL    |       |
| productScale       | varchar(10)   | NO   |     | NULL    |       |
| productVendor      | varchar(50)   | NO   |     | NULL    |       |
| productDescription | text          | NO   |     | NULL    |       |
| quantityInStock    | smallint(6)   | NO   |     | NULL    |       |
| buyPrice           | decimal(10,2) | NO   |     | NULL    |       |
| MSRP               | decimal(10,2) | NO   |     | NULL    |       |
+--------------------+---------------+------+-----+---------+-------+
9 rows in set (0.03 sec)
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



### 查询语句

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

### select 语句

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

### where 语句

* 想从`employees`表中获取销售代表员工

```mysql
mysql> SELECT lastname, firstname, jobtitle FROM employees WHERE jobtitle = 'Sales Rep';
+-----------+-----------+-----------+
| lastname  | firstname | jobtitle  |
+-----------+-----------+-----------+
| Jennings  | Leslie    | Sales Rep |
| Thompson  | Leslie    | Sales Rep |
| Firrelli  | Julie     | Sales Rep |
| Patterson | Steve     | Sales Rep |
| Tseng     | Foon Yue  | Sales Rep |
| Vanauf    | George    | Sales Rep |
| Bondur    | Loui      | Sales Rep |
| Hernandez | Gerard    | Sales Rep |
| Castillo  | Pamela    | Sales Rep |
| Bott      | Larry     | Sales Rep |
| Jones     | Barry     | Sales Rep |
| Fixter    | Andy      | Sales Rep |
| Marsh     | Peter     | Sales Rep |
| King      | Tom       | Sales Rep |
| Nishi     | Mami      | Sales Rep |
| Kato      | Yoshimi   | Sales Rep |
| Gerard    | Martin    | Sales Rep |
+-----------+-----------+-----------+
17 rows in set (0.03 sec)
```

* 将多个表达式与逻辑运算符(如AND，OR等)组合在一起的一个非常复杂的例子，要在办公室代码(`officeCode`)等于`1`中查找所有销售代表

```mysql
mysql> SELECT lastname, firstname, jobtitle FROM employees WHERE jobtitle = 'Sales Rep' AND officeCode = 1;
+----------+-----------+-----------+
| lastname | firstname | jobtitle  |
+----------+-----------+-----------+
| Jennings | Leslie    | Sales Rep |
| Thompson | Leslie    | Sales Rep |
+----------+-----------+-----------+
2 rows in set (0.02 sec)
```

* 可用于在`WHERE`子句中形成过滤表达式的比较运算符

| 操作符       | 描述                                          |
| ------------ | --------------------------------------------- |
| `=`          | 等于，几乎任何数据类型都可以使用它。          |
| `<>` 或 `!=` | 不等于                                        |
| `<=`         | 小于或等于，通常使用数字和日期/时间数据类型。 |
| `>=`         | 小于或等于，通常使用数字和日期/时间数据类型。 |

* 使用不等于(`!=`)运算符来获取不是销售代表的其它所有员工

```mysql
mysql> SELECT lastname, firstname, jobtitle FROM employees WHERE jobtitle <> 'Sales Rep';
+-----------+-----------+----------------------+
| lastname  | firstname | jobtitle             |
+-----------+-----------+----------------------+
| Murphy    | Diane     | President            |
| Patterson | Mary      | VP Sales             |
| Firrelli  | Jeff      | VP Marketing         |
| Patterson | William   | Sales Manager (APAC) |
| Bondur    | Gerard    | Sale Manager (EMEA)  |
| Bow       | Anthony   | Sales Manager (NA)   |
+-----------+-----------+----------------------+
6 rows in set (0.00 sec)
```

* 查询办公室代码大于`5`的每位员工

```mysql
mysql> SELECT lastname, firstname, officeCode FROM employees WHERE officecode > 5;
+-----------+-----------+------------+
| lastname  | firstname | officeCode |
+-----------+-----------+------------+
| Patterson | William   | 6          |
| Bott      | Larry     | 7          |
| Jones     | Barry     | 7          |
| Fixter    | Andy      | 6          |
| Marsh     | Peter     | 6          |
| King      | Tom       | 6          |
+-----------+-----------+------------+
6 rows in set (0.00 sec)
```

### between 语句

* 查找价格在`90`和`100`(含`90`和`100`)元范围内的商品，也可以通过使用大于或等于(`>=`)和小于或等于(`<=`)运算符来实现相同的结果

```mysql
mysql> SELECT productCode,productName,buyPrice FROM products WHERE buyPrice BETWEEN 90 AND 100;
mysql> SELECT productCode,productName,buyPrice FROM products WHERE buyPrice>=90 AND buyPrice<=100;
+-------------+--------------------------------------+----------+
| productCode | productName                          | buyPrice |
+-------------+--------------------------------------+----------+
| S10_1949    | 1952 Alpine Renault 1300             |    98.58 |
| S10_4698    | 2003 Harley-Davidson Eagle Drag Bike |    91.02 |
| S12_1099    | 1968 Ford Mustang                    |    95.34 |
| S12_1108    | 2001 Ferrari Enzo                    |    95.59 |
| S18_1984    | 1995 Honda Civic                     |    93.89 |
| S18_4027    | 1970 Triumph Spitfire                |    91.92 |
| S24_3856    | 1956 Porsche 356A Coupe              |    98.30 |
+-------------+--------------------------------------+----------+
7 rows in set (0.00 sec)
```

* 查找购买价格不在`20`到`100`(含`20`到`100`)之间的产品

```mysql
mysql> SELECT productCode,productName,buyPrice FROM products WHERE buyPrice NOT BETWEEN 20 AND 100;
mysql> SELECT productCode,productName,buyPrice FROM products WHERE buyPrice< 20 OR buyPrice> 100;
+-------------+-------------------------------------+----------+
| productCode | productName                         | buyPrice |
+-------------+-------------------------------------+----------+
| S10_4962    | 1962 LanciaA Delta 16V              |   103.42 |
| S18_2238    | 1998 Chrysler Plymouth Prowler      |   101.51 |
| S24_2840    | 1958 Chevy Corvette Limited Edition |    15.91 |
| S24_2972    | 1982 Lamborghini Diablo             |    16.24 |
+-------------+-------------------------------------+----------+
4 rows in set (0.00 sec)
```


* 当使用`BETWEEN`运算符与日期类型值时，要获得最佳结果，应该使用类型转换将列或表达式的类型显式转换为DATE类型，要查询获取所需日期(`requiredDate`)从`2013-01-01`到`2013-01-31`的所有订单，请使用以下查询

```mysql
mysql> SELECT orderNumber,requiredDate,STATUS FROM orders WHERE requireddate BETWEEN CAST('2013-01-01' AS DATE) AND CAST('2013-01-31' AS DATE);
+-------------+--------------+---------+
| orderNumber | requiredDate | STATUS  |
+-------------+--------------+---------+
|       10100 | 2013-01-13   | Shipped |
|       10101 | 2013-01-18   | Shipped |
|       10102 | 2013-01-18   | Shipped |
+-------------+--------------+---------+
3 rows in set (0.00 sec)
```

### like 语句

* `LIKE`操作符通常用于基于模式查询选择数据。以正确的方式使用`LIKE`运算符对于增加/减少查询性能至关重要。MySQL提供两个通配符，用于与`LIKE`运算符一起使用，它们分别是：百分比符号 - `%`和下划线 - `_`。
    - 百分比(`%`)通配符允许匹配任何字符串的零个或多个字符。
    - 下划线(`_`)通配符允许匹配任何单个字符。

* 搜索名字以字符`a`开头的员工信息，可以在模式末尾使用百分比通配符(`％`)

```mysql
mysql> SELECT employeeNumber,lastName,firstName FROM employees WHERE firstName LIKE 'a%';
+----------------+----------+-----------+
| employeeNumber | lastName | firstName |
+----------------+----------+-----------+
|           1143 | Bow      | Anthony   |
|           1611 | Fixter   | Andy      |
+----------------+----------+-----------+
2 rows in set (0.00 sec)
```

* 搜索员工以`on`字符结尾的姓氏，可以使用模式开头的`％`通配符

```mysql
mysql> SELECT employeeNumber,lastName,firstName FROM employees WHERE lastName LIKE '%on';
+----------------+-----------+-----------+
| employeeNumber | lastName  | firstName |
+----------------+-----------+-----------+
|           1056 | Patterson | Mary      |
|           1088 | Patterson | William   |
|           1166 | Thompson  | Leslie    |
|           1216 | Patterson | Steve     |
+----------------+-----------+-----------+
4 rows in set (0.00 sec)
```

* 查找 `lastname` 字段值中包含`on`字符串的所有员工，可使用带有`%on%`条件

```mysql
mysql> SELECT employeeNumber,lastName,firstName FROM employees WHERE lastname LIKE '%on%';
+----------------+-----------+-----------+
| employeeNumber | lastName  | firstName |
+----------------+-----------+-----------+
|           1056 | Patterson | Mary      |
|           1088 | Patterson | William   |
|           1102 | Bondur    | Gerard    |
|           1166 | Thompson  | Leslie    |
|           1216 | Patterson | Steve     |
|           1337 | Bondur    | Loui      |
|           1504 | Jones     | Barry     |
+----------------+-----------+-----------+
7 rows in set (0.00 sec)
```

* 要查找名字以`T`开头的员工，以`m`结尾，并且包含例如`Tom`，`Tim`之间的任何单个字符，可以使用下划线通配符来构建模式

```mysql
mysql> SELECT employeeNumber,lastName,firstName FROM employees WHERE firstname LIKE 'T_m';
+----------------+----------+-----------+
| employeeNumber | lastName | firstName |
+----------------+----------+-----------+
|           1619 | King     | Tom       |
+----------------+----------+-----------+
1 row in set (0.00 sec)
```

* 搜索姓氏(`lastname`)不以字符`B`开头的员工，则可以使用`NOT LIKE`作为以下查询

```mysql
mysql> SELECT employeeNumber,lastName,firstName FROM employees WHERE lastName NOT LIKE 'B%';
+----------------+-----------+-----------+
| employeeNumber | lastName  | firstName |
+----------------+-----------+-----------+
|           1002 | Murphy    | Diane     |
|           1056 | Patterson | Mary      |
|           1076 | Firrelli  | Jeff      |
|           1088 | Patterson | William   |
|           1165 | Jennings  | Leslie    |
|           1166 | Thompson  | Leslie    |
|           1188 | Firrelli  | Julie     |
|           1216 | Patterson | Steve     |
|           1286 | Tseng     | Foon Yue  |
|           1323 | Vanauf    | George    |
|           1370 | Hernandez | Gerard    |
|           1401 | Castillo  | Pamela    |
|           1504 | Jones     | Barry     |
|           1611 | Fixter    | Andy      |
|           1612 | Marsh     | Peter     |
|           1619 | King      | Tom       |
|           1621 | Nishi     | Mami      |
|           1625 | Kato      | Yoshimi   |
|           1702 | Gerard    | Martin    |
+----------------+-----------+-----------+
19 rows in set (0.00 sec)
```

* 查询`productCode`字段中包含`_20`字符串的值

```mysql
mysql> SELECT productCode,productName FROM products WHERE productCode LIKE '%\_20%';
+-------------+-------------------------------------------+
| productCode | productName                               |
+-------------+-------------------------------------------+
| S10_2016    | 1996 Moto Guzzi 1100i                     |
| S24_2000    | 1960 BSA Gold Star DBD34                  |
| S24_2011    | 18th century schooner                     |
| S24_2022    | 1938 Cadillac V-16 Presidential Limousine |
| S700_2047   | HMS Bounty                                |
+-------------+-------------------------------------------+
5 rows in set (0.00 sec)
```

* 模式`%$_20%`匹配任何包含`_20`字符串的字符串

```mysql
mysql> SELECT productCode,productName FROM products WHERE productCode LIKE '%$_20%' ESCAPE '$';
+-------------+-------------------------------------------+
| productCode | productName                               |
+-------------+-------------------------------------------+
| S10_2016    | 1996 Moto Guzzi 1100i                     |
| S24_2000    | 1960 BSA Gold Star DBD34                  |
| S24_2011    | 18th century schooner                     |
| S24_2022    | 1938 Cadillac V-16 Presidential Limousine |
| S700_2047   | HMS Bounty                                |
+-------------+-------------------------------------------+
5 rows in set (0.00 sec)
```

> `LIKE`操作符强制MySQL扫描整个表以找到匹配的行记录，因此，它不允许数据库引擎使用索引进行快速搜索。因此，当要从具有大量行的表查询数据时，使用`LIKE`运算符来查询数据的性能会大幅降低。



### in 语句

* `IN`运算符来确定指定列的值是否匹配列表中的值或子查询中的任何值。

```
SELECT 
    column1,column2,...
FROM
    table_name
WHERE 
 (expr|column_1) IN ('value1','value2',...);
```



> 可以在WHERE子句中与`IN`运算符一起使用，可使用列或表达式(`expr`)。
>
> 列表中的值必须用逗号(`，`)分隔。
>
> `IN`操作符也可以用在其他语句(如INSERT、UPDATE、DELETE等)的WHERE子句中。
> 



* 如果`column_1`的值或`expr`表达式的结果等于列表中的任何值，则`IN`运算符返回`1`，否则返回`0`。



> 当列表中的值都是常量时：
>
> - 首先，MySQL根据`column_1`的类型或`expr`表达式的结果来计算值。
> - 第二步，MySQL排序值。
> - 第三步，MySQL使用二进制搜索算法搜索值。因此，使用具有常量列表的`IN`运算符的查询将执行得非常快。
>
> > 请注意，如果列表中的`expr`或任何值为`NULL`，则`IN`运算符计算结果返回`NULL`。
>
> 可以将`IN`运算符与`NOT`运算符组合，以确定值是否与列表或子查询中的任何值不匹配。



* 查找位于美国和法国的办事处，可以使用`IN`运算符作为以下查询



```mysql
mysql> SELECT officeCode, city, phone, country FROM offices WHERE country IN ('USA' , 'France');
+------------+---------------+-----------------+---------+
| officeCode | city          | phone           | country |
+------------+---------------+-----------------+---------+
| 1          | San Francisco | +1 650 219 4782 | USA     |
| 2          | Boston        | +1 215 837 0825 | USA     |
| 3          | NYC           | +1 212 555 3000 | USA     |
| 4          | Paris         | +33 14 723 4404 | France  |
+------------+---------------+-----------------+---------+
4 rows in set (0.01 sec)
```

* 也可以使用`OR`运算符执行得到与上面查询相同的结果



```mysql
mysql> SELECT officeCode, city, phone FROM offices WHERE country = 'USA' OR country = 'France';
+------------+---------------+-----------------+
| officeCode | city          | phone           |
+------------+---------------+-----------------+
| 1          | San Francisco | +1 650 219 4782 |
| 2          | Boston        | +1 215 837 0825 |
| 3          | NYC           | +1 212 555 3000 |
| 4          | Paris         | +33 14 723 4404 |
+------------+---------------+-----------------+
4 rows in set (0.00 sec)
```



> 如果列表中有很多值，使用多个`OR`运算符则会构造一个非常长的语句。 因此，使用`IN`运算符则会缩短查询并使查询更易读。



* 要获得不在美国和法国的办事处，请在`WHERE`子句中使用`NOT IN`

``` mysql
mysql> SELECT officeCode, city, phone FROM offices WHERE country NOT IN( 'USA', 'France');
+------------+---------+------------------+
| officeCode | city    | phone            |
+------------+---------+------------------+
| 5          | Beijing | +86 33 224 5000  |
| 6          | Sydney  | +61 2 9264 2451  |
| 7          | London  | +44 20 7877 2041 |
+------------+---------+------------------+
3 rows in set (0.00 sec)
```



* 查找总金额大于`60000`的订单，则使用`IN`运算符查询如下所示

```mysql
mysql> SELECT orderNumber,customerNumber,STATUS,shippedDate FROM orders WHERE orderNumber IN (SELECT orderNumber FROM orderDetails GROUP BY orderNumber HAVING SUM(quantityOrdered*priceEach)> 60000);
+-------------+----------------+---------+-------------+
| orderNumber | customerNumber | STATUS  | shippedDate |
+-------------+----------------+---------+-------------+
|       10165 |            148 | Shipped | 2013-12-26  |
|       10287 |            298 | Shipped | 2014-09-01  |
|       10310 |            259 | Shipped | 2014-10-18  |
+-------------+----------------+---------+-------------+
3 rows in set (0.00 sec)
```



### group by 语句

* `GROUP BY`子句通过列或表达式的值将一组行分组为一个小分组的汇总行记录。 `GROUP BY`子句为每个分组返回一行。换句话说，它减少了结果集中的行数。

> `GROUP BY`子句必须出现在`FROM`和`WHERE`子句之后。 在`GROUP BY`关键字之后是一个以逗号分隔的列或表达式的列表，这些是要用作为条件来对行进行分组。
>
> 经常使用GROUP BY子句与聚合函数一起使用，如SUM，AVG，MAX，MIN和COUNT。SELECT子句中使用聚合函数来计算有关每个分组的信息



```mysql
SELECT 
    c1, c2,..., cn, aggregate_function(ci)
FROM
    table
WHERE
    where_conditions
GROUP BY c1 , c2,...,cn;
```



* 要将订单状态的值分组到子组中，则要使用`GROUP BY`子句并指定按`status`列来执行分组



```mysql
mysql> SELECT STATUS FROM orders GROUP BY STATUS;
+------------+
| STATUS     |
+------------+
| Cancelled  |
| Disputed   |
| In Process |
| On Hold    |
| Resolved   |
| Shipped    |
+------------+
6 rows in set (0.00 sec)
```



* `GROUP BY`子句返回状态(`status`)值是唯一的，它像`DISTINCT`运算符一样工作，`GROUP BY`按字母表顺序排序，`DISTINCT`不排序



```mysql
mysql> SELECT DISTINCT STATUS FROM orders;
+------------+
| STATUS     |
+------------+
| Shipped    |
| Resolved   |
| Cancelled  |
| On Hold    |
| Disputed   |
| In Process |
+------------+
6 rows in set (0.00 sec)
```



> 可使用聚合函数来执行一组行的计算并返回单个值。`GROUP BY`子句通常与聚合函数一起使用以执行计算每个分组并返回单个值。



* 如果想知道每个状态中的订单数，可以使用`COUNT`函数与`GROUP BY`子句查询语句



```mysql
mysql> SELECT STATUS,COUNT(*) AS total_number FROM orders GROUP BY STATUS;
+------------+--------------+
| STATUS     | total_number |
+------------+--------------+
| Cancelled  |            6 |
| Disputed   |            3 |
| In Process |            6 |
| On Hold    |            4 |
| Resolved   |            4 |
| Shipped    |          303 |
+------------+--------------+
6 rows in set (0.00 sec)
```



* 要按状态获取所有订单的总金额，可以使用`orderdetails`表连接`orders`表，并使用`SUM`函数计算总金额

```mysql
mysql> SELECT STATUS,SUM(quantityOrdered*priceEach) AS amount FROM orders INNER JOIN orderdetails USING (orderNumber) GROUP BY STATUS;
+------------+------------+
| STATUS     | amount     |
+------------+------------+
| Cancelled  |  238854.18 |
| Disputed   |   61158.78 |
| In Process |  135271.52 |
| On Hold    |  169575.61 |
| Resolved   |  134235.88 |
| Shipped    | 8865094.64 |
+------------+------------+
6 rows in set (0.01 sec)
```



* 按表达式对行进行分组，获取每年的总销售额

```mysql
mysql> SELECT YEAR (orderDate) AS YEAR,SUM(quantityOrdered*priceEach) AS total FROM orders INNER JOIN orderdetails USING (orderNumber) WHERE STATUS='Shipped' GROUP BY YEAR (orderDate);
+------+------------+
| YEAR | total      |
+------+------------+
| 2013 | 3223095.80 |
| 2014 | 4300602.99 |
| 2015 | 1341395.85 |
+------+------------+
3 rows in set (0.01 sec)
```

> 在`GROUP BY`子句中使用`DESC`以降序对状态进行排序。我们还可以在`GROUP BY`子句中明确指定`ASC`，按状态对分组进行升序排序

```mysql
mysql> SELECT STATUS,COUNT(*) FROM orders GROUP BY STATUS DESC;
+------------+----------+
| STATUS     | COUNT(*) |
+------------+----------+
| Shipped    |      303 |
| Resolved   |        4 |
| On Hold    |        4 |
| In Process |        6 |
| Disputed   |        3 |
| Cancelled  |        6 |
+------------+----------+
6 rows in set, 1 warning (0.00 sec)
```

### having 语句

* 可使用HAVING子句过滤`GROUP BY`子句返回的分组。以下查询使用`HAVING`子句来选择`2013`年以后的年销售总额

```mysql
mysql> SELECT YEAR (orderDate) AS YEAR,SUM(quantityOrdered*priceEach) AS total FROM orders INNER JOIN orderdetails USING (orderNumber) WHERE STATUS='Shipped' GROUP BY YEAR HAVING YEAR> 2013;
+------+------------+
| YEAR | total      |
+------+------------+
| 2014 | 4300602.99 |
| 2015 | 1341395.85 |
+------+------------+
2 rows in set (0.01 sec)
```




### create 语句

* 创建一个名为`tasks`的新表

```mysql
mysql> CREATE TABLE IF NOT EXISTS tasks (task_id INT (11) AUTO_INCREMENT,SUBJECT VARCHAR (45) DEFAULT NULL,start_date DATE DEFAULT NULL,end_date DATE DEFAULT NULL,description VARCHAR (200) DEFAULT NULL,PRIMARY KEY (task_id)) ENGINE=INNODB DEFAULT CHARSET=utf8;
Query OK, 0 rows affected (0.02 sec)
```

* 显示表格

```mysql
mysql> show tables;                                                                                                                                +--------------------+
| Tables_in_yiibaidb |
+--------------------+
| customers          |
| customers_bak      |
| employees          |
| items              |
| offices            |
| orderdetails       |
| orders             |
| payments           |
| productlines       |
| products           |
| tasks              |
| tokens             |
+--------------------+
12 rows in set (0.00 sec)
```

* 删除表格

```mysql
mysql> drop table if exists tasks;
Query OK, 0 rows affected (0.02 sec)
```

### insert 语句

> `INSERT`语句允许您将一行或多行插入到表中



```mysql
INSERT INTO table(column1,column2...)
VALUES (value1,value2,...);
```



* 把数据插入数据库

```mysql
mysql> INSERT INTO tasks (SUBJECT,start_date,end_date,description) VALUES ('Learn MySQL INSERT','2017-07-21','2017-07-22','Start learning..');
Query OK, 1 row affected (0.01 sec)
```

* 查看数据

```mysql
mysql> SELECT * FROM tasks;
+---------+--------------------+------------+------------+------------------+
| task_id | SUBJECT            | start_date | end_date   | description      |
+---------+--------------------+------------+------------+------------------+
|       1 | Learn MySQL INSERT | 2017-07-21 | 2017-07-22 | Start learning.. |
+---------+--------------------+------------+------------+------------------+
1 row in set (0.00 sec)
```

* 插入多行

```mysql
mysql> INSERT INTO tasks (SUBJECT,start_date,end_date,description) VALUES ('任务-1','2017-01-01','2017-01-02','Description 1'),('任务-2','2017-01-01','2017-01-02','Description 2'),('任务-3','2017-01-01','2017-01-02','Description 3');
Query OK, 3 rows affected (0.00 sec)
Records: 3  Duplicates: 0  Warnings: 0
```

* 查看数据

```mysql
mysql> SELECT*FROM tasks;
+---------+--------------------+------------+------------+------------------+
| task_id | SUBJECT            | start_date | end_date   | description      |
+---------+--------------------+------------+------------+------------------+
|       1 | Learn MySQL INSERT | 2017-07-21 | 2017-07-22 | Start learning.. |
|       3 | 任务-1             | 2017-01-01 | 2017-01-02 | Description 1    |
|       4 | 任务-2             | 2017-01-01 | 2017-01-02 | Description 2    |
|       5 | 任务-3             | 2017-01-01 | 2017-01-02 | Description 3    |
+---------+--------------------+------------+------------+------------------+
4 rows in set (0.00 sec)
```



> 如果为表中的所有列指定相应列的值，则可以忽略`INSERT`语句中的列列表



* 具有SELECT子句的INSERT

```mysql
mysql> CREATE TABLE tasks_bak LIKE tasks;
mysql> INSERT INTO tasks_bak SELECT*FROM tasks;
mysql> SELECT*FROM tasks_bak;
+---------+--------------------+------------+------------+------------------+
| task_id | SUBJECT            | start_date | end_date   | description      |
+---------+--------------------+------------+------------+------------------+
|       1 | Learn MySQL INSERT | 2017-07-21 | 2017-07-22 | Start learning.. |
|       3 | 任务-1             | 2017-01-01 | 2017-01-02 | Description 1    |
|       4 | 任务-2             | 2017-01-01 | 2017-01-02 | Description 2    |
|       5 | 任务-3             | 2017-01-01 | 2017-01-02 | Description 3    |
+---------+--------------------+------------+------------+------------------+
4 rows in set (0.00 sec)
```

### update 语句

* 我们使用`UPDATE`语句来更新表中的现有数据。也可以使用`UPDATE`语句来更改表中单个行，一组行或所有行的列值

```mysql
UPDATE [LOW_PRIORITY] [IGNORE] table_name 
SET 
    column_name1 = expr1,
    column_name2 = expr2,
    ...
WHERE
    condition;
```

在上面`UPDATE`语句中：

- 首先，在`UPDATE`关键字后面指定要更新数据的表名。
- 其次，`SET`子句指定要修改的列和新值。要更新多个列，请使用以逗号分隔的列表。以字面值，表达式或`子查询`的形式在每列的赋值中来提供要设置的值。
- 第三，使用`WHERE子句`中的条件指定要更新的行。`WHERE`子句是可选的。 如果省略`WHERE`子句，则`UPDATE`语句将更新表中的所有行。

请注意，`WHERE`子句非常重要，所以不应该忘记指定更新的条件。 有时，您可能只想改变一行; 但是，可能会忘记写上`WHERE`子句，导致意外更新表中的所有行。

MySQL在`UPDATE`语句中支持两个修饰符。

- `LOW_PRIORITY`修饰符指示`UPDATE`语句延迟更新，直到没有从表中读取数据的连接。 `LOW_PRIORITY`对仅使用表级锁定的**存储引擎**(例如*MyISAM*，*MERGE*，*MEMORY*)生效。
- 即使发生错误，*IGNORE*修饰符也可以使*UPDATE*语句继续更新行。导致错误(如重复键冲突)的行不会更新。



* 从`employees`表查询`Mary`的电子邮件

```mysql
mysql> SELECT firstname,lastname,email FROM employees WHERE employeeNumber=1056;
+-----------+-----------+----------------------+
| firstname | lastname  | email                |
+-----------+-----------+----------------------+
| Mary      | Patterson | mpatterso@yiibai.com |
+-----------+-----------+----------------------+
1 row in set (0.01 sec)
```



* 使用`UPDATE`语句将`Mary`的电子邮件更新为新的电子邮件

```mysql
mysql> UPDATE employees SET email='mary.new@yiibai.com' WHERE employeeNumber=1056;
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

* 再次执行`SELECT`语句来验证更改

```mysql
mysql> SELECT firstname,lastname,email FROM employees WHERE employeeNumber=1056;
+-----------+-----------+---------------------+
| firstname | lastname  | email               |
+-----------+-----------+---------------------+
| Mary      | Patterson | mary.new@yiibai.com |
+-----------+-----------+---------------------+
1 row in set (0.00 sec)
```

### delete 语句

```
DELETE FROM table_name
WHERE condition;
```



> 首先，指定删除数据的表(`table_name`)。
>
> 其次，使用条件来指定要在`WHERE`子句中删除的行记录。如果行匹配条件，这些行记录将被删除。
>
> 请注意，`WHERE`子句是可选的。如果省略`WHERE`子句，`DELETE`语句将删除表中的所有行。








