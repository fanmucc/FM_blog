#### 查询数据

简单示例(student表)

`SELECT name FROM test`   从test表中查询name列
`SELECT name, age FROM test` 从test表中查询name,age列
`SELECT DISTINCT age FROM test` DISTINCT 限定词， 返货test中不同的值，相同的值则会过滤掉
`SELECT DISTINCT name, age FROM test` 当限定词后面跟着两个条件时，只有两个条件的值相同才能过滤，否则一律返回

`SELECT name FROM test LIMIT 5`  返回name前5列
`SELECT name FROM test LIMIT 1,2`  返回name列 从第一列内容开始 到 第二列内容结束 就返回 1~2列；
`SELECT name FROM test LIMIT 2 OFFSET 1` 和上面内容相同 从第一列开始到第2列结束

使用完全限定的表名
`SELECT text.name FROM text.text`   // 从text数据库中的text表里查询name列

> SELECT * (* 表示全部,会展示符合条件的全部信息,如果只想获取单个字段的话将*替换成相应的字段名) FROM 表名 WHERE 判断修改那个字段值得条件(id =1 的内容)

`select * from student where grade > 50;`  // 查询grade大于50的数据

![运算符](https://i.loli.net/2019/10/19/mvzeIdatK5piX1n.png)

##### 多条件查询

> SELECT 字段名, 字段名... FROM 表名 WHERE 条件

`select name, password from user where name = 'fanmu' AND password = 123456`

#####  正序

> SELECT * (* 表示全部,会展示符合条件的全部信息,如果只想获取单个字段的话将*替换成相应的字段名) FROM 表名 ORDER BY 根据那个字段进行正序的字段名 ASC

##### 倒叙 

> SELECT * (* 表示全部,会展示符合条件的全部信息,如果只想获取单个字段的话将*替换成相应的字段名) FROM 表名 ORDER BY 根据那个字段进行倒叙的字段名 DESC