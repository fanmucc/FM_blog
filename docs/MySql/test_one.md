--  检索数据
-- 关键词 distinct 过滤
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
-- 关键词 order by 排序 默认升序     desc 倒叙  asc 升序
select id from test_one order by id			-- order by子句 升序 由小到大
select id, name, age from test_one order by id, name, age  -- 多条件排序， 只有order by 主要以其后面的属性名来进行排序，如果其值相同，才会以后面的为主, 下个例子
select age, id, name from test_one order by age, id, name
select id, name from test_one order by id desc			   -- 降序排序
select id, name, age from test_one order by age desc, id, name			-- 以order by 及 desc 中间的属性为主进行倒序排序
select age from test_one order by age asc			-- 升序

-- 过滤数据
-- 关键词  where    between 两个值范围中间
select id from test_one where id > 2			-- 筛选id值大于2的内容  操作符 = 相等 <> 不等于  != 不等于 < 小于  > 大于 <= 小于等于  >= 大于等于  betwee 在指定的两个值之间
select name from test_one where name = 'fanmu'	
select name from test_one where name <> 'fanmu'
select age, name from test_one where age between 20 and 22   -- 范围检查 包括所定义的范围值  用and链接符 
select age from test_one where age is null  -- is null 检查是否为空值null 没有则返回空


-- 数据过滤
-- 关键词 and/or  计算次序 ()  in 操作符 指定范围  not操作符 否定后面所带的条件，有排除的意思和in操作符连用
select id, name from test_one where id != 1 and name != 'fan'
select id, name, age from test_one where id !=1 or id !=2
select id, name, age from test_one where (id != 1 or id !=2) and age > 21
select id, name, age from test_one where id in (1,3) order by id desc
select id, name, age from test_one where id not in (1,3) order by id desc

-- 通配符 
-- 关键字  like  %号通配符匹配多个字符  _下划线通配符匹配单个字符
select id, cart_name from test_one where cart_name like 'guo%'
select id, cart_name from test_one where cart_name like '%guo%'
select id, cart_name from test_one where cart_name like "shan%123"
select id, cart_name from test_one where cart_name like "shangpin12_"
select id, cart_name from test_one where cart_name like "_hangpin123"

-- 正则表达式
-- 关键字 REGEXP
select id, name, cart_name from test_one where name REGEXP '[a-z]'


-- 创建计算字段
-- concat()拼接串  Rtrim()去掉右边的所有空格  as关键字赋值
select Concat(name,'(', age) from test_one order by age
select Concat(name,'(', age, ')')  as ages from test_one order by age


-- 使用数据处理函数
-- Upper() 小写转大写  Left()返回串左边的字符 length()返回串的长度  Locate()找出串的一个子串  Lower() 将串转为小写  LTrim() 去掉串左侧的空格 Rtrim()去掉串右侧的空格  Rigth() 返回串右边的字符
-- Soundex() 返回串的soundex值 subString() 返回子串的字符 
select Upper(name) as Name from test_one order by name

-- 时间及数值处理函数

-- 汇总数据
-- 关键字 AVG() 返回某的平困之 count() 返回某列的列数 max() 返回某列的最大值 min() 返回某列的最小值 sum() 返回某列之和
select AVG(age) as ageAvg from test_one 
select count(age) as ageCount from test_one
select max(age) as ageMax from test_one
select min(age) as ageMin from test_one
select sum(age) as ageSum from test_one
select count(*) from test_one
select avg(id) as idavg, max(age) as ageMax from test_one

