---
layout: post
title:  "CKAD-exercises Notes -1 Core Concepts"

categories: jekyll update
---

# CKAD-exercises Notes 1


## Delete all resource at one time 


```
# Delete everything from the current namespace:

k delete all --all


# Delete everything from a namespace you use the -n flag 

【Caution!!!】
## clear a namespace
kubectl delete all --all -n {namespace}

## clear all namespace
kubectl delete all --all --all-namespaces

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


```
 k create -f nginx-pod.yaml
```

##  Q1: Is  --command a must in kubectl run ?

If true and extra arguments are present, use them as the 'command' field in the container, rather than the 'args' field which is the default
默认--command的值是false的，一旦打开--command并且有额外的参数说明就说明是 容器中的命令而不是kubectl的参数

```
kubectl run nginx --image=nginx --command -- <cmd> <arg1> ... <argN>
```

举例：

```
k run busybox --image=busybox --restart=Never  --command -- ls /
```


```
k run busybox --image=busybox --restart=Never  -- ls /
```
貌似有没有 --command结果是一样的

## Q2： -it --rm   一定要一起用才行么？
```
-it --rm   一个是交互的意思  一个是执行完命令之后销毁pod的意思
```
单独的： --rm 提示

```
k run nginx --image=nginx  --rm --restart=Never --command -- ls /


error: --rm should only be used for attached containers

```

单独的： -it


```
k run nginx --image=nginx  -it  --restart=Never --command -- ls /  

-- 是可以的，但是没有--rm的效果，也就是pod执行结束后，不会自动删除
-- 但是是 busybox pod 处于 completed 状态 [为什么？]



所以应该执行：
k run nginx --image=nginx  -it  --restart=Never --command -- /bin/sh
-- 才行

-it和-- /bin/sh 合起来使用的话是进入到容器内部交互的意思

```
所以想要直接在容器中运行指定的命令的话，直接用：

```
k run nginx --image=nginx  -it --rm  --restart=Never --command -- ls / 
```
想要进行容器之后再执行命令的话就用：

```
k run nginx --image=nginx  -it --rm  --restart=Never --command -- /bin/sh
```


## Q3: kubectl generators

[https://kubernetes.io/docs/reference/kubectl/conventions/#generators](https://kubernetes.io/docs/reference/kubectl/conventions/#generators)

例如：

```
kubectl run nginx --image=nginx --restart=Never   --generator=run-pod/v1  --dry-run -o yaml > test.yaml
```
产生一个POD的YAML文件


## Create a busybox pod (using YAML) that runs the command "env". Run it and see the output


```
kubectl run busybox --image=busybox --restart=Never --dry-run -o yaml --command  -- env > envpod-1.yaml


kubectl  run busybox --image=busybox --restart=Never --dry-run -o yaml --command -- env > envpod-2.yaml

```



```
k run busybox --image=busybox --restart=Never --command -- env --dry-run -o yaml > env-pod-3.yaml
```
【Caution!!!】-o yaml 必须位于 --command的前方

否则，不是去产生YAML文件，而是直接去创建了Pod !!!


## et the YAML for a new ResourceQuota called 'myrq' without creating it


```
kubectl create quota myrq --hard=cpu=1,memory=1G,pods=2 --dry-run -o yaml
```


## Q4 kubectl run 中的port

### hostport 主机端口

The host port mapping for the container port. To demonstrate a single-machine container.

### port   容器端口或者SVC端口
The port that this container exposes. If --expose is true, this is also the port used by the service that is created.


## 查看容器中镜像的版本

```
kubectl get po nginx -o jsonpath='{.spec.containers[].image}{"\n"}'
```
这个路径是怎么产生的？




## Create a busybox pod that echoes 'hello world' and then exits

```
kubectl run busybox --image=busybox -it --rm --restart=Never -- echo 'hello world'

# or

kubectl run busybox --image=busybox -it --rm --restart=Never -- /bin/sh -c 'echo hello world'

```

## Create an nginx pod and set an env value as 'var1=val1'. Check the env value existence within the pod


解法1：

```
kubectl run nginx --restart=Never --image=nginx --env=var1=val1 -it --rm -- env
```



解法2：
```

kubectl run nginx --image=nginx --restart=Never --env=var1=val1
# then
kubectl exec -it nginx -- env
# or
kubectl describe po nginx | grep val1
```

