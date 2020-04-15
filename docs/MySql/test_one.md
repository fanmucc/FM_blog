--  检索数据
select id,name from test_one  -- 多行检索
select name from test_one    
select * from test_one
select DISTINCT name from test_one		-- distinct 只返回不同的值，相同的值会被过滤掉
select distinct id, name from test_one
select distinct name,id from test_one		-- 当检索出现多个条件时，只有多个条件的值一致时才会被过滤
select name,id from test_one limit 2		-- 限制结果 只输出前两行
select name from test_one limit 2,2			-- 限制结果，从第二行开始的后2行(计算机从0开始), 既从第3行开始到第4行结束
select name from test_one limit 3 offset 2  -- 上面 limit 2,2 的替代语句， 意思为第三行结束，从第二行开始
select test_one.name from test.test_one     -- 表名也可以是完全限定， 此句意思为 从test库中的test_one 表里 查找test_one的name列的值

-- 排序检索数据
select id from test_one order by id			-- order by子句 升序 由小到大
select id, name, age from test_one order by id, name, age  -- 多条件排序， 只有order by 主要以其后面的属性名来进行排序，如果其值相同，才会以后面的为主, 下个例子
select age, id, name from test_one order by age, id, name
select id, name from test_one order by id desc			   -- 降序排序
select id, name, age from test_one order by age desc, id, name			-- 以order by 及 desc 中间的属性为主进行倒序排序
select age from test_one order by age asc			-- 升序

-- 过滤数据
-- where --
select id from test_one where id > 2			-- 筛选id值大于2的内容  操作符 = 相等 <> 不等于  != 不等于 < 小于  > 大于 <= 小于等于  >= 大于等于  between 在指定的两个值之间
select name from test_one where name = 'fanmu'	
select name from test_one where name <> 'fanmu'
select age, name from test_one where age between 20 and 22   -- 范围检查 包括所定义的范围值  用and链接符 
select age from test_one where age is null  -- is null 检查是否为空值null 没有则返回空

-- 数据过滤
