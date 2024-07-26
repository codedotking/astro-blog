---
author: huala
pubDatetime: 2022-09-23T15:22:00Z
modDatetime: 2023-12-21T09:12:47.400Z
title: Rust windows 最小化安装
slug: rust-windows-zui-xian-an-zhuang
featured: true
draft: false
tags:
  - rust
  - 学习
description: Rust windows 最小化安装
---

## 本文是最简最快最小化安装

### 安装 C++环境

rust 底层是依赖 C 环境的连接器，所以需要先安装 C/C++编译环境, [点击下载 64 位](https://github.com/niXman/mingw-builds-binaries/releases/tag/13.2.0-rt_v11-rev1) mingw-builds-binaries
下载后解压到任意盘根目录，然后把文件夹的 bin 目录路径配置到系统环境变量 path。
比如：C:\mingw64\bin
验证配置是否成功

```shell
gcc -v
```

### 安装 Rust

如果不想默认安装到 C 盘，安装之前要先设置一些系统环境变量，改变默认安装的位置。
比如全部安装到 D 盘的 rust 文件夹下。
bash 代码解读复制代码

```shell
RUSTUP_HOME D:\rust\.rustup // 默认路径 ~/.rustup 或 %USERPROFILE%/.rustup
CARGO_HOME D:\rust\.cargo // 默认路径 ~/.cargo 或 %USERPROFILE%/.cargo
```

如果默认从官网安装，下载很慢且容易失败，推荐使用镜像加速安装，先设置以下环境变量：
arduino 代码解读复制代码

```shell
RUSTUP_DIST_SERVER https://rsproxy.cn
RUSTUP_UPDATE_ROOT https://rsproxy.cn/rustup
```
[点击下载](https://static.rust-lang.org/rustup/dist/x86_64-pc-windows-msvc/rustup-init.exe) rustup-init.exe

做好以上准备工作之后，就可以用 rustup-init.exe 安装了
总体安装步骤中有三次需要输入数字选项，总结下来就是：3，2，1

运行 rustup-init.exe 后出现如下提示：
```rust
Rust Visual C++ prerequisites

Rust requires a linker and Windows API libraries but they don't seem to be
available.

These components can be acquired through a Visual Studio installer.

1. Quick install via the Visual Studio Community installer
   (free for individuals, academic uses, and open source).

2. Manually install the prerequisites
   (for enterprise and advanced users).

3. Don't install the prerequisites
   (if you're targeting the GNU ABI).
> 3

```

输入 3 回车：

```rust
1) Proceed with standard installation (default - just press enter) 
2) Customize installation 
3) Cancel installation
> 2
```
输入 2 回车：

```rust
I'm going to ask you the value of each of these installation options.
You may simply press the Enter key to leave unchanged.

Default host triple? [x86_64-pc-windows-msvc]
x86_64-pc-windows-gnu
```

这里默认是 `x86_64-pc-windows-msvc`，也就是需要安装 VS 的 msvc 那一堆。这里我们使用自己单独下载配置好的编译环境。
输入 `x86_64-pc-windows-gnu`，（小提示，先复制 `x86_64-pc-windows-gnu`，然后命令行上鼠标右键就自动粘贴上去了，可以不用手写输入。
出现提示：

```sql
Default toolchain? (stable/beta/nightly/none) [stable]
```

直接回车，默认选择是稳定版。
出现提示：

```sql
Profile (which tools and data to install)? (minimal/default/complete) [default]
```

直接回车，默认选择默认。
出现提示：

```bash
Modify PATH variable? (Y/n)
y
```

输入 Y 回车（不分大小写），表示修改环境变量。
出现提示：

```sql
Current installation options:

default host triple: x86_64-pc-windows-gnu
default toolchain: stable
profile: default
modify PATH variable: yes

1. Proceed with selected options (default - just press enter)
2. Customize installation
3. Cancel installation
   > 1
```

输入 1 回车，然后开始安装并打印相关信息：

```vbnet
info: profile set to 'default'
info: setting default host triple to x86_64-pc-windows-gnu
info: syncing channel updates for 'stable-x86_64-pc-windows-gnu'
info: latest update on 2022-12-15, rust version 1.66.0 (69f9c33d7 2022-12-12)
info: downloading component 'cargo'
7.3 MiB / 7.3 MiB (100 %) 1.9 MiB/s in 5s ETA: 0s
info: downloading component 'clippy'
3.6 MiB / 3.6 MiB (100 %) 1.7 MiB/s in 2s ETA: 0s
info: downloading component 'rust-docs'
19.0 MiB / 19.0 MiB (100 %) 2.1 MiB/s in 10s ETA: 0s
info: downloading component 'rust-mingw'
4.2 MiB / 4.2 MiB (100 %) 2.6 MiB/s in 1s ETA: 0s
info: downloading component 'rust-std'
27.8 MiB / 27.8 MiB (100 %) 1.8 MiB/s in 14s ETA: 0s
info: downloading component 'rustc'
74.3 MiB / 74.3 MiB (100 %) 1.5 MiB/s in 49s ETA: 0s
info: downloading component 'rustfmt'
6.6 MiB / 6.6 MiB (100 %) 2.2 MiB/s in 3s ETA: 0s
info: installing component 'cargo'
info: installing component 'clippy'
info: installing component 'rust-docs'
19.0 MiB / 19.0 MiB (100 %) 3.0 MiB/s in 5s ETA: 0s
info: installing component 'rust-mingw'
info: installing component 'rust-std'
27.8 MiB / 27.8 MiB (100 %) 9.0 MiB/s in 3s ETA: 0s
info: installing component 'rustc'
74.3 MiB / 74.3 MiB (100 %) 10.3 MiB/s in 7s ETA: 0s
info: installing component 'rustfmt'
info: default toolchain set to 'stable-x86_64-pc-windows-gnu'

stable-x86_64-pc-windows-gnu installed - rustc 1.66.0 (69f9c33d7 2022-12-12)

Rust is installed now. Great!

To get started you may need to restart your current shell.
This would reload its PATH environment variable to include
Cargo's bin directory (D:\Programs\rust\cargo_home\bin).

Press the Enter key to continue.
```

等待它下载文件完毕，这里需要等待的时间有点长，但耐心就好，假如下载出现错误，就重设上面的设定，再来一次流程。
当出现最后一行，敲回车，然后窗口自动关闭。
验证安装是否成功
打开命令提示符，也就是 cmd。
分别输入每一行命令后回车，出现相关信息后，说明 rust 安装成功了。

```sql
rustup -V
cargo -V
rustup show
```
