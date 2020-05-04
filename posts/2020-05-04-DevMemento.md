# NodeJS
### nrm
管理registry地址小工具
```
npm install -g nrm //全局安装
nrm add 镜像名称 镜像地址 //添加镜像
nrm ls //查看镜像列表
nrm use 镜像名称 //切换镜像
```

## npm run serve错误集合
### System limit for number of file watchers reached
方案
```bash
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p 
sudo sysctl --system
```


# Kotlin与Java混编
## maven compile失败
1. 执行```mvn clean kotlin:compile package -Dmaven.test.skip=true```。
2. 继续执行mvn compile
