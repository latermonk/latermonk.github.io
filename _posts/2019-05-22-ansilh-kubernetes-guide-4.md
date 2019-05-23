


---

layout: post
title:  " ansilh's k8s guide 5 "

categories: jekyll update

---


# PART 5


# CONFIGMAPS
## create 

###  from literal
```
kubectl create configmap myconfig --from-literal=VAR1=val1

```


```
k create configmap cc  --from-literal=suername=admin  --dry-run -o yaml > cc.yaml
```

```
apiVersion: v1
data:
  suername: admin
kind: ConfigMap
metadata:
  creationTimestamp: null
  name: cc
```


```
kubectl create -f cc.yaml
```

### from file

```
cat <<EOF >configFile
This content is coming from a file
EOF

```
then:

```
kubectl create configmap myconfig --from-file=configFile

```


```
apiVersion: v1
kind: ConfigMap
metadata:
  name: myconfig
data:
  configFile: |
    This content is coming from a file
    Also this file have multiple lines

```
 
```
kubectl create -f cc.yaml
```


##  use



# SECRETS
## create 
## use


# DEPLOYMENT

## 

```
kubectl get pod nginx-7cdbd8cdc9-vfbn8 --show-labels

```

```
label:  run=nginx

```

create a svc to expose deploy  nginx :


```
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  labels:
    run: nginx-svc
  name: nginx-svc
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    run: nginx
  type: LoadBalancer

```

或者：

直接使用命令：

```
k expose deployment nginx --port=80  --target-port=80 --dry-run -o yaml > svc.yaml
```

```
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    run: nginx
status:
  loadBalancer: {}
```

然后：


```
kubectl apply -f nginx-svc.yaml

```




使用busybox访问：


```
k run b --image=busybox --restart=Never -it --rm -- /bin/sh
```



# Deployment



![Deployment](https://raw.githubusercontent.com/latermonk/latermonk.github.io/master/_posts/_images/Deployment.png)


