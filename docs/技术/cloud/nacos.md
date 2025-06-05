## nacos

### pom文件添加依赖

```yaml

```

### app中加上

```
@EnableDiscoveryClient
public class TripGateWayApplication {
```

### yml文件中加上

```json
server:
  port: 9999
spring:
  application:
    name: trip-gateway
  cloud:
    nacos:
      discovery: # 服务注册中心地址
        server-addr: 127.0.0.1:8848
```

## nacos config

配置中心

1. 统一管理配置
2. 必须重启微服务才能生效

![1747208584944](image/nacos/1747208584944.png)

## gateway

applicaiton yml

![1747138867459](image/nacos/1747138867459.png)

自定义路由转发

![1747138995509](image/nacos/1747138995509.png)

id：唯一

uri：匹配规则后，请求的路径，lb（load balance）+服务名称

predicates：数组类型：断言url是否匹配规则，成功的话转发到uri上去

filters：strip去除前缀，再转发给uri，比如order-serv/orders/1变成orders/1

## feign

声明式的伪http客户端，只需创建接口添加注解

feign默认继承了ribben，负载均衡

### 服务调用者方增加

![1747126350657](image/nacos/1747126350657.png)

![1747126529949](image/nacos/1747126529949.png)

![1747126566053](image/nacos/1747126566053.png)

## 跨域问题

协议、ip、端口一致

1. 前端设置代理
2. 后端允许访问

### springboot跨域访问

![1747287147907](image/nacos/1747287147907.png)

### springcloud

![1747287496477](image/nacos/1747287496477.png)

## nacos鉴权

### config配置档

nacos\conf\application.properties

```properties
### If turn on auth system:
nacos.core.auth.enabled=true

nacos.core.auth.server.identity.key=jojo
nacos.core.auth.server.identity.value=jojo

### worked when nacos.core.auth.system.type=nacos

### The default token (Base64 String):
nacos.core.auth.plugin.nacos.token.secret.key=VGhpc01zTX1DdXN0b21TZWNyZXRLZXkwMTIzNDU2Nzg=
```

默认账号密码是 nacos/nacos
