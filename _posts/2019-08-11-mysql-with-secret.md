---
layout: post
title:  "mysql with secret "
date:   2019-08-11 10:07:14 +0800
categories: jekyll update
---
#  mysql with secret


**mysecret2**

```
mysecret2 ：


echo admin > username

kubectl create secret generic mysecret2 --from-file=username


kubectl get secret mysecret2 -o yaml --export
echo YWRtaW4K | base64 -d # shows 'admin'


```

#   mounts the secret mysecret2 in a volume on path /etc/foo



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
  - image: nginx
    name: nginx
    volumeMounts:
      - name: secret-volume
        mountPath: /etc/foo
    resources: {}
  volumes:
    - name: secret-volume
      secret:
        secretName: mysecret2
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}

```


#   mount the variable 'username' from secret mysecret2 onto a new nginx pod in env variable called 'USERNAME'



```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx-nginx
spec:
  containers:
  - image: nginx
    name: nginx
    resources: {}
    env:
    - name: USERNAME
      valueFrom:
        secretKeyRef:
          name: mysecret2
          key: username
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}

```

