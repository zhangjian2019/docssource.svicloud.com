---
name: Docker 安装
---

# 安装 Docker

```bash
# 国内 DaoCloud 镜像安装
curl -sSL https://get.daocloud.io/docker | sh
# clone 后直接脚本安装
git clone https://github.com/rancher/install-docker.git
cd ./install-docker && bash <LATEST__XX>.sh
Docker 开机自启动
systemctl  enable docker.service
```

# 检查

    docker info | grep WARN
    
> WARNING: No swap limit support
> 解决方法见第 1 步，配置 `grub` 参数

> WARNING: bridge-nf-call-ip6tables is disabled
> 解决方法：

    vim /etc/sysctl.conf
        net.bridge.bridge-nf-call-ip6tables = 1
        net.bridge.bridge-nf-call-iptables = 1
        net.bridge.bridge-nf-call-arptables = 1

    sysctl -p
    
    # 配置 Docker 加速器（用于国内加速）
> 以下操作需重启 Docker 服务生效

vi /etc/docker/daemon.json

```json
{
  "registry-mirrors": [
     "https://2lqq34jg.mirror.aliyuncs.com",
     "https://pee6w651.mirror.aliyuncs.com",
     "https://registry.docker-cn.com",
     "http://hub-mirror.c.163.com"
  ]
}
配置加速后要重启或reload
service docker reload
```

# 配置 Docker 代理（用于国内无法访问国外某些网站的 https）

```bash
vi /etc/docker/daemon.json

# 直接启动（当然也可以写入 systemd）
http_proxy=<IP_ADDR>:<PORT> https_proxy=<IP_ADDR>:<PORT> dockerd
```
