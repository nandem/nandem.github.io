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
通过 sed 命令进行替换，这里以 ubuntu 18.04.5 举例。
```
# 我们可以看一下 ubuntu 的源是什么样的格式
cat /etc/apt/sources.list
```
输出如下: 
```
#deb cdrom:[Ubuntu 18.04.5 LTS _Bionic Beaver_ - Release amd64 (20200806.1)]/ bionic main restricted

# See http://help.ubuntu.com/community/UpgradeNotes for how to upgrade to
# newer versions of the distribution.
deb http://cn.archive.ubuntu.com/ubuntu/ bionic main restricted
# deb-src http://cn.archive.ubuntu.com/ubuntu/ bionic main restricted

## Major bug fix updates produced after the final release of the
## distribution.
deb http://cn.archive.ubuntu.com/ubuntu/ bionic-updates main restricted
# deb-src http://cn.archive.ubuntu.com/ubuntu/ bionic-updates main restricted

## N.B. software from this repository is ENTIRELY UNSUPPORTED by the Ubuntu
## team. Also, please note that software in universe WILL NOT receive any
## review or updates from the Ubuntu security team.
deb http://cn.archive.ubuntu.com/ubuntu/ bionic universe
# deb-src http://cn.archive.ubuntu.com/ubuntu/ bionic universe
deb http://cn.archive.ubuntu.com/ubuntu/ bionic-updates universe
# deb-src http://cn.archive.ubuntu.com/ubuntu/ bionic-updates universe

## N.B. software from this repository is ENTIRELY UNSUPPORTED by the Ubuntu 
## team, and may not be under a free licence. Please satisfy yourself as to 
## your rights to use the software. Also, please note that software in 
## multiverse WILL NOT receive any review or updates from the Ubuntu
## security team.
deb http://cn.archive.ubuntu.com/ubuntu/ bionic multiverse
# deb-src http://cn.archive.ubuntu.com/ubuntu/ bionic multiverse
deb http://cn.archive.ubuntu.com/ubuntu/ bionic-updates multiverse
# deb-src http://cn.archive.ubuntu.com/ubuntu/ bionic-updates multiverse

## N.B. software from this repository may not have been tested as
## extensively as that contained in the main release, although it includes
## newer versions of some applications which may provide useful features.
## Also, please note that software in backports WILL NOT receive any review
## or updates from the Ubuntu security team.
deb http://cn.archive.ubuntu.com/ubuntu/ bionic-backports main restricted universe multiverse
# deb-src http://cn.archive.ubuntu.com/ubuntu/ bionic-backports main restricted universe multiverse

## Uncomment the following two lines to add software from Canonical's
## 'partner' repository.
## This software is not part of Ubuntu, but is offered by Canonical and the
## respective vendors as a service to Ubuntu users.
# deb http://archive.canonical.com/ubuntu bionic partner
# deb-src http://archive.canonical.com/ubuntu bionic partner

deb http://security.ubuntu.com/ubuntu bionic-security main restricted
# deb-src http://security.ubuntu.com/ubuntu bionic-security main restricted
deb http://security.ubuntu.com/ubuntu bionic-security universe
# deb-src http://security.ubuntu.com/ubuntu bionic-security universe
deb http://security.ubuntu.com/ubuntu bionic-security multiverse
# deb-src http://security.ubuntu.com/ubuntu bionic-security multiverse
```
网上找一个镜像源，如阿里源：mirrors.aliyun.com，执行 sed 替换
```
# 将所有 cn.archive.ubuntu.com（注意根据你的文件中的具体情况而定） 替换为 mirrors.aliyun.com
sudo sed -i 's/cn\.archive\.ubuntu\.com/mirrors\.aliyun\.com/g' /etc/apt/sources.list

# 将所有 security.ubuntu.com 替换为 mirrors.aliyun.com
sudo sed -i 's/security\.ubuntu\.com/mirrors\.aliyun\.com/g' /etc/apt/sources.list
```
> 进行操作前最好将 /etc/apt/sources.list 进行备份

#### 错误处理
- ```sudo apt update``` 报如下错误
```bash
E: Could not get lock /var/lib/apt/lists/lock. It is held by process 1532 (packagekitd)
N: Be aware that removing the lock file is not a solution and may break your system.
```
最好不要删除文件。执行以下命令大概率即可解决问题
```bash
sudo fuser -vki /var/lib/apt/lists/lock
```

### 故障处理
#### NIC Copper Link is Down
参考解决方案
- 执行网口点灯命令
```shell
ethtool -p 网卡名
```

### 阿里云
#### 云盘扩容
- 买云盘
- 挂在云盘
> 当前需要扩容来解决该问题，您参考如下流程，即可解决：
> 
> 一、首先是注意事项（阿里云云盘扩容因涉及到磁盘操作，所以存在数据安全风险，为保证您数据安全，需要您进行如下操作）：
> 
> 1.在扩容操作前请您务必在业务低峰期将系统中运行的服务和程序停止，停止数据写入
> 2.做好全量的数据备份，建议您在阿里云控制台制作实例的快照（系统盘和数据盘都需要制作快照），以保护您的数据安全。
> 制作快照参考：https://help.aliyun.com/document_detail/25455.html
> 
> 二、其次是开始进行扩容操作流程，登录服务器，执行下面的命令：
> 
> 1、apt-get update
> 2、apt-get install -y cloud-guest-utils
> 3、growpart /dev/vdb  1
> 4、resize2fs /dev/vdb1
> 
> 三、最后扩容文档中有任何不了解的，或者扩容命令执行后有报错的，您随时工单反馈，这边协助您一起分析解决，谢谢
