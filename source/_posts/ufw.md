---
title: UFW 防火墙
categories: 教程
tags: 
  - UFW
  - Linux
  - 安全
abbrlink: 1354586903
date: 2022-10-28 22:20:53
cover: /img/ufw_bg.webp
---
# 安装 UFW
Centos
```powershell
yum update && yum install ufw
```
Ubuntu/Debian
```powershell
apt-get update && apt-get install ufw
```
# 查看状态
```powershell
ufw status
```
`active`已激活
`inactive`：未激活
# 启用 / 禁用
```powershell
ufw enable      #启用
ufw disable     #禁用
```
# 使用与配置
## 列出当前规则
```powershell
ufw status
ufw status verbose    #详细规则
```
## 添加规则
### 允许入站
默认情况，没有允许就是拒绝（入站），使用 `ufw allow <端口>` 来添加允许访问的端口或协议。
```powershell
ufw allow ssh             #添加22端口

ufw allow http            #添加80端口

ufw allow https           #添加443端口

ufw allow 2333/tcp        #添加2333端口，仅TCP协议

ufw allow 6666/udp        #添加6666端口，仅UDP协议

ufw allow 8888:9999       #添加8888到9999之间的端口
```
### 拒绝入站
使用 `ufw deny <端口>` 来添加拒绝入站的端和协议，与添加允许的类似。
## 删除规则
先使用 `ufw status` 查看规则，再使用 ufw delete [规则] <端口> 来删除规则。
```powershell
ufw delete allow 2333/tcp
```
如果你有很多条规则，使用 `ufw status numbered` 参数，可以在每条规则上加个序号数字。
然后使用 `ufw delete <序号>` 来删除规则。
```powershell
root@simple:~# ufw status numbered  #列出规则，并加上序号。
Status: active

     To                         Action      From
     --                         ------      ----
[ 1] 20,21,22,80,888,8888/tcp   ALLOW IN    Anywhere
[ 2] 39000:40000/tcp            ALLOW IN    Anywhere
[ 3] 8896/tcp                   ALLOW IN    Anywhere
[ 4] 8896/udp                   ALLOW IN    Anywhere
[ 5] 443/tcp                    ALLOW IN    Anywhere
[ 6] 20,21,22,80,888,8888/tcp (v6) ALLOW IN    Anywhere (v6)
[ 7] 39000:40000/tcp (v6)       ALLOW IN    Anywhere (v6)
[ 8] 8896/tcp (v6)              ALLOW IN    Anywhere (v6)
[ 9] 8896/udp (v6)              ALLOW IN    Anywhere (v6)
[10] 443/tcp (v6)               ALLOW IN    Anywhere (v6)

root@p3terx:~# ufw delete 4  #删除上面的第4条规则
Deleting:
 allow 8896/udp
Proceed with operation (y|n)? y  #最后会询问你是否进行操作
```
# 常用命令速查表
```powershell
enable                        #启用防火墙
disable                       #禁用防火墙
allow <port>                  #添加允许规则
deny [rule] <port>            #添加拒绝规则
delete [rule] <port>          #删除规则
status                        #查看防火墙状态
status numbered               #将防火墙状态显示为带编号的规则列表
status verbose                #显示详细的防火墙状态
reload                        #重启防火墙
reset                         #重置防火墙
version                       #显示版本信息
```
>转载自
https://p3terx.com/archives/installing-and-configuring-ufw-in-debian.html