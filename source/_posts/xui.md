---
title: x-ui 面板 VMESS/VLESS+WS+TLS+CDN 节点搭建
cover: /img/xui_bg.webp
top_img: false
abbrlink: 3967340161
date: 2022-09-07 17:53:34
categories: 教程
tags: 
  - x-ui
---
## 准备
- VPS 一台
- 域名一个
- Cloudflare 账号一个
### 安装 x-ui
参考官方文档 https://github.com/vaxilu/x-ui
### 解析域名
进入 [Cloudflare](https://dash.cloudflare.com)，选择你的域名 -> DNS -> 添加记录
![](/img/xui.webp)
记得打开代理
### 申请证书
可以使用脚本或宝塔面板申请证书，这里使用的是 cf 的免费证书
进入 [Cloudflare](https://dash.cloudflare.com)，选择你的域名 -> SSL -> 源服务器 -> 创建证书
![](/img/xui1.webp)
复制源证书和私钥备用
## 搭建节点
1. 进入 x-ui 面板新建节点
2. 协议选 VMESS 或 VLESS （建议VLESS）
3. 端口填 cf 支持的端口
4. 传输选 WS
5. 新建一个请求头，值填前面解析的域名
6. 打开 tls，域名同上，公钥填源证书，密钥填私钥
```
cf 支持的端口：
443     #不建议使用
2053
2083
2087
2096
8443
```
![](/img/xui2.webp)
`查看 -> 复制链接` 导出节点