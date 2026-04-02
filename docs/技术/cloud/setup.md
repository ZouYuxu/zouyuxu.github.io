### zookeeper

#### 安装

```bash
scoop install zookeeper
```

或者按照这个教程

[ZooKeeper安装教程1.下载网站 https://mirrors.tuna.tsinghua.edu.cn/apa - 掘金](https://juejin.cn/post/7291936541395910675)


#### 配置

环境变量

```bash
setx ZOOKEEPER_HOME E:\Scoop\apps\zookeeper\3.9.3
```

 

`zkserver.cmd中在call Java后面加上 `

`"-Dzookeeper.audit.enable=true"`
