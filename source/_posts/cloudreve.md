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
找到第一步添加的网站 点击设置 找到反向代理 添加反向代理。名字随意 目标url填`http://127.0.0.1:5212`，其他设置默认。
# 配置 Aria2
在安全中放行`6800`端口
## 安装 Aria2
安装 Aria2 管理脚本
项目地址：https://github.com/P3TERX/aria2.sh
```powershell
#请以root用户运行
wget -N git.io/aria2.sh && chmod +x aria2.sh
```
运行脚本
```powershell
./aria2.sh
```
运行后：
```
[root@www ~]# ./aria2.sh

 Aria2 一键安装管理脚本 增强版 [v2.7.0] by P3TERX.COM
 
  0. 升级脚本
 ———————————————————————
  1. 安装 Aria2
  2. 更新 Aria2
  3. 卸载 Aria2
 ———————————————————————
  4. 启动 Aria2
  5. 停止 Aria2
  6. 重启 Aria2
 ———————————————————————
  7. 修改 配置
  8. 查看 配置
  9. 查看 日志
 10. 清空 日志
 ———————————————————————
 11. 手动更新 BT-Tracker
 12. 自动更新 BT-Tracker
 ———————————————————————
```
输入 1 安装 Aria2，安装完成后显示配置信息：
```
Aria2 简单配置信息：

 IPv4 地址      : 124.70.**.**
 IPv6 地址      : ********（失败则不需要）
 RPC 端口       : 6800
 RPC 密钥       : 7d0bb173a2a101******
 下载目录       : /root/downloads
 AriaNg 链接    : http://ariang.js.org/****
```
## 对接 cloudreve
打开管理面板-参数设置-离线下载，把配置依次填入，具体看图
![](/img/cloudreve.png)
配置完成后先保存，再测试连接，测试成功即可用。
>参考文档 https://docs.cloudreve.org/
https://cloud.tencent.com/developer/article/1935056
https://cloud.tencent.com/developer/article/1937575