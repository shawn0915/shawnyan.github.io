---
layout: post
title:  "在Docker上运行Oracle Database"
date:   2018-02-20 20:20:01 +0800
author: 严少安
categories: docker
tag: docker oracle
excerpt: a14
---

## Run Oracle on Docker

> Oracle Database 11.2.0.2 XE

> host swap space size need more than 2048M

拉取基础镜像
```bash
docker pull oraclelinux:7-slim
```

下载xe安装包
```html
http://download.oracle.com/otn/linux/oracle11g/xe/oracle-xe-11.2.0-1.0.x86_64.rpm.zip
```

定制镜像
```bash
cd oracleDatabase/dockerfiles
./buildDockerImage.sh -v 11.2.0.2 -x
```

## Reference

- https://github.com/oracle/docker-images/blob/master/OracleDatabase/Docker-OracleDatabase.md