### Redis为什么这么快

1. redis基于内存，QPS大概是5w~10w+（MySQL是4k）
2. 单线程事件循环和IO多路复用机制
3. 高效的数据结构

### Redis的使用场景

1. 分布式锁
2. 限流
3. 消息队列
4. 延时队列

### Redis的基础数据类型

1. String
   最基础的类型，存放字符串、数字、图片（base64编码或者路径）、序列化的对象
2. List（双向链表）
3. Hash（哈希，键值对）
   经常修改对象的字段，使用hash
4. Set
5. Zset（有序集合）

特殊数据类型：

### 线程模型

多个客户端使用IO多路复用，文件事件分派器将事件 绑定 事件处理器

### 设置过期时间

```bash
setex key 60 value # 60s后过期string
expire key 60 # 其他类型
```

好处：

1. 缓解内存消耗
2. 临时存在的业务处理更高效（1分钟的验证码）

### 指令

删除制定前缀的key

```bash
    redis-cli --scan --pattern "prefix*" > keys.txt &&for /f %i in (keys.txt) do redis-cli DEL "%i"

```

查询制定前缀的key

```bash
keys xxxx*
```
