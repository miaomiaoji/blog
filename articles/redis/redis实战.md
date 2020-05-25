相关网站：
- [Redis-in-action源码地址以及原书英文版地址](http://redisinaction.com/)
- [本书代码的javascript版本](https://github.com/josiahcarlson/redis-in-action/tree/master/node)
- [redis不同语言使用的包](https://redis.io/clients)
- [node_redis使用](https://github.com/NodeRedis/node_redis)
- 


## Redis简介
Redis是一个速度非常快的非关系数据库，可以存储键(key)与多种不同类型的值(value)之间的映射(mapping)，可以将存储在内存中的键值对**数据持久化**到硬盘，可以使用**复制特性来扩展读**性能，还可以使用**客户端分片来扩展写**性能。
> 客户端分片：将数据存储到多台机器中，也可以从多台机器中获取数据，可以在解决某些问题时获得线性级别的性能提升。

#### 与其他数据库对比
- 不使用表，也不会预定义或者强制要求用户对Redis的不同数据进行关联
- 可作为主数据库，也可以作为辅数据库
- 通过复制，持久化和事务保证数据的完整性
#### 附加特性
- 两种方式持久化
  - 时间点转储：指定时间内由指定数量的写操作执行
  - 将所有修改了数据库的命令都写入一个只追加文件中
- 主从复制特性:为了扩展读性能，提供故障转移支持
  - 执行复制操作的从服务器连接上主服务器，接收主服务器发送的整个数据库的初始副本；之后主服务器执行的写命令，都会被发送给所有从服务器去执行，从而实时更新从服务器的数据集。所以客户端可以向任意一个从服务器发送读请求，避免对主服务器的集中式访问
#### 使用Redis的理由
- 支持多种数据类型，各种类型由相应的操作
- 运行效率和易用性比关系数据库好
- 对于数据库随机写操作非常快

## redis数据类型操作
### 字符串
```
set hello world
get hello
del hello
```
### 列表
```
lpush list-item item
lrange
lindex
lpop
```
### 集合
```
sadd
smembers
sismember
srem

sinter
sunion
sdiff
```
### 散列
```
hset hash-key sub-key1 value1
hget hash-key sub-key1
hgetall hask-key
hdel hash-key sub-key1
```
### 有序集合
有序集合的值称为分值，分值必须为浮点数。可以根据成员访问元素，也可以根据分值以及分值的排列顺序来访问元素。
```
<!-- 添加元素 -->
zadd zset-key 728 member1
zadd zset-key 982 member0
<!-- 获取一个范围中获取多个元素 -->
zrange zset-key 0 -1 withscores
<!-- 获取分值范围内的所有元素 -->
zrangebyscore
<!-- 如果元素在有序集合中,移除成员 -->
zrem  
```


