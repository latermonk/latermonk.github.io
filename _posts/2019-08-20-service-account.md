---
layout: post
title:  " clusterrole-and-binding  "
date:   2019-08-20 10:07:14 +0800
categories: jekyll update
---
# service account

对于api-server 来讲有两种客户端：
- user
- Pod

user是外部系统管理的，而Pod则使用**serviceaccount**来作为认证访问api-server   



![serviceaccount-01.png](https://raw.githubusercontent.com/latermonk/latermonk.github.io/master/_posts/_images/serviceaccount-01.png)

- serviceaccount 是namespace级别的
- 多个Pod可以共用一个serviceaccount
- 一个namespace中的Pod无法使用 另外一个namespace中的serviceaccount

 





---------------
![rolebing00.png](https://raw.githubusercontent.com/latermonk/latermonk.github.io/master/_posts/_images/rolebing00.png)

