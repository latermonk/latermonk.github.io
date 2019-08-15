---
layout: post
title:  "  k8s change namespace  "
date:   2019-08-15 10:07:14 +0800
categories: jekyll update
---

#   k8s change namespace

**check context**

```
kubectl config current-context 
```

**create a new namespace**


```
kubectl create ns mywebapp
```

**change to new namespace**


```
kubectl config set-context minikube --namespace mywebapp
```

**check on which namespace **


```
kubectl get sa default -o jsonpath='{.metadata.namespace}'
```


