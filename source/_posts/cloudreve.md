---
title: 宝塔搭建 cloudreve 并配置 Aria2
categories: 教程
tags: cloudreve
abbrlink: 2241284019
date: 2022-10-02 04:27:17
cover:
---
# 搭建网站
新建网站，创建 mysql 数据库，php 设为静态，部署 ssl 证书
保存 mysql 账密备用
# 部署 cloudreve
前往 [github release](https://github.com/cloudreve/Cloudreve/releases/latest) 获取最新版的 cloudreve
在根目录新建文件夹 `cloudreve`，设置权限为 `755`，所有者设置为 `www`，上传压缩包并解压
运行 cloudreve
```powershell
cd /cloudreve
chmod +x ./cloudreve && ./cloudreve
```
这时候会出现初始管理员账号和密码，记得保存
编辑 `conf.ini` 文件，在末尾添加
```
[Database]
Type = mysql
; MySQL 端口
Port = 3306
; 
User = 第一创建数据库的用户名
; 
Password = 第一创建数据库的密码
; 
Host = 127.0.0.1
; 
Name = 数据库名称
```
# 设置进程守护
进入软件商店安装`进程守护管理器`并添加守护进程，名称随意（只支持英文），启动用户选`www`，运行目录填`/cloudreve/`，启动命令填`/cloudreve/cloudreve`
# 反代

# 配置 Aria2

>参考文档 https://docs.cloudreve.org/
https://cloud.tencent.com/developer/article/1935056
https://cloud.tencent.com/developer/article/1937575