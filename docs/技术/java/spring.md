BeanFactory是ApplicationContext的父接口

也是applicationContext的成员变量，通过组合来实现功能

### BeanFactory和ApplicationContext的区别

1. bean工厂和bean容器（更后期，更加高级）
2. appContext对beanFactory进行了扩展

### 读取配置中的数据

#### yml中引用变量

${}

使用""字符串支持转义符

#### 读取引用数据

1. 创建类
2. 定义为spring管控的bean，@component
3. 指定加载的配置中的数据，@configuration（prefix=）

![1739167716131](image/spring/1739167716131.png)

如果在不在引导类所在的包和父包下的话，需要加上引导类
![1739174520335](image/spring/1739174520335.png)

#### 第三方Bean属性绑定

![1741221837357](image/spring/1741221837357.png)

![1741222563131](image/spring/1741222563131.png)

![1741222554874](image/spring/1741222554874.png)

#### 整合mybatis

②添加依赖

mybatis starter

postgresql driver

![1739177368402](image/spring/1739177368402.png)

![1739177378282](image/spring/1739177378282.png)

![1739177449570](image/spring/1739177449570.png)

#### 整合druid

![1739235980225](image/spring/1739235980225.png)

或者

![1739235973668](image/spring/1739235973668.png)

### 配置文件

#### 四级文件目录

![1740900770148](image/spring/1740900770148.png)

合并所有的属性，高级的替代低级的

#### 参数指定配置文件

spring.config.name=xxx

指定配置文件名称

classpath:/xxx.yml

#### 多环境配置

![1740903543937](image/spring/1740903543937.png)

#### 文件配置

![1740903764533](image/spring/1740903764533.png)

#### 组控制group

![1740908838679](image/spring/1740908838679.png)

### 日志控制

默认info级别以上

debug：true，可以显示debug

#### 设置整体的日志级别

```yaml
loggin：
	level：
		root：info
```

#### 设置日志组

![1741049776582](image/spring/1741049776582.png)

#### 日志文件

### 启动热部署

![1741087405338](image/spring/1741087405338.png)

热部署只有restart的过程，不需要重新加载jar包![1741087490029](image/spring/1741087490029.png)

### 数据校验

![1741763351568](image/spring/1741763351568.png)

![1741763380318](image/spring/1741763380318.png)

### yml格式

0(0-7) 八进制

0x(0-9, a-f) 16进制

![1741766083931](image/spring/1741766083931.png)

### 测试属性加载

![1741768218482](image/spring/1741768218482.png)![1741768241662](image/spring/1741768241662.png)

### web环境启动模拟

![1741768959434](image/spring/1741768959434.png)

![1741769404589](image/spring/1741769404589.png)![1741769929392](image/spring/1741769929392.png)

#### 请求体json匹配

![1741830078432](image/spring/1741830078432.png)

#### 请求头匹配

![1741830165886](image/spring/1741830165886.png)

### spring 事务

#### 事务的特性（ACID）

1. 原子性
2. 一致性
3. 隔离性
4. 持久性

#### 如何保证数据库的原子性

发生异常的时候，根据undolog恢复到执行前的数据

#### 事务管理器

```java
package org.springframework.transaction;

import org.springframework.lang.Nullable;

public interface PlatformTransactionManager {
    //获得事务
    TransactionStatus getTransaction(@Nullable TransactionDefinition var1) throws TransactionException;
    //提交事务
    void commit(TransactionStatus var1) throws TransactionException;
    //回滚事务
    void rollback(TransactionStatus var1) throws TransactionException;
}
```

#### [事务属性](https://javaguide.cn/system-design/framework/spring/spring-transaction.html#transactiondefinition-%E4%BA%8B%E5%8A%A1%E5%B1%9E%E6%80%A7) TransactionDefinition

1. 传播行为
2. 隔离级别
3. 回滚规则

##### **`PROPAGATION_REQUIRED`**

1. 外方法没开启事务或者不是required的话，内方法是required，内方法会新开一个自己的事务，互不打扰
2. 内外方法都是required的话，就是用同一个事务

##### `PROPAGATION_REQUIRED_NEW`

1. 内方法required new，新建一个事务，互不干扰

##### **`PROPAGATION_NESTED`**

1. 子事务依赖于父事务，父级提交，子才能提交，父级回滚，子回滚

##### **`MANDATORY`**

1. 强制需要事务

#### 事务状态 TransactionStatus

#### spring aop动态代理

如果目标对象实现了接口，使用jdk Proxy创建代理对象

如果没实现接口，使用了继承，使用Cglib


### spring cache


![1748508961259](image/spring/1748508961259.png)
