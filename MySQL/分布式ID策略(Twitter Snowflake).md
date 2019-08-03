# MySQL分布式id生成策略`Twitter Snowflake`
[github地址_github.com/twitter-archive/snowflake](https://github.com/twitter-archive/snowflake)
### Snowflake 生成的 unique ID 的组成 (由高位到低位):
+ 1   bits: 最高位是0(无符号)
+ 41 bits: Timestamp (毫秒级时间戳) 能用到2039/9/7 23:47:35
+ 10 bits: 节点 ID (datacenter ID`数据库标识` 5 bits + worker ID`业务标识` 5 bits)
+ 12 bits: sequence number (序列号)
>`有效字节`一共 63 bits (最高位是 0)