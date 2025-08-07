### 意向所

加锁之前判断有没有行所，用意向所判断有无上锁

1. 意向共享锁（IS）：有意向对某些记录加S锁，加之前必须取得IS锁
2. 意向互斥锁（IX）：有意向对某些记录加X锁，加之前必须获取IX锁

意向锁只之间是兼容的，意向锁和表级别的共享锁和排他锁互斥，IS锁和S锁兼容

### 快找读和当前度

#### 快照读（一致性非锁定读）

每行记录有多个快照，如果读取的记录正在执行U、D的操作的话，不会去等待X锁，而是读取一个快照

1. 如果是RC级别下，读取最新的一份快照
2. RR，读取事务开始的那一份记录

#### 当前读

给记录加上X、S锁

### 自增锁

表级锁，insert的时候拿不到这个锁就阻塞，

#### 自增锁模式

传统、连续、交错（2）

交错模式下，所有的insert-like的语句都不使用表级别的锁，而是轻量级互斥锁

主从同步需求的话，设置为交错模式会有不一致的问题


### 实际问题

#### 如果栏位以;隔开，如何查询是否包含某个数据

例如123;456;789或者123；456或者456，如何查找是否456

直接ilike %email%是不行的，这样不是全匹配，可能会找到3456

```java
        String userEmail = UserInfoThreadLocalUtil.userIdLocal.get();
        String sql;
        MapSqlParameterSource params = new MapSqlParameterSource();

        if (StringUtils.equalsIgnoreCase("pending", vo.getType())) {
            sql = "SELECT * FROM xxx.table WHERE " +
                    "(reviewer ILIKE :userEmail OR " +
                    "reviewer ILIKE CONCAT(:userEmail, ';%') OR " +
                    "reviewer ILIKE CONCAT('%;', :userEmail) OR " +
                    "reviewer ILIKE CONCAT('%;', :userEmail, ';%'))";
        } else {
            sql = "SELECT * FROM table WHERE creator ILIKE :userEmail";
        }
        params.addValue("userEmail", userEmail);
        vo.setSortedColumnIfBlank("modify_date");
        StringBuilder stringBuilder = new StringBuilder(sql);
        return JDBCTemplateUtil.getPageResult(proccommonNamedJdbcTemplate, stringBuilder, vo, params, CommonInboxTaskEntity.class);
```
