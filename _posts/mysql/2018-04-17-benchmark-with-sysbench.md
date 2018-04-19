---
layout: post
title: "Benchmark with Sysbench"
date: 2018-04-17 15:15:01 +0800
author: Shawn Yan
categories: mysql
tag: mysql sysbench
excerpt: a25
---

## Sysbench

- Dependencies

```bash
yum -y install make automake libtool pkgconfig libaio-devel
# For MySQL support, replace with mysql-devel on RHEL/CentOS 5
yum -y install mariadb-devel
# For PostgreSQL support
yum -y install postgresql-devel
```

- Sysbench v1.0.14

https://github.com/shawn0915/mariadb-tools

## Key Parameter

- Server

```
cpu
memory
disk
network
```

- OS

```
os version
kernel version
```

- MariaDB

```
version
innodb_buffer_pool_size
innodb_buffer_pool_instances
sync_binlog
innodb_page_size
innodb_doublewrite
innodb_flush_log_at_trx_commit
PS
```

## Usage

```bash
sysbench prepare/run/cleanup
```


## Reference

- https://github.com/akopytov/sysbench
- https://github.com/akopytov/sysbench/releases
- https://src.fedoraproject.org/cgit/rpms/sysbench.git/
- https://www.oschina.net/question/12_90065
- https://github.com/MariaDB/mariadb.org-tools/blob/master/sysbench/run-sysbench.sh

