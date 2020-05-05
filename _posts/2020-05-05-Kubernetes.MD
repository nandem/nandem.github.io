---
layout: post
title: "Kubernets"
categories:
  - Kubernets
tags:
  - kubernets
  - k8s
  - 云计算
---

# 常用命令
|功能|命令|说明|
|:---:|:---|:---:|
|查看日志|```kubectl logs -f <pod_name> -c <container_name>```|```-f```: 类似于tail -f|

# 系统命令
|功能|命令|说明|
|:---:|:---|:---:|
|查看当前配置|```kubectl config view```|无|
|新增上下文|```kubectl config set-context <context_name> --namespace=<namespace_in_context> --cluster=<cluster_name> --user=<user_name>```|无|
|删除上下文|```kubectl config delete-context <context_name>```|无|
|切换上下文|```kubectl config use-context <context_name>```|```<context_name>```: 上下文名称|
|查看当前生效的上下文|```kubectl config current-context```|无|
|修改默认命名空间|```kubectl config set-context --current --namespace=<namespace_name>```|```--current```: 设置当前上下文默认命名空间，换成其他上下文名称同理|

# 发行版
## k3s
### 安装
官网已提供完整的安装说明，支持在线和离线方式。<br>
[国内](https://docs.rancher.cn/k3s/) | [普通](https://rancher.com/docs/k3s/latest/en/quick-start/)

### 注意事项
- 安装时指定```export INSTALL_K3S_EXEC="--write-kubeconfig ~/.kube/config --write-kubeconfig-mode 666"```以修改默认配置文件位置和文件访问权限
