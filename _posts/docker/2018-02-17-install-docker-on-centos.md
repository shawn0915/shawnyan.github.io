---
layout: post
title:  "CentOS 7环境下安装Docker CE"
date:   2018-02-17 21:01:01 +0800
author: 严少安
categories: docker
tag: docker centos install
---

Docker分为社区版和企业版两种版本，下面演示Docker社区稳定版本的安装过程。

## 环境信息

> CentOS 7.4
>
> Docker CE v17.12

## 安装Docker CE

### 安装依赖及仓库

```bash
sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
```



## Reference

- https://docs.docker.com/engine/installation/
- https://docs.docker.com/install/linux/docker-ce/centos/
- http://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html