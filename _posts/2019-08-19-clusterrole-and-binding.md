---
layout: post
title:  " clusterrole-and-binding  "
date:   2019-08-19 10:07:14 +0800
categories: jekyll update
---
# clusterrole-and-binding

- serviceaccount 代表的是Pod
- Role 是动作  

如下图：

role-01



![role-01](https://raw.githubusercontent.com/latermonk/latermonk.github.io/master/_posts/_images/role-01.png)


**用户和serviceccount 如何和动作建立关联？**
答案是 Rolebinding 



![rolebing00.png](https://raw.githubusercontent.com/latermonk/latermonk.github.io/master/_posts/_images/rolebing00.png)


每个命名空间都是有一些资源的：

![sa-luster-role.png](https://raw.githubusercontent.com/latermonk/latermonk.github.io/master/_posts/_images/sa-luster-role.png)


**完整过程展示**


```
新建一个namespace: foo


k create ns foo 
```
总共分三步：



![rolebing01.png](https://raw.githubusercontent.com/latermonk/latermonk.github.io/master/_posts/_images/rolebing01.png)

#  **创建 user/serviceaccount**
user就是实际的用户
serviceaccount就是Pod

比如使用namespace默认的serviceaccount: default  -->  foo:default

当然是完全可以在namespace内部定义serviceaccount的




# **创建 Role:**
**HELP**


```
k -n foo create role  -h
```


```

Create a role with single rule.

Examples:
  # Create a Role named "pod-reader" that allows user to perform "get", "watch" and "list" on pods
  kubectl create role pod-reader --verb=get --verb=list --verb=watch --resource=pods
  
  # Create a Role named "pod-reader" with ResourceName specified
  kubectl create role pod-reader --verb=get --resource=pods --resource-name=readablepod --resource-name=anotherpod
  
  # Create a Role named "foo" with API Group specified
  kubectl create role foo --verb=get,list,watch --resource=rs.extensions
  
  # Create a Role named "foo" with SubResource specified
  kubectl create role foo --verb=get,list,watch --resource=pods,pods/status

Options:
      --allow-missing-template-keys=true: If true, ignore any errors in templates when a field or map key is missing in
the template. Only applies to golang and jsonpath output formats.
      --dry-run=false: If true, only print the object that would be sent, without sending it.
  -o, --output='': Output format. One of:
json|yaml|name|go-template|go-template-file|template|templatefile|jsonpath|jsonpath-file.
      --resource=[]: Resource that the rule applies to
      --resource-name=[]: Resource in the white list that the rule applies to, repeat this flag for multiple items
      --save-config=false: If true, the configuration of current object will be saved in its annotation. Otherwise, the
annotation will be unchanged. This flag is useful when you want to perform kubectl apply on this object in the future.
      --template='': Template string or path to template file to use when -o=go-template, -o=go-template-file. The
template format is golang templates [http://golang.org/pkg/text/template/#pkg-overview].
      --validate=true: If true, use a schema to validate the input before sending it
      --verb=[]: Verb that applies to the resources contained in the rule

Usage:
  kubectl create role NAME --verb=verb --resource=resource.group/subresource [--resource-name=resourcename] [--dry-run]
[options]

Use "kubectl options" for a list of global command-line options (applies to all commands).

```

#  **创建Role**

```
kubectl -n foo create role pod-reader --verb=get --verb=list  --resource=services
```
YAML:

```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: service-reader
  namespace: foo
  resourceVersion: "268433"
  selfLink: /apis/rbac.authorization.k8s.io/v1/namespaces/foo/roles/service-reader
  uid: 0f394277-00ff-49e3-a323-fd45b1b63290
rules:
- apiGroups:
  - ""
  resources:
  - services
  verbs:
  - get
  - list

```

# **创建RoleBinding**


```
kubectl create rolebinding NAME --clusterrole=NAME|--role=NAME [--user=username] [--group=groupname]
[--serviceaccount=namespace:serviceaccountname] [--dry-run] [options]

```


```
k -n foo create rolebinding test-test --serviceaccount=foo:default --role=service-reader
```




![rolebing02.png](https://raw.githubusercontent.com/latermonk/latermonk.github.io/master/_posts/_images/rolebing02.png)



