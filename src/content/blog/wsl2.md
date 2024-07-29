---
author: huala
pubDatetime: 2022-09-23T15:22:00Z
modDatetime: 2023-12-21T09:12:47.400Z
title: 如何更好的使用 WSL2
slug: how-to-better-use-wsl2
featured: true
draft: false
tags:
  - WSL2
description: 如何更好的使用 WSL2
---

## 切换到 D 盘

**关闭 wsl**
```
wsl --shutdown
```
**查看状态**

查看wsl下的Linux是否为关闭状态，当wsl为Stopped才能进行下一步。

```
wsl -l -v
_________________________________
NAME      STATE           VERSION
* Debian    Stopped         2
```

**导出镜像**
以压缩包的形式导出到其他盘。

```
wsl --export Debian D:\linux\Debian.tar
```

**注销原有的linux系统**

```
wsl --unregister Debian
```

**查看系统状态**
查看是否真的注销成功。

```
wsl -l -v
```

**导入系统**

> wsl --import <导入的Linux名称> <导入盘的路径> <ubuntu.tar的路径> --version 2 (代表wsl2)

```
wsl --import Debian D:\linux\ D:\linux\Debian.tar --version 2

```

**修改默认用户**

如果不修改这时候启动 WSL，发现好像已经恢复正常了，但是用户变成了 root，之前使用过的文件也看不见了。

```
Debian config --default-user coder
```

在导入任意盘linux系统时，我起名 Debian，所以这里是 Debian；如果你起的名字是 Debian-20.04，那这里就是 Debian2004；如果你起的名字是Debian-18.04，那这里就是Debian1804。

**启动 Debian**

```
wsl -d  Debian
```
