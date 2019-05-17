---
layout: post
title:  "CKAD-exercises Notes -2 Pod Design"

categories: jekyll update
---

# CKAD-exercises Notes 2


## Create a Pod with two containers, both with image busybox and command "echo hello; sleep 3600". Connect to the second container and run 'ls'



```
k run two-busy --image=busybox --restart=Never --dry-run -o yaml --command -- /bin/sh -c "echo hello; sleep 3600" >  sea2.yaml
```

## Create a pod that will be deployed to a Node that has the label 'accelerator=nvidia-tesla-p100'

```source-yaml
apiVersion: v1
kind: Pod
metadata:
  name: cuda-test
spec:
  containers:
    - name: cuda-test
      image: "k8s.gcr.io/cuda-vector-add:v0.1"
  nodeSelector: # add this
    accelerator: nvidia-tesla-p100 # the slection label
```
You can easily find out where in the YAML it should be placed by:

```source-shell
kubectl explain po.spec
```

## label and annotation



![label-annotations](https://raw.githubusercontent.com/latermonk/latermonk.github.io/master/_posts/_images/label-annotations.png)


