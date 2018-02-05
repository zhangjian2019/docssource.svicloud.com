---
name: 安装前提
---

# 操作系统 



# 内核升级
# Ubuntu 升级内核（如最新，可跳过）：

**直接使用 apt-get 安装内核**

apt-get update

apt-cache search linux-image-extra

**安装最新的内核**

apt-get install linux-image-extra-<NEWEST_KERNEL_RELEASE>

dpkg -l | grep linux-image

apt-get remove <OLD_KERNEL_RELEASE>

update-grub

reboot

**查看一下目前的内核版本**

应该是显示为 <NEWEST_KERNEL_RELEASE>

uname -r

**当前内核为：**

![image](https://note.youdao.com/yws/api/personal/file/B941815143204B808650F1E109F120BD?method=download&shareKey=036dfdbe8ed1acc6503ea7bfaa8f1fa3)


