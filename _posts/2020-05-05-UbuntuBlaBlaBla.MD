---
layout: post
title: "Ubuntu"
categories:
  - Ubuntu
tags:
  - ubuntu
  - linux
---

# 查看系统架构
```bash
uname -a #几乎所有 Linux/Unix 系统
dpkg --print-architecture #只适用于基于 Debian 和 Ubuntu 的 Linux 发行版
```

# 启动图形界面以便设置软件源
``` bash
sudo update-manager -c -d
```

# shadowsocks配置
1. 下载github上的[ShadowSocks](https://github.com/shadowsocks/shadowsocks-qt5)，格式为APPImage，右键->properties->permissions->Allow executing file as program，双击即可运行。
2. 设置系统代理为Manual，Socks Host为127.0.0.1:1080（1080为ss中设置的本地端口号），其余默认。
3. 重启生效。

# 查看系统架构类型
```bash
uname -a #几乎所有 Linux/Unix 系统适用
dpkg --print-architecture #只适用于基于 Debian 和 Ubuntu 的 Linux 发行版
```

# 中文输入法
1. Ctrl + Alt + T打开终端，输入fcitx检查是否安装fcitx，若没有则根据提示进行安装，否则进行2。
2. 系统设置->Region & Language->Manage Installed Languages->Keyboard input method system->fcitx。
3. （可选）此时重启系统发现已经有默认的中文输入法。但想要安装sougou的话需要去官网下载安装包并双击安装，之后点击小键盘选择搜狗输入法。

# 命令行安装oracle-jdk
``` bash
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
```

# 命令行安装IntelliJ IDEA
#### 安装 INTELLIJ IDEA COMMUNITY版本：
``` bash
sudo snap install intellij-idea-community --classic --edge
```
#### 安装INTELLIJ IDEA ULTIMATE版本：
``` bash
sudo snap install intellij-idea-ultimate --classic --edge
```

# 安装Android Studio
下载[Android Studio](https://developer.android.google.cn/studio/)
移动到软件文件夹
```bash
sudo mv android-studio-ide-xxx.xxxxxxx-xxx.zip /opt
```
解压
```bash
sudo unzip android-studio-ide-xxx.xxxxxxx-xxx.zip
```

# 安装CLion
#### 先导工作
```bash
sudo apt-get update
sudo apt-get install g++ ##安装g++编译器
sudo apt-get install make ##make工具
sudo apt-get install cmake ##安装cmake工具

sudo apt-get install bison 
sudo apt-get install libncurses5-dev
sudo apt-get install kdelibs5-dev
```
下载[CLion](https://www.jetbrains.com/clion/download/)。
移动到自己的软件文件夹
```bash
sudo mv Clion-xxxx.x.tar.gz /opt
```
进入软件文件夹并解压
```bash
cd /opt
sudo tar -zxvf CLion-xxxx.x.tar.gz  
```
启动
```bash
cd clion-xxxx.x/bin/  
./clion.sh  
```
选择cmake路径，ok！

# JetBrains系列IDE破解
```bash
sudo vim /etc/hosts
```
加入“0.0.0.0 account.jetbrains.com”
保存（若忘了sudo打开导致权限不足又不想sudo重新打开，使用“**:w !sudo tee %**”，注意空格）
百度搜Idea注册码，复制粘贴即可。

# 安装Node.js
1. 下载[Node.js](https://nodejs.org/en/)
2. 移动到自己的软件文件夹，如`sudo mv node-vx.xx.x-linex-64.tar.xz`
3. 解压`sudo tar -xJf node-vx.xx.x-linex-64.tar.xz`
4. 安装npm和node命令到系统命令
``` bash
sudo ln -s /opt/node-vx.xx.x-linex-64/bin/node /usr/local/bin/node #node命令
sudo ln -s /opt/node-vx.xx.x-linex-64/bin/npm /usr/local/bin/npm #npm命令
```
验证是否安装成功，分别输入`node -v`和`npm -v`
#### 设置淘宝镜像
终端输入`npm install -g cnpm --registry=https://registry.npm.taobao.org`

#### 安装nvm
``` bash
wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash

source ~/.bashrc
```

# 安装Gradle
#### 使用package manager（这里选择SDKMAN!）
- 打开终端输入`$ curl -s "https://get.sdkman.io" | bash`
- 输入`sdk version`查看是否成功
- 重新打开终端输入`sdk install gradle x.x`即可
> 有多种安装方式，我这里选择我认为比较简洁和舒服的方式，肯定不唯一

# 安装Postman
``` shell
wget https://dl.pstmn.io/download/latest/linux64 -O postman.tar.gz #命令行下载最新版postman
sudo mv postman.tar.gz /opt #移动至软件文件夹
sudo tar -xzf postman.tar.gz #解压
sudo ln -s /opt/Postman/Postman /usr/bin/postman #加入环境变量
```
> 这里不制作启动项了，直接通过终端输入`postman`即可启动

# 安装MongoDB
#### 安装
```shell
sudo apt update #更新源
sudo apt install -y mongodb #ubuntu仓库里有最新稳定版MongoDB，所以可以直接命令行安装
```
#### 管理
```shell
sudo systemctl status mongodb #查看mogodb状态
sudo systemctl stop mongodb #停止服务
sudo systemctl start mongodb #启动服务
sudo systemctl restart mongodb #重启服务
sudo systemctl disable mongodb #禁止自动启动
sudo systemctl enable mongodb #启用自动启动
```
> systemctl 为Systemd命令，Systemd 是 Linux 系统工具，用来启动守护进程，已成为大多数发行版的标准配置。参考[这篇教程](http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-commands.html)
和[这篇文章](https://huur.cn/course/yw/1712.html)

#### 基本操作
##### 添加管理员账户
``` shell
use admin #进入admin数据库

db.createUser(
  {
    user: "root",
    pwd: "root2333",
    roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
  }
)
```
*role说明*:
- read：允许用户读取指定数据库
- readWrite：允许用户读写指定数据库
- dbAdmin：允许用户在指定数据库中执行管理函数，如索引创建、删除，查看统计或访问system.profile
- userAdmin：允许用户向system.users集合写入，可以找指定数据库里创建、删除和管理用户
- clusterAdmin：只在admin数据库中可用，赋予用户所有分片和复制集相关函数的管理权限。
- readAnyDatabase：只在admin数据库中可用，赋予用户所有数据库的读权限
- readWriteAnyDatabase：只在admin数据库中可用，赋予用户所有数据库的读写权限
- userAdminAnyDatabase：只在admin数据库中可用，赋予用户所有数据库的userAdmin权限
- dbAdminAnyDatabase：只在admin数据库中可用，赋予用户所有数据库的dbAdmin权限。
- root：只在admin数据库中可用。超级账号，超级权限

##### 修改用户密码
``` shell
db.changeUserPassword('tank2','test');
```
##### 创建或者使用数据库
``` shell
use test #有test数据库则切换至test，否则创建并切换至test
```
