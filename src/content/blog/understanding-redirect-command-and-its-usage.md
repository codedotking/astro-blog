---
author: huala
pubDatetime: 2022-09-23T15:22:00Z
modDatetime: 2023-12-21T09:12:47.400Z
title: 深入解析命令行中的重定向符号
slug: understanding-redirect-command-and-its-usage
featured: true
draft: false
tags:
  - redirect
  - linux
  - 重定向符号
description: 深入解析命令行中的重定向符号 >, >>, < 2>, 2>&1 或者 &>
---

> 在 `Unix/Linux Shell` 命令行环境中，重定向符号是非常强大的工具，能够帮助用户灵活地管理命令的输入和输出。本文将深入解析常见的重定向符号及其用法。

### 四种重定向符号的用法


#### 1. 基本重定向符号

##### 标准输出重定向 (`>`)

使用 `>` 可以将命令的标准输出重定向到文件中。如果文件已存在，其内容将被覆盖。

**示例：**

```sh
echo "Hello, World!" > test.txt
```

##### 追加重定向 (`>>`)

使用 `>>` 可以将命令的标准输出追加到文件的末尾。如果文件不存在，将创建该文件。

```sh
echo "Hello, World!" >> test.txt
```

执行此命令后，文件 `test.txt` 将包含：

```sh
Hello, World!
Hello again!
```

#### 2. 输入重定向 (`<`)

输入重定向符号 `<` 用于将文件的内容作为命令的输入。

**示例：**

```sh
cat <  unsorted_list.txt
```

此命令会读取文件 ` unsorted_list.txt` 的内容，进行排序并输出结果。

#### 3. 错误重定向 (`2>`)

错误重定向符号 `2>` 用于将命令的标准错误输出重定向到文件。

**示例：**

```sh
ls non_existent_file 2> error.log
```

如果文件 non_existent_file 不存在，错误信息将被写入 `error.log` 文件。

#### 4. 同时重定向标准输出和标准错误 (`&>` 或 `2>&1`)

**`&>` 用法**

`&>` 符号用于将标准输出和标准错误同时重定向到文件，这个符号通常在 Bash 和一些其他现代 shell 中可用。

**示例：**

```sh
ls non_existent_file &> output.log
```

此命令将标准输出和错误输出都重定向到 `output.log` 文件。

**`2>&1` 用法**

`2>&1` 是另一种将标准错误重定向到标准输出的方法，几乎适用于所有 Unix/Linux shell，经常与标准输出重定向符号 `>` 一起使用。

**示例：**

```sh
command > output.log 2>&1
```

这条命令将标准输出重定向到 `output.log` 文件，并将标准错误重定向到标准输出，最终都写入 `output.log` 文件。

### 实用示例

假设你有一个长时间运行的 `Python` 脚本 `long_running_script.py`，你希望在后台运行它，并将所有输出记录到一个文件中。你可以使用以下命令：

```sh
nohup python3 long_running_script.py > output.log 2>&1 &
```

- nohup：确保即使终端关闭，脚本仍然继续运行。
- python3 long_running_script.py：执行 `Python` 脚本。
- `output.log`：将标准输出重定向到 `output.log` 文件。
- `2>&1`：将标准错误重定向到标准输出，使得所有输出都被写入 `output.log` 文件。
- `&`：将命令放到后台运行。

### 总结

> 重定向符号在命令行操作中提供了强大的功能，允许用户灵活地管理命令的输入和输出：

- `>`：将标准输出重定向到文件（覆盖）。
- `>>` ：将标准输出重定向到文件（追加）。
- `<`：将文件内容作为命令的输入。
- `2>`：将标准错误输出重定向到文件。
- `&>` 或 `2>&1`：将标准输出和标准错误同时重定向到文件。

这些符号在编写脚本、自动化任务和调试程序时尤其有用，可以大大提高工作效率。掌握这些重定向符号的用法，将使你在命令行环境中更加得心应手。
