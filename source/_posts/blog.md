---
title: 使用 Github webhook 配合宝塔 webhook 自动部署 hexo 博客
date: 2022-08-27 21:47:11
cover: /img/blog_bg.webp
categories:
  - 教程
tags:
  - Github
  - Hexo
abbrlink: 1090495405
---
## 安装 Git
**Centos/RedHat:**
```powershell
yum install curl-devel expat-devel gettext-devel  openssl-devel zlib-devel
yum -y install git-core
git --version
```
**Debian/Ubuntu:**
```powershell
apt-get install libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev
apt-get install git
git --version
```

## 配置SHH密钥
检查SSH-KEY是否已经生成过
```powershell
ls -al ~/.ssh
```
生成新的SSH-KEY
```powershell
ssh-keygen -t rsa -C "example@example.com"
```
把``example@example.com``替换为你自己的邮箱
查看生成成功的KEY
```powershell
cat /root/.ssh/id_rsa.pub
```
将``id_rsa.pub``的内容添加到Github
Setting -> SSH and GPC keys -> New SSH key
![](/img/blog.webp)
## 配置宝塔面板 webhook
宝塔面板安装``宝塔Webhook``
添加Webhook
```
cd /www/wwwroot/username.github.io; # 可替换为其他目录
git pull;
```
注意``username.github.io``要改为你的仓库名
点击查看秘钥，蓝色选中的部分就是宝塔面板提供的 webhook url ，当链接被访问时，就会执行我们上一步配置的命令，自动 git pull 了。
![获取WebHook url](/img/blog1.webp)
## 配置Github Webhooks
进入仓库 -> Settings -> Webhooks -> Add webhook
将宝塔提供的 webhook url 填入 Payload URL，并将下方的 Content type 修改为 application/json
## 宝塔面板创建网站
网站根目录为[上文](https://blog.laozheng.cf/posts/1090495405/#:~:text=New%20SSH%20key-,%E9%85%8D%E7%BD%AE%E5%AE%9D%E5%A1%94%E9%9D%A2%E6%9D%BF%20webhook,-%E5%AE%9D%E5%A1%94%E9%9D%A2%E6%9D%BF%E5%AE%89%E8%A3%85)创建的目录，其他默认就行
>参考来源：
>https://segmentfault.com/a/1190000013450267
>https://sugarless.cn/posts/how-to-use-github-webhook-and-btpanel-webhook.html