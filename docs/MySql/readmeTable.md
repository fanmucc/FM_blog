#### 查询数据

简单示例(student表)

> SELECT * (* 表示全部,会展示符合条件的全部信息,如果只想获取单个字段的话将*替换成相应的字段名) FROM 表名 WHERE 判断修改那个字段值得条件(id =1 的内容)

`select * from student where grade > 50;`  // 查询grade大于50的数据

![运算符](https://i.loli.net/2019/10/19/mvzeIdatK5piX1n.png)

正序

> SELECT * (* 表示全部,会展示符合条件的全部信息,如果只想获取单个字段的话将*替换成相应的字段名) FROM 表名 ORDER BY 根据那个字段进行正序的字段名 ASC

倒叙 

> SELECT * (* 表示全部,会展示符合条件的全部信息,如果只想获取单个字段的话将*替换成相应的字段名) FROM 表名 ORDER BY 根据那个字段进行倒叙的字段名 DESC