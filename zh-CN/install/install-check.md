---
name: 检查安装
---

# 若想删除rancher-server

```bash
docker rm -f -v rancher-server
```

重启机器后，由于dns问题会丢失/etc/resolv.conf中的内容，需重新添加

```bash
vi /etc/resolv.conf 

nameserver 114.114.114.114
```
添加后启动rancher

```bash
docker start rancher-server
```

查看：docker ps

![image](https://note.youdao.com/yws/api/personal/file/D6E6F9AFD572442EB2600E9D67A22F48?method=download&shareKey=7d086c231e268c428ac0abd27c5d4ad1)


对于主机中显示DISCONNECTED（非ACTIVE）,在该机器上启动agent：
```bash
docker start rancher-agent 
```
查看日志:
```bash
docker logs  -f rancher-agent
```
