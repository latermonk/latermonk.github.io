---
layout: post
title:  "CKAD-exercises Notes -5   Services and Networking"

categories: jekyll update
---

# CKAD-exercises Notes 5


![Services](https://raw.githubusercontent.com/latermonk/latermonk.github.io/master/_posts/_images/Services.png)


### Create an nginx deployment of 2 replicas, expose it via a ClusterIP service on port 80\. Create a NetworkPolicy so that only pods with labels 'access: true' can access the deployment and apply it


```
kubectl run nginx --image=nginx --replicas=2 --port=80 --expose
kubectl describe svc nginx # see the 'run=nginx' selector for the pods
# or
kubectl get svc nginx -o yaml --export

vi policy.yaml
```

```
# Create the NetworkPolicy
kubectl create -f policy.yaml

# Check if the Network Policy has been created correctly:
kubectl run busybox --image=busybox --rm -it --restart=Never -- wget -O- http://nginx:80                       # This should not work
kubectl run busybox --image=busybox --rm -it --restart=Never --labels=access=true -- wget -O- http://nginx:80  # This should be fine
```


