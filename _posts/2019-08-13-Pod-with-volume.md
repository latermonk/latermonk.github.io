---
layout: post
title:  "  Pod with volumes  "
date:   2019-08-13 10:07:14 +0800
categories: jekyll update
---
#  Pod with volumes


#  emptyDir  --  Pod内容器之间共享Volume





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
    name: nginx1
    volumeMounts:
    - mountPath: /etc/foo
      name: cache-volume
    resources: {}
  - args:
    - sh
    - -c
    - sleep 3600
    image: nginx
    name: nginx2
    volumeMounts:
    - mountPath: /etc/foo
      name: cache-volume
    resources: {}
  volumes:
  - name: cache-volume
    emptyDir: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}

```


**check**

login  nginx2
```
k exec nginx -c nginx2 -it -- sh 
```
cp /etc/passwd  to  /etc/foo/passwd
```
cp /etc/passwd /etc/foo/passwd
```
login  nginx1 and cat /etc/foo/passwd


```
k exec nginx -c nginx1 -it -- sh


cat /etc/foo/passwd

```



#  pv,pvc



