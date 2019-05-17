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


## Jobs and CronJob

### Create a job with image perl that runs default command with arguments "perl -Mbignum=bpi -wle 'print bpi(2000)'"

```
k run pi --image=perl --restart=OnFailure   -- /bin/sh -c  "perl -Mbignum=bpi -wle 'print bpi(2000)'"
```

```
kubectl run pi --image=perl --restart=OnFailure -- perl -Mbignum=bpi -wle 'print bpi(2000)'
```

## Q: follow the logs


```
kubectl logs busybox-ptx58 -f
```

### Create the same job, make it run 5 times, one after the other. Verify its status and delete it


```
kubectl create job busybox --image=busybox --dry-run -o yaml -- /bin/sh -c 'echo hello;sleep 30;echo world' > job.yaml
vi job.yaml
```
## Add job.spec.completions=5


```
apiVersion: batch/v1
kind: Job
metadata:
  creationTimestamp: null
  labels:
    run: busybox
  name: busybox
spec:
  completions: 5 # add this line
  template:
    metadata:
      creationTimestamp: null
      labels:
        run: busybox
    spec:
      containers:
      - args:
        - /bin/sh
        - -c
        - echo hello;sleep 30;echo world
        image: busybox
        name: busybox
        resources: {}
      restartPolicy: OnFailure
status: {}
```
then execute :

```
kubectl create -f job.yaml
```

### Create the same job, but make it run 5 parallel times

# job.spec.parallelism=5



```
apiVersion: batch/v1
kind: Job
metadata:
  creationTimestamp: null
  labels:
    run: busybox
  name: busybox
spec:
  parallelism: 5 # add this line
  template:
    metadata:
      creationTimestamp: null
      labels:
        run: busybox
    spec:
      containers:
      - args:
        - /bin/sh
        - -c
        - echo hello;sleep 30;echo world
        image: busybox
        name: busybox
        resources: {}
      restartPolicy: OnFailure
status: {}
```



## CronJob

https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/

https://kubernetes.io/docs/tasks/job/automated-tasks-with-cron-jobs/


```
kubectl run busybox --image=busybox --restart=OnFailure --schedule="*/1 * * * *" -- /bin/sh -c 'date; echo Hello from the Kubernetes cluster'
```


