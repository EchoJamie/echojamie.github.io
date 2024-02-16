---
title: centos安装蒲公英
donate: false
from: EchoJamie
url: 'https://echojamie.github.io/'
author: EchoJamie
about: "stay hungry, stay foolish.\U0001F98E"
avatar: /image/sidebar/avatar.jpg
comments: true
tags:
  - CentOS
categories:
  - - Linux
    - Network
sticky: 0
description: 贝锐蒲公英异地组网-CentOS部分
abbrlink: 3851b001
date: 2024-02-17 00:24:24
---


# 蒲公英组网 安装教程

## 安装

1. 通过wget蒲公英官网复制的下载网址，进行蒲公英Linux个人版客户端下载。
   下载命令如下：

   ```bash
   # 32位：
   wget https://pgy.oray.com/softwares/42/download/1838/PgyVisitor_CentOS_2.4.0.52291_i386.rpm
   # 64位：
   wget https://pgy.oray.com/softwares/42/download/1838/PgyVisitor_CentOS_2.4.0.52291_x86_64.rpm
   ```

2. 通过cd命令进入安装包所在的文件夹后，使用rpm命令进行软件安装。
   安装命令如下：

   ```bash
   # 32位：
   rpm -ivh PgyVisitor_CentOS_2.4.0.52291_i386.rpm
   # 64位：
   rpm -ivh PgyVisitor_CentOS_2.4.0.52291_x86_64.rpm
   ```

## 常用命令

```bash
# 基础命令
pgyvisitor
# 帮助
pgyvisitor -h
# 登陆
pgyvisitor login -h
pgyvisitor login
pgyvisitor login -u [UID]
pgyvisitor login -u [UID] -p [password]
pgyvisitor logout
pgyvisitor logininfo
# 自动登录
pgyvisitor autologin -h
pgyvisitor autologin -y
pgyvisitor autologin -n
# 旁路信息
pgyvisitor bypass
# 组网成员
pgyvisitor getmbrs -h
pgyvisitor getmbrs -m
pgyvisitor getmbrs -s [在线且有子设备的硬件成员序号]
pgyvisitor showsets
# 日志路径 /var/log/oray/pgyvpn
# 卸载
rpm -e PgyVPN
```
