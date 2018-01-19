---
name: 平台安装
---

# 单机安装

```bash
# 在一台服务器上执行命令

# 下载 rancher/server 镜像
docker pull rancher/server

# 启动
docker run -d --restart=always \
-v /opt/svicloud/rancher/server_db:/var/lib/mysql \
--name rancher-server -p 8080:8080  rancher/server

# 然后，浏览器打开 http://<SERVER_IP>:8080 即可
```

# 设置 Rancher SSL（可选）

```bash
mkdir -p /opt/svicloud/rancher/cert
cp cert.pem key.pem /opt/svicloud/rancher/cert

docker run -d \
--restart=always \
--name rancher-server-ssl \
--link rancher-server \
-p 80:80 -p 443:443 \
-e 'RANCHER_URL=<YOUR_DOMAIN>' \
-e 'RANCHER_CONTAINER_NAME=rancher-server' \
-e 'RANCHER_PORT=8080' \
-v /opt/svicloud/rancher/cert:/etc/nginx/external/ \
codedevote/nginx-ssl-proxy-rancher
```
