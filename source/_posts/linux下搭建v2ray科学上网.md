---
title: linux下搭建v2ray科学上网
date: 2020-10-01 08:10:41
tags: 工作
---
# 说明
寒假配置了一台manjaro，但是由于同性交友网站GitHub经常进不去，包括wget一些代码时速度很慢，为了更加方便地上网，特地配置v2ray。

# wget v2ray和Qv2ray
```
# v2ray
wget https://github.com/v2ray/v2ray-core/releases/download/v4.27.0/v2ray-linux-64.zip

# Qv2ray
wget https://github.com/Qv2ray/Qv2ray/releases/download/v2.6.3/Qv2ray.v2.6.3.linux-x64.AppImage
```
# 解压v2ray
```
unzip v2ray-linux-64.zip
```

# 添加运行权限然后运行v2ray
```
chmod +x Qv2ray.v2.6.3.linux-x64.AppImage
./Qv2ray.v2.6.3.linux-x64.AppImage
```

# 配置文件路径
进入首选项-内核设置配置可执行文件路径和资源目录
![配置文件路径](https://i.loli.net/2020/10/05/6gCNOSQliraeWZc.png "配置文件路径")

# 添加订阅链接
![添加订阅链接](https://i.loli.net/2020/10/05/xDPkfcaJHMqNbpX.png "添加订阅链接")

# error!
出现如下错误修改系统时间即可
![出现错误](https://i.loli.net/2020/10/05/ahq6mUrJtoO9STI.png "error")
```
sudo date -s "20201001 08:23:00" #yyyymmdd hh:mm:ss
```
![修改系统时间](https://i.loli.net/2020/10/05/erMwj7OFfiVqKJ2.png "修改系统时间")

# alias 添加快速启动命令
```
alias vpn /home/wlz/qv2ray/Qv2ray.v2.6.3.linux-x64.AppImage
funcsave vpn
```
![配置启动命令](https://i.loli.net/2020/10/05/UqTzSOwx7QarGAg.png "配置启动命令")
