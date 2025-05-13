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

## feign

声明式的伪http客户端，只需创建接口添加注解

feign默认继承了ribben，负载均衡

### 服务调用者方增加

![1747126350657](image/nacos/1747126350657.png)

![1747126529949](image/nacos/1747126529949.png)

![1747126566053](image/nacos/1747126566053.png)
