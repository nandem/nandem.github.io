---
layout: post
title: "Linux Common"
categories:
  - Linux
tags:
  - 系统管理
  - linux
---

### 端口 相关
#### 端口占用
```
# 找出占用端口pid
sudo lsof -i:port
# 结束进程
sudo kill -9 pid
```

### 软件源
#### 管理
##### 正常做法
```
sudo vim /etc/apt/sources.list
```
网上找到一个数据源后，直接抄进去就行，不要有任何心理压力，到此为止就可以了。
下面的能看懂就继续看，看不懂就等摸索一段时间后再回来看，基本使用上面的方法就足够了。

##### 进阶做法
通过 sed 命令进行替换，这里以 ubuntu 18.04 举例。
```
# 我们可以看一下 ubuntu 的源是什么样的格式
cat /etc/apt/sources.list
```
输出如下: 
```
……
deb http://xxx.xxx.xxx/ubuntu bionic-security main
deb-src http://xxx.xxx.xxx/ubuntu bionic-security main
deb http://xxx.xxx.xxx/ubuntu bionic-security universe
deb-src http://xxx.xxx.xxx/ubuntu bionic-security universe
……
```
网上找一个镜像源如：aaa.bbb.ccc，执行 sed 替换
```
sudo sed -i 's/xxx\.xxx\.xxx/aaa\.bbb\.ccc/g' /etc/apt/sources.list
```
> 进行操作前最好将 /etc/apt/sources.list 进行备份
