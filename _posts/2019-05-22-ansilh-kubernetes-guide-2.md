


---

layout: post
title:  " ansilh's k8s guide 2 "

categories: jekyll update

---

[https://github.com/mhausenblas/kubectl-in-action](https://github.com/mhausenblas/kubectl-in-action)




# Multi-Container Pods

## inject data  to pod

```
kubectl run tea --image=ansilh/demo-tea --env=MY_NODE_NAME=scratch --restart=Never --dry-run -o yaml >pod-with-env.yaml

kubectl create -f pod-with-env.yaml

kubectl expose pod tea --port=80 --target-port=8080 --type=NodePort

kubectl get svc tea
NAME   TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
tea    NodePort   192.168.10.37   <none>        80:32258/TCP   42s



```
### extract the `nodeName` from spec

```
k8s@k8s-master-01:~$ kubectl get pods tea -o=jsonpath='{.spec.nodeName}' && echo
k8s-worker-01
k8s@k8s-master-01:~$ kubectl get pods tea -o=jsonpath='{.status.hostIP}' && echo
192.168.56.202
k8s@k8s-master-01:~$ kubectl get pods tea -o=jsonpath='{.status.podIP}' && echo
10.10.1.23
k8s@k8s-master-01:~$

```

# volume basic
[https://ansilh.com/07-multi_container_pod/02-volumes/](https://ansilh.com/07-multi_container_pod/02-volumes/)

```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
spec:
  volumes:
  - name: "data"
    hostPath:
      path: "/var/data"
  containers:
  - image: nginx
    name: nginx
    volumeMounts:
    - name: "data"
      mountPath: "/usr/share/nginx/html"
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}

```

# init-container


# manual-schedule

```
kubectl label node k8s-worker-01 disktype=3

```




```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    env: test
spec:
  containers:
  - name: nginx
    image: nginx
  nodeSelector:
    disktype: ssd

```

如果没有可用的node,则提示：

```
0/4 nodes are available: 4 node(s) didn't match node

```

当修改node: k8s-worker-01的标签为：

```
kubectl label node k8s-worker-01 disktype=ssd  --overwrite
```
之后，就能正常的调度

```
Successfully assigned default/nginx to kind-worker-X
```
# taints-and-tolerations



