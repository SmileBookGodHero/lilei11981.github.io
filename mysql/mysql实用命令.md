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

