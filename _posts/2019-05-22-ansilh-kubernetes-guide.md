


---
layout: post
title:  " ansilh's k8s guide "

categories: jekyll update
---



[https://ansilh.com/](https://ansilh.com/)

# BANG!!!


```
查看一个YAML文件的层级结构的方法：

k run nginx --image=nginx --restart=Never 

then:

k get po nginx -o yaml --export

```



## Requests and limits

### command line

```
kubectl run nginx --image=nginx --restart=Never --requests='cpu=100m,memory=256Mi' --limits='cpu=200m,memory=512Mi'
```
### yaml way


```
spec:
  containers:
  - image: nginx
    imagePullPolicy: Always
    name: nginx
    resources:
      limits:
        cpu: 200m
        memory: 512Mi
      requests:
        cpu: 100m
        memory: 256Mi

```

# Q1:  pod的YAML内部是如何使用label的？

##  元数据

```
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx

```
## label selector


```
yaml文件内部如何表示？
```
# YAML crash course

[https://ansilh.com/05-yaml_primer/01-structure/](https://ansilh.com/05-yaml_primer/01-structure/)








