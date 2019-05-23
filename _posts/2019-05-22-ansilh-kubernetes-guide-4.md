


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









