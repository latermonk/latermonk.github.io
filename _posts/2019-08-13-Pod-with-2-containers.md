---
layout: post
title:  "Pod with 2 containers  "
date:   2019-08-13 10:07:14 +0800
categories: jekyll update
---
#  Pod with 2 containers 



[https://github.com/dgkanatsios/CKAD-exercises/blob/master/g.state.md](https://github.com/dgkanatsios/CKAD-exercises/blob/master/g.state.md)


##  design a pod with two containers 


```
k run nginx --image=nginx --restart=Never -o yaml --dry-run  -- sh -c  'sleep 3600' >  nginx-pod.yaml 

```
得到如下的YAML：

```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
spec:
  containers:
  - args:
    - sh
    - -c
    - sleep 3600
    image: nginx
    name: nginx
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}

```


```
另个容器的YAML：

==

apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
spec:
  containers:
  - args:
    - sh
    - -c
    - sleep 3600
    image: nginx
    name: nginx
    resources: {}
  - args:
    - sh
    - -c
    - sleep 3600
    image: nginx
    name: nginx
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}

```


**Pod的启动过程如下**

```
Events:
  Type    Reason     Age   From                 Message
  ----    ------     ----  ----                 -------
  Normal  Scheduled  22s   default-scheduler    Successfully assigned default/nginx to i-95544c65
  Normal  Pulling    20s   kubelet, i-95544c65  Pulling image "nginx"
  Normal  Pulled     16s   kubelet, i-95544c65  Successfully pulled image "nginx"
  Normal  Created    16s   kubelet, i-95544c65  Created container nginx1
  Normal  Started    15s   kubelet, i-95544c65  Started container nginx1
  Normal  Pulling    15s   kubelet, i-95544c65  Pulling image "nginx"
  Normal  Pulled     11s   kubelet, i-95544c65  Successfully pulled image "nginx"
  Normal  Created    11s   kubelet, i-95544c65  Created container nginx2
  Normal  Started    10s   kubelet, i-95544c65  Started container nginx2

```
可以看到是启动了两个容器的 

另外从DashBoard也可以看出来。


