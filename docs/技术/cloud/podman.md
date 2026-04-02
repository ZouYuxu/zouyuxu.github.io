### podman

```
podman machine start

pip3 install podman-compose
```

### podman-compose

```
podman-compose up -d
podman-compose down

```

### 参考资料

[podman快捷键](https://docs.podman.org.cn/en/latest/Commands.html)

[Podman Compose 新手指南 - 堆码志 - 博客园](https://www.cnblogs.com/rockety/p/17291605.html)

[摆脱Docker-compose的限制，实现从Podman-compose到Pod化的过程 - Blog - Silicon Cloud](https://www.silicloud.com/zh/blog/%e6%91%86%e8%84%b1docker-compose%e7%9a%84%e9%99%90%e5%88%b6%ef%bc%8c%e5%ae%9e%e7%8e%b0%e4%bb%8epodman-compose%e5%88%b0pod%e5%8c%96%e7%9a%84%e8%bf%87%e7%a8%8b%e3%80%82/)

[podman在Windows下更换registry镜像 - 掘金](https://juejin.cn/post/7163211173154799624)

[如何配置 Podman 使用国内镜像源？\_podman国内镜像\_podman配置国内镜像镜像-CSDN博客](https://blog.csdn.net/m0_55025322/article/details/137677307)

### 已失效，无需操作

~~国内的镜像源（镜像站）加速地址有：~~

* 阿里云（需登录，免费），`http://<你的ID>.mirror.aliyuncs.com`
* 网易，`http://hub-mirror.c.163.com`
* 百度，`https://mirror.baidubce.com`
* 上海交大，`https://docker.mirrors.sjtug.sjtu.edu.cn`
* 南京大学，`https://docker.nju.edu.cn`

```
unqualified-search-registries = ["docker.io"]

[[registry]]
prefix = "docker.io"
insecure = false
blocked = false
location = "docker.io"

[[registry.mirror]]
# 百度镜像源
location = "mirror.baidubce.com"
insecure = true
[[registry.mirror]]
# 网易 163 镜像源
location = "hub-mirror.c.163.com"
insecure = true
[[registry.mirror]]
# 上海交大镜像源
location = "docker.mirrors.sjtug.sjtu.edu.cn"
insecure = true
[[registry.mirror]]
# 南京大学镜像源
location = "docker.nju.edu.cn"
insecure = true

```
