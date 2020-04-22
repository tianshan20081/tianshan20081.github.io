---
title: Centos7 升级 Kernel 内核版本
date: 2020-04-12 19:01:38
tags:
---

### 查看 系统 内核版本
```
[root@host ~]# yum list kernel
已加载插件：fastestmirror
Loading mirror speeds from cached hostfile
 * base: repos.lax.quadranet.com
 * elrepo: repos.lax-noc.com
 * extras: mirrors.cat.pdx.edu
 * updates: repos-lax.psychz.net
pgdg-common                                                                                                                            | 2.9 kB  00:00:00
pgdg-common/7/x86_64/primary_db                                                                                                        | 125 kB  00:00:01
已安装的软件包
kernel.x86_64                                                          3.10.0-957.1.3.el7                                                             @updates
kernel.x86_64                                                          3.10.0-957.10.1.el7                                                            @updates
kernel.x86_64                                                          3.10.0-1062.4.1.el7                                                            @updates
kernel.x86_64                                                          3.10.0-1062.4.3.el7                                                            @updates
kernel.x86_64                                                          3.10.0-1062.18.1.el7                                                           @updates
[root@host ~]#
```



```shell
[root@host ~]# uname -r
3.10.0-1062.18.1.el7.x86_64
```



### **升级安装ELRepo**

```
rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-4.el7.elrepo.noarch.rpm
yum --enablerepo=elrepo-kernel install -y kernel-lt
[root@host ~]# yum --enablerepo=elrepo-kernel install -y kernel-lt
已加载插件：fastestmirror
Loading mirror speeds from cached hostfile
 * base: repos.lax.quadranet.com
 * elrepo: repos.lax-noc.com
 * elrepo-kernel: repos.lax-noc.com
 * extras: mirrors.cat.pdx.edu
 * updates: repos-lax.psychz.net
elrepo-kernel                                                                                                                          | 2.9 kB  00:00:00
elrepo-kernel/primary_db                                                                                                               | 1.9 MB  00:00:00
正在解决依赖关系
There are unfinished transactions remaining. You might consider running yum-complete-transaction, or "yum-complete-transaction --cleanup-only" and "yum history redo last", first to finish them. If those don't work you'll have to try removing/installing packages by hand (maybe package-cleanup can help).
--> 正在检查事务
---> 软件包 kernel-lt.x86_64.0.4.4.218-1.el7.elrepo 将被 安装
--> 解决依赖关系完成

依赖关系解决

==============================================================================================================================================================
 Package                           架构                           版本                                            源                                     大小
==============================================================================================================================================================
正在安装:
 kernel-lt                         x86_64                         4.4.218-1.el7.elrepo                            elrepo-kernel                          39 M

事务概要
==============================================================================================================================================================
安装  1 软件包

总下载量：39 M
安装大小：180 M
Downloading packages:
kernel-lt-4.4.218-1.el7.elrepo.x86_64.rpm                                                                                              |  39 MB  00:00:06
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  正在安装    : kernel-lt-4.4.218-1.el7.elrepo.x86_64                                                                                                     1/1
  验证中      : kernel-lt-4.4.218-1.el7.elrepo.x86_64                                                                                                     1/1

已安装:
  kernel-lt.x86_64 0:4.4.218-1.el7.elrepo

完毕！
```



### **查看当前实际启动顺序**

```
[root@mz ~]# grub2-editenv list
saved_entry=CentOS Linux (3.10.0-1062.9.1.el7.x86_64) 7 (Core)
```



### 设置开机从新内核启动

```
# //grub2-set-default 'CentOS Linux (3.10.0-1062.9.1.el7.x86_64) 7 (Core)'
# grub2-set-default 'CentOS Linux (4.4.218-1.el7.elrepo.x86_64) 7 (Core)'

```



### 重启 && 查看内核版本

```
[root@host ~]# uname -sr
Linux 4.4.218-1.el7.elrepo.x86_64
```

