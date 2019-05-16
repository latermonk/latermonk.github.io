---
layout: post
title:  "CKAD-exercises Notes"

categories: jekyll update
---

# CKAD-exercises Notes


## Delete all resource at one time 


```
# Delete everything from the current namespace:

k delete all --all


# Delete everything from a namespace you use the -n flag 

【Caution!!!】
kubectl delete all --all -n {namespace}

# Delete a namespace. This will delete everything that belongs to it

kubectl delete namespace {mynamespace}


```

## Create a pod using YAML file

```
k run nginx --image=nginx --restart=Never --dry-run -o yaml > nginx-pod.yaml
```


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
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}

```


