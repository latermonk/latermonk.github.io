---
layout: post
title:  "  k8s  components   "
date:   2019-08-17 10:07:14 +0800
categories: jekyll update
---
#   k8s  components 


![k8s-control-plane](https://raw.githubusercontent.com/latermonk/latermonk.github.io/master/_posts/_images/k8s-control-plane.png)


##  控制平面组件
etcd
apiserver
scheduler
controller-mangaer

##  工作节点组件
kubelet
kubeproxy
runtime

##  插件
 
dash-board
dns
ingress
heapster
nci


```
查看控制面组件状态
k get cs
```
#  组件之间的通信

- 系统组件之间只能通过api-server通信，系统组件之间并不会直接通信
- 只有apiserver和etcd通信，其他的组件都不直接和etcd通信
- 其他组件一般和apiserver通信都是由组件发起的，apiserver一般不会主动发起通信请求
- 多个etcd & apiserver可以并行工作，调度器和控制器则不行。一个调度器和控制器在工作，其他的调度器和控制器全都standby

- kubelet要部署在实体机上，其他的组件都可以以Pod方式部署


![k8s-control-plane02](https://raw.githubusercontent.com/latermonk/latermonk.github.io/master/_posts/_images/k8s-control-plane02.png)


