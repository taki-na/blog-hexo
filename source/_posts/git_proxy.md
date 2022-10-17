---
title: git 设置代理
abbrlink: 1229225829
date: 2022-10-17 21:07:33
categories: 教程
tags: git
cover: /img/git_proxy_bg.webp
top_img: false
---
```powershell
#使用http代理 
git config --global http.proxy http://127.0.0.1:1089
git config --global https.proxy https://127.0.0.1:1089
#使用socks5代理
git config --global http.proxy socks5://127.0.0.1:1088
git config --global https.proxy socks5://127.0.0.1:1088
```
端口换成代理监听的端口
>参考文档：https://tjfish.top/posts/git%E8%AE%BE%E7%BD%AE%E4%BB%A3%E7%90%86%E8%A7%A3%E5%86%B3%E8%A2%AB%E5%A2%99/