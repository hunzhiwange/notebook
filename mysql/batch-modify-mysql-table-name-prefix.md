# Mysql 批量修改数据表前缀

有时候我们需要批量修改一下 MySQL 数据库表前缀，这个时候有时候少的时候可以手动改一下，但是数量一旦多了的话就不好整了。


## 修改表名原型

Mysql 可以通过下面的方式来修改表名字。

```sql
ALTER TABLE old_tablename RENAME TO new_tablename;
```

接着我们可以通过一个简单的 SQL 来获取批量修改的 SQL ,拷贝到一些数据库管理工具如 Mysqlworkbench、PHPMyadmin 等数据库管理工具中运行即可。

```sql
SELECT
    CONCAT(
        'ALTER TABLE ',
        table_name,
        ' RENAME TO ',
        SUBSTRING(table_name, 6),
        ';'
    )
FROM
    information_schema. TABLES
WHERE
    table_name LIKE 'test_%';
```