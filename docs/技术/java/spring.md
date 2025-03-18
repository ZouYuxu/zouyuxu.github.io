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
