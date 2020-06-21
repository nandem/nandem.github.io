---
layout: post
title: "Deepin"
categories:
  - Linux
  - Deepin
tags:
  - linux
  - deepin
---

# 网络问题
## A start job is running for wait for network to be Configured
打开终端编辑 ```/etc/systemd/system/network-online.target.wants/systemd-networkd-wait-online.service``` 在 [Service] 下增加超时设置
```bash
...

[Service]
...
TimeoutStartSec=2sec # 增加这行，这里设置成 2s 可以根据自己需要设置

...
```
