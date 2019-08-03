# MySQL锁
> 锁的粒度划分 `表锁`, `行锁`, `页锁`(BerkeleyDB)
1.  InnoDB 默认`行锁`, `支持表锁`(未命中索引时为表锁)
2. MyISAM 默认`表锁`, 不支持行锁

## 锁的纬度划分
1. 排它锁(`写锁 / X锁`)
2. 1. 共享锁(`读锁 / S锁`)
|Engine|排它锁|共享锁|
| --- | --- | --- |
|InnoDB|`select XXX for update`, `update`,`insert`,`delete`|默认不开启,`select XXX lock in share mode`
|MyISAM|`同InnoDB`|默认select开启共享锁

### 共享锁 / 排它锁 兼容性
|-/-|排它锁|共享锁|
| --- | --- | --- |
|排它锁|❌|❌|
|共享锁|❌|✅|


## 其他锁
> 加锁方式 `自动锁` `显示锁`
> 操作语句划分 `DML锁` `DDL锁`

## 锁和索引
>tips: InnoDB的非聚集索引加锁时, 会同时对聚集索引加锁
> 比如: select xxx from t_user where cardNum= 'xxxx' for update;
> 假设t_user表的聚集索引为主键`id`, 上面的sql使用了非聚集索引 `index_cardNum`
> 则: cardNum 被锁 同时id 也被锁
>  原因是`InnoDB`的非聚集索引不会存储数据内容,只会存储聚集索引的标志,根据聚集索引的标志去查询对应的数据内存,所以当index_cardNum被锁时,同时id也会锁住