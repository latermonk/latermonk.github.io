---
layout: post
title:  " kubectl skills"

categories: jekyll update
---

# kubectl skills


## important


```
kubectl explain Pod.spec --recursive |less
```

```
k explain job.spec --recursive |less
```


## reference:
CKAD考试技巧汇总
[https://mp.weixin.qq.com/s?src=11&timestamp=1558077978&ver=1611&signature=GfijsvsnZJaTpWqPMekwR0AY-xWlQL0s0rT9eYWWQFliI1mDc1UWvtXyRyUPdXbHWuu8xymFJY*dfbByXUoPjYwaktvEIclI9DNCrgQDax6BMXng3R8nf6pzl8myFqxO&new=1](https://mp.weixin.qq.com/s?src=11&timestamp=1558077978&ver=1611&signature=GfijsvsnZJaTpWqPMekwR0AY-xWlQL0s0rT9eYWWQFliI1mDc1UWvtXyRyUPdXbHWuu8xymFJY*dfbByXUoPjYwaktvEIclI9DNCrgQDax6BMXng3R8nf6pzl8myFqxO&new=1)





```
1# 在less中查看Pod资源顶层API
2kubectl explain Pod | less
3
4# 在less中查看Pod资源spec键下的API
5kubectl explain Pod.spec | less
6
7# 在less中查看Pod资源spec键下所有内容
8kubectl explain Pod.spec --recursive | less
```




