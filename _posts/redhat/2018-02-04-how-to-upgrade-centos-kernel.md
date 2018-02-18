---
layout: post
title: "升级CentOS 7.4内核版本的三种方案"
date: 2018-02-04 12:01:01 +0800
author: 严少安
categories: redhat
tag: redhat centos kernel
excerpt: a1
---

![](https://shawn0915.github.io/assets/img_redhat/centos-logo.png)

在实验环境下，已安装了最新的CentOS 7.4操作系统，现在需要升级内核版本。下面提供三种常用方案，以供参考。

- 方案一：小版本升级
- 方案二：大版本升级
- 方案三：自编译升级

## 实验环境信息

> CentOS-7-x86_64-Minimal-1708.iso
>
> CentOS Linux release 7.4.1708 (Core)
>
> Kernel 3.10.0-693.el7.x86_64

## 方案一：小版本升级

小版本升级，指的是在当前内核大版本不变的基础之上，做小版本更新。此方法适用于更新内核补丁。
确认连接并同步CentOS自带yum源，更新内核版本。

实验步骤：

```bash
sudo yum list kernel
sudo yum update -y kernel
```

![](https://shawn0915.github.io/assets/img_redhat/a1-img/img-01.png)
![](https://shawn0915.github.io/assets/img_redhat/a1-img/img-02.png)
![](https://shawn0915.github.io/assets/img_redhat/a1-img/img-03.png)

此时，已安装成功，但若想将系统运行在新版本的kernel上，则需要重新启动操作系统。

![](https://shawn0915.github.io/assets/img_redhat/a1-img/img-04.png)

重启完成，至此，Kernel版本已升级至`3.10.0-693.17.1.el7.x86_64`

![](https://shawn0915.github.io/assets/img_redhat/a1-img/img-05.png)


## 方案二：大版本升级

大版本升级，是指将升级内核最新的主线版本或者长期支持版本。

实验步骤：

载入elrepo源，搜索内核更新资源，并进行更新操作。

```bash
# 载入公钥
sudo rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
# 安装ELRepo
sudo rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm
# 载入elrepo-kernel元数据
sudo yum --disablerepo=\* --enablerepo=elrepo-kernel repolist
# 查看可用的rpm包
sudo yum --disablerepo=\* --enablerepo=elrepo-kernel list kernel*
```

![](https://shawn0915.github.io/assets/img_redhat/a1-img/img-06.png)
![](https://shawn0915.github.io/assets/img_redhat/a1-img/img-07.png)


确认要安装的kernel，这里安装最新版本的kernel-ml
```bash
sudo yum --disablerepo=\* --enablerepo=elrepo-kernel install -y kernel-ml.x86_64
```

![](https://shawn0915.github.io/assets/img_redhat/a1-img/img-08.png)

重启，选择新版本内核进入系统。

![](https://shawn0915.github.io/assets/img_redhat/a1-img/img-09.png)

此时，操作系统使用的内核已升级为`4.15.0-1.el7.elrepo.x86_64`

![](https://shawn0915.github.io/assets/img_redhat/a1-img/img-10.png)

最后一步，建议将内核工具包一并升级

```bash
# 删除旧版本工具包
sudo yum remove kernel-tools-libs.x86_64 kernel-tools.x86_64
# 安装新版本工具包
sudo yum --disablerepo=\* --enablerepo=elrepo-kernel install -y kernel-ml-tools.x86_64
```

![](https://shawn0915.github.io/assets/img_redhat/a1-img/img-11.png)

至此，升级完成。


## 方案三：自编译升级

- Step1: 下载源码
- Step2: 安装gcc bc cmake
- Step3: 编译源码，安装新内核

自编译升级过程略微复杂，且不便于后期维护，具体实验步骤在此略去不表。

## 话题扩展

如何将新安装的内核设定为操作系统的默认内核，或者说如何将新版本的内核设置为重启后的默认内核？
仅需两步，之后重启即可。

```bash
sudo grub2-set-default 0
sudo grub2-mkconfig -o /etc/grub2.cfg
```

![](https://shawn0915.github.io/assets/img_redhat/a1-img/img-12.png)
![](https://shawn0915.github.io/assets/img_redhat/a1-img/img-13.png)


## 术语解析

- kernel-ml

kernel-ml 中的ml是英文【mainline stable】的缩写，elrepo-kernel中罗列出来的是最新的稳定主线版本。

- kernel-lt

kernel-lt 中的lt是英文【long term support】的缩写，elrepo-kernel中罗列出来的长期支持版本。


## Reference

- [the ELRepo Project](http://elrepo.org/tiki/tiki-index.php)
- [kernel.org](https://www.kernel.org/)
