# EXPLAIN 执行计划分析
1. type列，连接类型。一个好的sql语句至少要达到range级别。杜绝出现all级别
(system > const > eq_ref > ref > fulltext > ref_or_null > index_merge > nique_subquery > index_subquery > range > index > ALL)
1. key列，使用到的索引名。如果没有选择索引，值是NULL。可以采取强制索引方式
2. key_len列，索引长度
3. rows列，扫描行数。该值是个预估值
4. extra列，详细说明。注意常见的不太友好的值有：Using filesort, Using temporary
- - - - - - - - - - - - 
## 优化方案
1. between > IN > OR
>如果限制条件中其他字段没有索引，尽量少用or
>再例如：select id from t where num in(1,2,3) 对于连续的数值，能用 between 就不要用 in 了
1. JOIN >SUBSELECT(子查询)
2. SELECT语句务必指明字段名称
3. 只有一条查询结果limit 1
4. 如果排序字段没有用到索引，就尽量少排序(容易出现文件排序)
5. 尽量用union all代替union
>union会做去重处理 加重CPU的运算量
1. 使用合理的分页方式以提高分页的效率
 >select id,name from product limit 866613, 20   >>>  select id,name from product where id> 866612 limit 20
2. 避免在 where 子句中对字段进行 null 值判断(索引失效全表扫描)