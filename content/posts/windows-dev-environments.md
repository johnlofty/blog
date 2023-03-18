---
title: "Windows10 Dev Environement Setup"
date: 2021-05-15T11:21:26+08:00
---


最近因为工作需要开始在Windows10的PC上进行开发工作，但用惯了MacOS的zsh，在Windows下十分不习惯。于是便开始折腾。

经过一段时间的折腾，从最开始的不适应，慢慢已经逐渐比较顺手了。总结一下我是如何setup windows下面的开发环境。

### 命令行环境

----


#### WSL2 + Ubuntu

因为Windows的命令行实在是比较弱，而且命令都不太习惯，于是果断放弃，转投Linux环境。之前就看到Windows Terminal确实漂亮，于是打算试一试WSL2。

1. 安装WSL2之前需要完成一些配置，参考官方文档[这里](https://docs.microsoft.com/en-us/windows/wsl/install-win10)。
2. 之后再安装对应的发行版，如Ubuntu20.04。
3. 安装Windows Terminal。

安装过程本来很顺利，而且，不过据官方文档说，IO速度会比较慢。

但用了一段时间后发现一个比较蛋疼的问题，WSL2的实例是跑在一个NAT子网里，WSL2可以通过<code>/etc/resolve.conf</code>拿到host主机的IP，可以直接访问host主机。但反过来就比较麻烦，目前WSL2还没有能很好的解决这个问题，只能手动去配置转发规则，

总结一下wsl2的优缺点:

#### Pros

* WSL2可以直接访问windows文件系统
* 启动比较快速，性能比较好。
* Window Terminal 比较好看。

#### Cons:

* 不太方便做端口转发，可以手动配置 [参考这里](https://stackoverflow.com/questions/61002681/connecting-to-wsl2-server-via-local-network)。
* 以及其他一堆奇奇怪怪的兼容性问题

---

#### VirtualBox + Ubuntu

折腾一段时间wsl2后，发现奇奇怪怪的问题是在太多了，无奈之下，还是选择了用VirtualBox装Ubuntu的方案。毕竟是纯纯的Linux，不会有奇奇怪怪的问题。

装上Ubuntu 之后，安装openssh-server，开启端口转发之后就可以用xshell连接了。

#### Pros

* 100% Linux
* 端口映射可以很方便的将host端口映射到虚拟机端口。
* 可以配置共享文件夹，参考[这里](https://helpdeskgeek.com/virtualization/virtualbox-share-folder-host-guest/)

#### Cons

* 需要手动启动VirtualBox，再启动Ubuntu虚拟机。
* 性能不如WSL2。
* 需要手动配置CPU，内存，硬盘大小（万幸可以随时调整硬盘大小）。

---

除了命令行环境，其他工具如IDE，Docker，Git等等，倒是没啥差异。

有了比较好用的命令行环境后，我似乎没有那么怀念MacOS了。常用的工具软件都有对应的版本，Windows 桌面PC还提供了更好的硬件性能。

不过在笔记本领域，Apple Sillicon加持的MBP还是香的让人无法抵抗。期待一下今年的all new MacBook Pro。
