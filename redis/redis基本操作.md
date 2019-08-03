#Redis基本操作

##Redis Key
|cmmand|desc|
|---|---|
keys pattern | 查找所有符合给定模式( pattern)的 key( keys *xxx)
type key | 查看 key存储的数据类型
del key | 删除key
exisits key | 检查key是否存在
rename key newkey | 重命名key的名字
rename<b>nx</b> key newkey| 仅当 newkey 不存在是进行重命名操作
move key dbNo |将前key移动到指定的的数据库db中
-- | --
expire key sec | 设置过期时间(秒)
expire<b>at</b> key timestamp | 设置过期时间(unix 秒)
ttl key | 返回key的过期时间(秒)
-- | --
<b>p</b>expire key  mill | 设置过期时间(毫秒)
<b>p</b>expire<b>ta</b> key  mil-timestamp | 设置过期时间的时间戳(unix 毫秒)
pttl key | 返回key的过期时间(毫秒)
-- | -- 
persist key  | 清除过期时间 永久保存key

## Redis string
|cmmand|desc|
|---|---|
strlen | 返回key的字符串长度
get key | 获取key的值
getset key val | 指定key设置值 并返回old值
mget key1 key2...  | 获取多个key的值
getrange key start(int) end(int)  |截取字符串
-- |  --
set key val | 指定key设置值
setnx key val | 仅当key不存在时 设置值
setex key sec  val |  设置值 并添加过期时间(秒)
psetex key mill  val |  设置值 并添加过期时间(毫秒)
mset key1 val1 key2 val2 ... | 批量设置 key
metnx key1 val1 key2 val2 ... | 批量设置 key 仅当不存在时设置
setrange key index val | 覆盖设定值 从index开始
-- | -- 
incr key | 将key中的数字+1
incrby key increment | 将key指定+量
incrbyfloat key increment |将key指定+量的float
decr | 将key中的数字 - 1
decrby key increment | 将key指定-量
append key val | 如果key 是string 则append在末尾添加一个字符串

#Redis hash
|cmmand|desc|
|---|---|



## Redis List
|cmmand|desc|
|---|---|
lindex key index | 通过索引index 获取list中的值
llen key | 获取list的长度
lrange key  indx1(int) index2(int) | 获取 截取 list中的元素
blpop key1 {key2} timeout | 移除并获取 第一个元素 没有元素会堵塞 timeout(秒)
brpop key1 {key2} timeout |移除并获取 最后一个元素 没有元素会堵塞 timeout(秒)
linsert key {before | after} v1 val | 在v1 之前或者之后插入元素
--|--
lset key index val | 通过索引值设置元素
lpush key val1 {val2...} |将一个值或多个值插入到list头部
rpush key val1 {val2...} |将一个值或多个值插入到list尾部
lpushx key val |  仅当 key存在时将val插入到 list头部
rpushx key val |  仅当 key存在时将val插入到 list尾巴部
--|--
lpop key | 移除并返回第一次个元素
rpop key | 移除并返回最后一次个元素
ltrim index1 index2  | 存在 index1-index2 之间的元素 其他删除
lrem key count(int) value | 移除列表中与val相等的参数, `count > 0`: 从表头开始向表尾搜索，移除与 VALUE 相等的元素，数量为 COUNT 。`count < 0`: 从表尾开始向表头搜索，移除与 VALUE 相等的元素，数量为 COUNT 的绝对值。`count = 0`: 移除表中所有与 VALUE 相等的值。
rpoplpush list1 list2 timeout  | 从list1中取出最后一个元素，并插入到lis2的尾部(阻塞)
brpoplpush list1 list2 timeout  | 从list1中取出最后一个元素，并插入到lis2的头部(阻塞)