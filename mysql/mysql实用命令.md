# mysql实用命令

## 1.查看所有数据库容量大小

``` mysql
SELECT
	table_schema AS '数据库',
	sum( table_rows ) AS '记录数',
	sum( TRUNCATE ( data_length / 1024 / 1024, 2 ) ) AS '数据容量(MB)',
	sum( TRUNCATE ( index_length / 1024 / 1024, 2 ) ) AS '索引容量(MB)' 
FROM
	information_schema.TABLES 
GROUP BY
	table_schema 
ORDER BY
	sum( data_length ) DESC,
	sum( index_length ) DESC;
```

``` mysql
+--------------------+-----------+------------------+------------------+
| 数据库             | 记录数    | 数据容量(MB)     | 索引容量(MB)     |
+--------------------+-----------+------------------+------------------+
| java               |    778096 |            87.19 |            17.72 |
| mysql              |      3138 |             2.13 |             0.15 |
| yiibaidb           |      4004 |             0.35 |             0.14 |
| kfptzfb            |         0 |             0.14 |             0.31 |
| information_schema |      NULL |             0.10 |             0.00 |
| sys                |         6 |             0.01 |             0.00 |
| RUNOOB             |         4 |             0.01 |             0.00 |
| performance_schema |   1330790 |             0.00 |             0.00 |
+--------------------+-----------+------------------+------------------+
8 rows in set (0.10 sec)
```

## 2.查看所有数据库各表容量大小

``` mysql
SELECT
	table_schema AS '数据库',
	table_name AS '表名',
	table_rows AS '记录数',
	TRUNCATE ( data_length / 1024 / 1024, 2 ) AS '数据容量(MB)',
	TRUNCATE ( index_length / 1024 / 1024, 2 ) AS '索引容量(MB)' 
FROM
	information_schema.TABLES 
ORDER BY
	data_length DESC,
	index_length DESC 
	LIMIT 10;
```

```
+-----------+--------------------+-----------+------------------+------------------+
| 数据库    | 表名               | 记录数    | 数据容量(MB)     | 索引容量(MB)     |
+-----------+--------------------+-----------+------------------+------------------+
| java      | cnarea_2018        |    778092 |            87.17 |            17.72 |
| mysql     | help_topic         |       621 |             1.51 |             0.07 |
| mysql     | proc               |        48 |             0.28 |             0.00 |
| yiibaidb  | orderdetails       |      2996 |             0.15 |             0.07 |
| mysql     | help_keyword       |       728 |             0.09 |             0.07 |
| yiibaidb  | products           |       110 |             0.06 |             0.01 |
| mysql     | help_relation      |      1491 |             0.06 |             0.00 |
| yiibaidb  | orders             |       326 |             0.04 |             0.01 |
| mysql     | innodb_index_stats |       153 |             0.04 |             0.00 |
| kfptzfb   | my_buy_jnl         |         0 |             0.01 |             0.06 |
+-----------+--------------------+-----------+------------------+------------------+
10 rows in set (0.06 sec)
```

