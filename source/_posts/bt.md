---
title: 宝塔面板跳过强制绑定账户
date: 2022-08-20 01:51:22
author: 
cover: http://img.xjh.me/random_img.php?ctype=acg&return=302
categories: # 分类
- 教程
- 宝塔面板
copyright: false
---

{% note blue no-icon %}
**转载增改自https://www.xiaoyao01.com/bsma780tgqzadzh/**
{% endnote %}
## 一、安装原版宝塔
首先安装宝塔面板的官方版本：bt.cn
## 二、安装依赖
**wget**
Ubuntu\Debian
```powershell
apt-get install wget
```
CentOS
```powershell
yum install -y wget
```
**unzip**
Ubuntu\Debian
```powershell
apt-get install unzip
```
CentOS
```powershell
yum install -y unzip
```
## 三、安装更新
在root目录下安装
7.4.3版本，此版本不需要账户登录
```powershell
wget https://github.com/wei/baota/releases/download/7.4.3/LinuxPanel-7.4.3.zip
```
7.70版本，此版本强制登录需要用代码更改
```powershell
wget https://github.com/wei/baota/releases/download/7.7.0/LinuxPanel-7.7.0.zip
```
关闭强制登录代码
```powershell
echo "{\"uid\":1000,\"username\":\"admin\",\"serverid\":1}" > /www/server/panel/data/userInfo.json
```
解压文件
```powershell
unzip LinuxPanel-*
```
切换到升级包目录
```powershell
cd panel
```
执行升级脚本
```powershell
bash update.sh
```
删除升级包
```powershell
cd .. && rm -f LinuxPanel-*.zip && rm -rf panel
```
为了更安全，你可以执行以下内容，避免一些问题~~
```powershell
echo '127.0.0.1 bt.cn' >>/etc/hosts
```