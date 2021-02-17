---
title: Windows10-下安装-Mit-scheme-流程-2021
date: 2021-02-17 21:46:53
tags: scheme
---

本文记录一下在2021年，windows 10系统如何通过 WSL(Windows Subsystem for Linux) 安装Mit-scheme。

安装前置条件：

* 安装WSL2 (Ubuntu发行版)
* 安装Visual Studio Code与它的Remote-WSL插件

### 1. 安装Mit-scheme
因为Mit-scheme的[官方页面][1]已经明确指出不再支持windows系统，

>We no longer support OS/2, DOS, or Windows, though it's possible that this software could be used on Windows Subsystem for Linux (we haven't tried).

所以我们采取在linux子系统中安装的手段。

打开安装好的 Ubuntu 子系统，_bash_ 内输入:
```sh
sudo apt-get update
sudo apt-get install mit-scheme
```

安装完成后，_bash_ 内输入`mit-scheme`可以打开 scheme 的 REPL (Read Eval Print Loop: Interactive Interpretor)。

```
MIT/GNU Scheme running under GNU/Linux
Type `^C' (control-C) followed by `H' to obtain information about interrupts.

Copyright (C) 2019 Massachusetts Institute of Technology
This is free software; see the source for copying conditions. There is NO warranty; not even for MERCHANTABILITY or
FITNESS FOR A PARTICULAR PURPOSE.

Image saved on Thursday September 5, 2019 at 11:51:46 AM
  Release 10.1.10 || Microcode 15.3 || Runtime 15.7 || SF 4.41 || LIAR/x86-64 4.118

1 ]=>
```
按 *ctrl + D* 可退出 REPL。

### 2. 优化 REPL 输入环境
此时安装好的 REPL 并没有自动补全与命令历史，使用体验比较差。StackOverflow上有人给出了安装 _readline wrapper (rlwrap)_ 工具的[解决方案][2]。
接下来通过安装 _rlwrap_ 工具对 *scheme* 的 REPL 进行功能补充。



先下载工具的配置文件 *mit_scheme_bindings.txt* 到HOME目录，*bash* 中输入：
```bash
cd ~
wget https://gist.githubusercontent.com/bobbyno/3325982/raw/fc0208d287e56adc12b4c76114fcd21a107082ad/mit_scheme_bindings.txt
```

备用防挂链接：{% asset_link mit_scheme_bindings.txt mit_scheme_bindings.txt %}

接着安装 *rlwrap* ：
```bash
sudo apt-get install rlwrap
```
安装完成后,编辑 *~/.bashrc* 文件 (之前最好安装 vscode 与 remote-wsl 插件)：
```bash
code ~/.bashrc
```
没装用 vscode 可以使用 vim：
```bash
vim ~/.bashrc
```
文件中插入一行：
```sh
alias myscheme='rlwrap -r -c -f "$HOME"/mit_scheme_bindings.txt scheme'
```
保存后应用配置：
```bash
source ~/.bashrc
```

### 3. 学习 scheme 的一些网站
1. [Yet Another Scheme Tutorial][3]
2. [Learn page of GNU guile][4]








[1]: https://www.gnu.org/software/mit-scheme/
[2]: https://stackoverflow.com/questions/11908746/mit-scheme-repl-with-command-line-history-and-tab-completion
[3]: http://www.shido.info/lisp/idx_scm_e.html
[4]: https://www.gnu.org/software/guile/learn/