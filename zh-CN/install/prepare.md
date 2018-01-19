---
name: 安装准备
---


# 服务器时间同步
> 如果不配置时间同步，可能会导致调度服务有可能不正常 <br>
> 最好使用 UTC time:<br>

    rm -rf /etc/localtime

# 支持 BBR，请升级内核至 4.9 以上版本（弱网环境建议）
> 如果要支持 aufs，请安装 linux-image-extra 的包

# 所有服务器需要设置外部 DNS
```bash
# stop and disable the local dns generator
systemctl disable systemd-resolved.service
systemctl stop systemd-resolved.service

# show the service status
systemctl status systemd-resolved.service


# Comment out the dns=dnsmasq line
# vi /etc/NetworkManager/NetworkManager.conf
  # dns=dnsmasq

# restart network and docker service
systemctl restart network-manager
systemctl restart docker


# 修改为外部 DNS 服务器
vi /etc/network/interfaces
  dns-nameservers 114.114.114.114
```


# 设置 hostname
    [root@rancher-server] echo "<HOSTNAME>" >/etc/hostname && hostname <HOSTNAME>
    [root@rancher-server] hostnamectl set-hostname svi1r01n08

