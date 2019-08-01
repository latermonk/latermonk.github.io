---
layout: post
title:  "imagePullPolicy "
date:   2019-08-01 14:26:14 +0800
categories: jekyll update
---
#  imagePullPolicy


```
k  explain pod.spec.containers --recursive |grep imagePullPolicy
```
得到结果：

```
imagePullPolicy	<string>
```


```
k  explain pod.spec.containers
```
得到结果：

```
imagePullPolicy	<string>
     Image pull policy. 
		One of Always, Never, IfNotPresent. 
		Defaults to Always
     if :latest tag is specified, or IfNotPresent otherwise. Cannot be updated.
     More info:
     https://kubernetes.io/docs/concepts/containers/images#updating-images

```


## 解释

```
--image-pull-policy=Never

Always  总是从远端拉去镜像  【默认配置】
IfNotPresent
Never

```

| A0 | B0 | C0 |
|---|---|---|
| Always   | 总是从远端拉去镜像| 默认配置 |
| Never| 从来不从远端拉去镜像 | 使用本地 |
| IfNotPresent| 本地不存在则从远端拉取 | 没有就拉 |






