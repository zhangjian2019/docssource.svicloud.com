---
name: Dockerfile
---
**登录Rancher及配置**

http://192.168.10.230:8080


**添加镜像库**

在基础架构-镜像库-添加镜像库（custom）：

地址：registry.sviyun.com

用户名：admin

密码：**********


在环境管理--cattle编辑---模板Cattle中

Networking中禁用Rancher ipsec，把Rancher VXLAN启用

**添加环境**

在环境管理-添加环境

添加环境成功后，即可查看基础设施

添加应用route53：

AWS_ACCESS_KEY: AKIAITPARJW7F4MWKSEA

AWS_SECRET_KEY: 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

NAME_TEMPLATE: %{{service_name}}.%{{stack_name}}.%{{environment_name}}

ROOT_DOMAIN：svi.pub

ROUTE53_MAX_RETRIES: 3

ROUTE53_ZONE_ID: Z2JG7XAAL9WE8F

点应用-基础设施，如下图：

![image](https://note.youdao.com/yws/api/personal/file/CB5A48AF2C5747EE82AB186735DBDD48?method=download&shareKey=d7f717379056b5e3e0932a2810a144c6)



**添加应用商店**

在系统管理-系统设置-中点添加应用商店

名称：wisecloud

地址：git@git.svicloud.com:svicloud/catalog-wisecloud.git 

分支：master


应用商店就会出来wisecloud：

![image](https://note.youdao.com/yws/api/personal/file/0127C2072B854988A5508E0B14DB625F?method=download&shareKey=b0a89c43b60073d3df2aae805a7a29fb)


在sever端

root@192-168-10-230:~# ssh-keygen 

将秘钥拷到目录/root/.ssh下

root@192-168-10-230:~# cd .ssh

root@192-168-10-230:~/.ssh# ls

id_rsa  id_rsa.pub  known_hosts

root@192-168-10-230:~/.ssh# rm -rf 

root@192-168-10-230:~/.ssh# 

建立云平台与git应用商店的互信

![image](https://note.youdao.com/yws/api/personal/file/431BFCB09E7D4769886E3A5650069969?method=download&shareKey=e0e32bd3f83d71b51d7376488c416520)

root@59af88b246de:~/.ssh# chmod 600 id_rsa 

![image](https://note.youdao.com/yws/api/personal/file/2057107302574D70A8B981DCE11E1CA7?method=download&shareKey=a0fbd48e3b9c10c7d09ebf672b448a01)

**添加主机**

基础架构-主机-添加主机

点击页面中的第5步右边的复制按钮：


Xshell登录主机，在每台主机中执行拷贝的语句

应用-基础设施，（此时基础设施状态为正常active）：

**添加标签**

每台主机上点编辑-添加标签（参考如下）：

1：vslb=true nfs=true

2：authcenter=true edge=true vslb=true fastdfs=true pg2=true pg1=true pg3=true

3：edge=true web=true fixed=true pg4=true pg6=true pg5=true

添加主机后，基础设施中healthcheck等启动异常，需删除以前环境的残留数据（对切换了环境的情况下）

```bash
docker stop $(docker ps |awk '{print $1}')

docker rm $(docker ps -a |awk '{print $1}')
```

![image](https://note.youdao.com/yws/api/personal/file/FE64D72163F0437381B90B5DC95E4C8B?method=download&shareKey=0c4537f237049b562a8b3751a290cb1c)

添加成功后：

![image](https://note.youdao.com/yws/api/personal/file/F29EC923B75742D7AA14B2FF62B75FFD?method=download&shareKey=75f56cc0cafd7c67cd98b533f6037b60)


**添加数据库**

首先添加数据库pg和redis：

应用-用户-从应用商店添加 ，搜postgres或redis，

![image](https://note.youdao.com/yws/api/personal/file/181A0C72FB9C4F298D8404F603D431A0?method=download&shareKey=af218aaf6875472582625657f18ace2d)


点查看详情，启动

启动后自动在/data/pgdata目录下生成pg*的文件夹，（*为1-6）

安装成功pg和redis后：

![image](https://note.youdao.com/yws/api/personal/file/DBE316AF1B40485DAEB1677C1F5E00E8?method=download&shareKey=54f23454ff7f756b9bbcd5d18fd2dab8)

**添加应用**

应用商店-wisecloud，选中aaa点查看详情--启动

安装完成后，查看所在的机器ip，然后在该机器查看images：

执行命令docker images

![image](https://note.youdao.com/yws/api/personal/file/55A46F8B29A743AA8865D8FBFB140C8A?method=download&shareKey=046950b0bce70cdd60c40036f7e020da)

查看添加的应用aaa：

![image](https://note.youdao.com/yws/api/personal/file/0BC5C3B58C1D4A93891CF8A425BF7872?method=download&shareKey=0509b6fbf6668b3b73932ef64e846d19)


