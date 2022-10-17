---
title: freenom 自动续期脚本
categories: 教程
tags: freenom
abbrlink: 116274935
date: 2022-09-27 23:55:38
cover: /img/freenom_bg.webp
---

***所有操作均在 Centos8 中进行，php 版本要求7.3以上***
## 源码部署
### 获取源码
创建文件夹
```powershell
mkdir -p /data/wwwroot/freenom && cd /data/wwwroot/freenom
```
clone 仓库源码
```powershell
git clone https://github.com/luolongfei/freenom.git ./
```
### 修改配置
复制配置文件模板
```powershell
cp .env.example .env
```
编辑配置文件
```powershell
vim .env
```
```
# 注意事项
# .env 文件里每个项目都有详细的说明，这里不再赘述，简言之，你需要把里面所有项都改成你自己的。需要注意的是多账户配置的格式：
# e.g. MULTIPLE_ACCOUNTS='<账户1>@<密码1>|<账户2>@<密码2>|<账户3>@<密码3>'
# （注意不要省略“<>”符号，否则无法正确匹配）
# 当然，若你只有单个账户，只配置 FREENOM_USERNAME 和 FREENOM_PASSWORD 就够了，单账户和多账户的配置会被合并在一起读取并去重。

# 编辑完成后，按“Esc”回到命令模式，输入“:wq”回车即保存并退出，不会用 vim 编辑器的可以谷歌一下:)
```
### 配置计划任务
如果安装了宝塔面板可以直接进面板设置计划任务
#### 安装 crontabs 以及 cronie
```powershell
yum -y install cronie crontabs
```
验证 crond 是否安装及启动
```powershell
yum list cronie && systemctl status crond
```
验证 crontabs 是否安装
```powershell
yum list crontabs $$ which crontab && crontab -l
```
#### 编辑任务表单
```powershell
crontab -e
```
```
# 任务内容如下
# 此任务的含义是在每天早上 9点 执行 /data/wwwroot/freenom/ 路径下的 run 文件，最佳实践是将这个时间修改为一个非整点的时间，防止与很多人在同一时间进行续期操作导致 freenom 无法稳定提供服务
# 注意：某些情况下，crontab 可能找不到你的 php 路径，下面的命令执行后会在 freenom_crontab.log 文件输出错误信息，你应该指定 php 路径：把下面的 php 替换为 /usr/local/php/bin/php （根据实际情况，执行 whereis php 即可看到 php 执行文件的真实路径）
00 09 * * * cd /data/wwwroot/freenom/ && php run > freenom_crontab.log 2>&1
```
#### 重启 crond 守护进程（每次编辑任务表单后都需此步，以便任务生效）
```powershell
systemctl restart crond
```
## 配置 telegram bot
1、将`.env`文件中的`TELEGRAM_BOT_ENABLE`的值改为`1`，即可启用 Telegram Bot 送信功能
2、在 Telegram 客户端中搜索 [@userinfobot](t.me/userinfobot)，并打开聊天窗口
3、发送`/start`给 [@userinfobot](t.me/userinfobot) 即可以获取自己的 Id，将`.env`文件中的`TELEGRAM_CHAT_ID`的值改为前面获取到的 Id
4、在 Telegram 客户端中搜索 [@BotFather](t.me/userinfobot)，并打开聊天窗口
5、发送`/newbot`给 [@BotFather](t.me/userinfobot)，然后根据提示创建，创建完成后根据图示操作获取`token`
![](/img/freenom.webp)
6、将`.env`文件中的`TELEGRAM_BOT_TOKEN`的值改为上一步获取的`token`值
7、在 Telegram 客户端中搜索你创建的机器人的账户，上面示例中机器人账户为@fat_tiger_bot，请替换为你自己的。找到机器人账户并打开聊天对话框，点击聊天输入框中的`/start`按钮或者直接给机器人发送`/start`，以启用机器人
8、（可选）为 Telegram Bot 设置代理。针对国内网络环境，可将`.env`文件中的`TELEGRAM_PROXY`的值改为代理值，具体参考`.env`文件中的注释
## 验证
你可以先将`.env`中的`NOTICE_FREQ`的值改为1（即每次执行都推送通知），然后执行
```powershell
cd /data/wwwroot/freenom/ && php run
```
不出意外的话，你将收到一封关于域名情况的消息。
## 更新脚本
cd 到安装目录直接拉取代码
```powershell
cd /data/wwwroot/freenom && git clone https://github.com/luolongfei/freenom.git ./
```
>仓库地址 https://github.com/luolongfei/freenom/
编辑自 https://github.com/luolongfei/freenom/wiki/%E7%9B%B4%E6%8E%A5%E6%8B%89%E5%8F%96%E6%BA%90%E7%A0%81%E9%83%A8%E7%BD%B2
https://github.com/luolongfei/freenom/wiki/Telegram-Bot