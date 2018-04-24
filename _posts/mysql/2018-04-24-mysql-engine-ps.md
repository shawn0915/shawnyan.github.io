---
layout: post
title: "MySQL Performance Schema"
date: 2018-04-23 16:19:01 +0800
author: Shawn Yan
categories: mysql
tag: mysql ps engine
excerpt: a34
---

Check PS Status

```mysql
show global variables like '%performance_schema%';
show global status like '%performance_schema%';
show engine performance_schema status;
```




## Reference

- https://mariadb.com/kb/en/library/foreign-keys/
