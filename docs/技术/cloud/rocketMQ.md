# 配置环境

## Rocket MQ

安装[Releases · apache/rocketmq](https://github.com/apache/rocketmq/releases)

### Please set the ROCKETMQ_HOME variable in your environment!

#### 在mqnamesrv.cmd文件中加入这些

```bash
set ROCKETMQ_HOME=E:\rocketmq-all-5.3.2-bin-release
set JAVA_HOME=E:\zulu-17\
```

#### mqadmin中加入

```bash
set JAVA_HOME=E:\zulu-17\
```

### Caused by: org.apache.rocketmq.client.exception.MQClientException: No route info of this topic, LOGIN_TOPIC

> mqadmin updateTopic -c DefaultCluster -t LOGIN\_TOPIC -n localhost:9876[error] Make sure the specified clusterName exists or the name server connected to is correct.TopicConfig [topicName=LOGIN\_TOPIC, readQueueNums=8, writeQueueNums=8, perm=RW-, topicFilterType=

```bash
E:\rocketmq-all-5.3.2-bin-release\bin>mqadmin updateTopic -c DefaultCluster -t LOGIN_TOPIC -n localhost:9876
create topic to 172.29.32.1:10911 success.
TopicConfig [topicName=LOGIN_TOPIC, readQueueNums=8, writeQueueNums=8, perm=RW-, topicFilterType=SINGLE_TAG, topicSysFlag=0, order=false, attributes={}]
```

### 修改参数

mqnameserver，mqbroker中使用runbroker.cmd、runbroker.cmd中

修改-Xms512m,xn也需要该，一开始为2G

-Xms512m -Xmx512m -Xmn256m

### 修改broker.conf配置档

```
notepad %ROCKETMQ_HOME%/conf/broker.conf
```

加上以下内容

```
brokerClusterName = DefaultCluster
brokerName = broker-a
brokerId = 0
deleteWhen = 04
fileReservedTime = 48
brokerRole = ASYNC_MASTER
flushDiskType = ASYNC_FLUSH
# 启用 sq192过滤模式 
enablePropertyFilter=true
# 启用 broker 自动创建主题
enableAutoCreateTopic=true
#数据存储磁盘可用空间比例,如果小于该空间就会报错
diskMaxUsedSpaceRatio=98
# NameServer 地址
namesrvAddr=localhost:9876
```

### 设置 `%ROCKETMQ_HOME%`

```bash
setx ROCKETMQ_HOME "E:\rocketmq-all-5.3.2-bin-release"
setx JAVA_HOME # 最好是1。8版本
```

![image.png](assets/环境百度.png)

### 创建cmd指令

```bash
%ROCKETMQ_HOME%\bin\mqnamesrv.cmd

%ROCKETMQ_HOME%\bin\mqbroker.cmd -c %ROCKETMQ_HOME%\conf\broker.conf

#最后这条可能不需要执行
%ROCKETMQ_HOME%\bin\mqadmin.cmd updateTopic -c DefaultCluster -t LOGIN_TOPIC -n 127.0.0.1:9876
```
