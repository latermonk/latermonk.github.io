---
layout: post
title:  "k8s  dashboard "
date:   2019-08-09 10:07:14 +0800
categories: jekyll update
---
#  k8s dashboard



# Creating sample user

## Create Service Account
```
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kube-system
```

## Create ClusterRoleBinding
```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: admin-user
  namespace: kube-system
```

## Bearer Token

```
kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep admin-user | awk '{print $1}')
```


# Deploying the Dashboard UI

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta1/aio/deploy/recommended.yaml
```


#  configure NodePort and access UI


```
k get svc -n kubernetes-dashboard
```

```
 k edit -n kubernetes-dashboard  svc kubernetes-dashboard
```

#  Open NodePort:NodePort in broswer


