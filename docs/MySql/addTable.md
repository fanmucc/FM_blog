#### 增加数据

简单示例(使用刚刚创建的空表student表)

> INSERT INTO 表名(字段名1，字段名2，，，，，字段名n) VALUES(值1，值2，，，，值n)

``` insert into student (id, name, grade) values (1, 'zhangsan', 98.5)```

插入多条数据

> INSERT INTO 表名 (字段名1，字段名2，，，，，字段名n) VALUES(值1，值2，，，，值n),(第二条数据),...

!> 插入数据时也不是必须写出字段名,但是必须按照相应顺序进行添加;

`insert into student values(4, 'eoeo', 70)`