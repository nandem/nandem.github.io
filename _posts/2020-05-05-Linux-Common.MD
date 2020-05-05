---
layout: post
title: "Linux Common"
categories:
  - Linux
tags:
  - 系统管理
  - linux
---

# 端口 相关
## 端口占用
```
# 找出占用端口pid
sudo lsof -i:port
# 结束进程
sudo kill -9 pid
```

# 软件源
## 管理
```
sudo vim /etc/apt/sources.list　　
```
