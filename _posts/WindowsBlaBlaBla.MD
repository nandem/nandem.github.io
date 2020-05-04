# 无法安装
- 修复计算机=>命令行
- 输入`diskpart`进入diskpart模式
- 输入`list disk`，眼睛亮一点，确定哪个是你的硬盘
- 输入`select disk 编号`选择你的硬盘
- 输入`clean`清除硬盘
- 输入`convert gpt`转成gpt格式
- 退出重启，应该就可以了
> diskpart用处很多，比如格式化硬盘和U盘等。最zhuangbility的就是通过它来分区，而不是使用各种分区软件

# 安装CLion
- 下载安装Clion
- 下载Mingw-64 installer
- 配置

# NodeJS无法安装依赖
## 可能原因：
- 权限
- cnpm的问题，换成npm
