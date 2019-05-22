


---
layout: post
title:  " ansilh's k8s guide "

categories: jekyll update
---



[https://ansilh.com/](https://ansilh.com/)

# BANG!!!


```
查看一个YAML文件的层级结构的方法：

k run nginx --image=nginx --restart=Never 

then:

k get po nginx -o yaml --export

```



## Requests and limits

### command line

```
kubectl run nginx --image=nginx --restart=Never --requests='cpu=100m,memory=256Mi' --limits='cpu=200m,memory=512Mi'
```
### yaml way


```
spec:
  containers:
  - image: nginx
    imagePullPolicy: Always
    name: nginx
    resources:
      limits:
        cpu: 200m
        memory: 512Mi
      requests:
        cpu: 100m
        memory: 256Mi

```

# Q1:  pod的YAML内部是如何使用label的？

##  元数据

```
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx

```
## label selector


```
yaml文件内部如何表示？
```
# YAML crash course

[https://ansilh.com/05-yaml_primer/01-structure/](https://ansilh.com/05-yaml_primer/01-structure/)




## Ports in Service Objects


## port  in  kubectl 


```
 --port=80 

 --target-port=9090  

 --type=NodePort
```


#### nodePort 
#### port  
#### targetPort

For example:

```
apiVersion: v1
kind: Service
metadata:
  name: order-service
spec:
  ports:
  - port: 8080
    targetPort: 8170
    nodePort: 32222
    protocol: TCP 
  selector:
    component: order-service-app
```


![svc-type](https://raw.githubusercontent.com/latermonk/latermonk.github.io/master/_posts/_images/svc-type.png)


```
k  get svc nginx -o yaml --export
```


```
Flag --export has been deprecated, This flag is deprecated and will be removed in future.
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
  selfLink: /api/v1/namespaces/default/services/nginx
spec:
  externalTrafficPolicy: Cluster
  ports:
  - port: 8964
    protocol: TCP
    targetPort: 80
  selector:
    run: nginx
  sessionAffinity: None
  type: NodePort
status:
  loadBalancer: {}

```
所以访问一个服务有三种办法：



![access-service](https://raw.githubusercontent.com/latermonk/latermonk.github.io/master/_posts/_images/access-service.png)






参考资料：
[https://vitalflux.com/kubernetes-port-targetport-and-nodeport/](https://vitalflux.com/kubernetes-port-targetport-and-nodeport/)




