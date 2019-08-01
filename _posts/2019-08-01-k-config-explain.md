---
layout: post
title:  "kubectl config "
date:   2019-08-01 10:07:14 +0800
categories: jekyll update
---
#  kubectl config

![k-config](https://raw.githubusercontent.com/latermonk/latermonk.github.io/master/_posts/_images/k-config.png)


```
Modify kubeconfig files using subcommands like "kubectl config set current-context my-context"

 The loading order follows these rules:

  1.  If the --kubeconfig flag is set, then only that file is loaded. The flag may only be set once and no merging takes
place.
  2.  If $KUBECONFIG environment variable is set, then it is used as a list of paths (normal path delimiting rules for
your system). These paths are merged. When a value is modified, it is modified in the file that defines the stanza. When
a value is created, it is created in the first file that exists. If no files in the chain exist, then it creates the
last file in the list.
  3.  Otherwise, ${HOME}/.kube/config is used and no merging takes place.

Available Commands:
  current-context Displays the current-context
  delete-cluster  Delete the specified cluster from the kubeconfig
  delete-context  Delete the specified context from the kubeconfig
  get-clusters    Display clusters defined in the kubeconfig
  get-contexts    Describe one or many contexts
  rename-context  Renames a context from the kubeconfig file.
  set             Sets an individual value in a kubeconfig file
  set-cluster     Sets a cluster entry in kubeconfig
  set-context     Sets a context entry in kubeconfig
  set-credentials Sets a user entry in kubeconfig
  unset           Unsets an individual value in a kubeconfig file
  use-context     Sets the current-context in a kubeconfig file
  view            Display merged kubeconfig settings or a specified kubeconfig file

Usage:
  kubectl config SUBCOMMAND [options]

Use "kubectl <command> --help" for more information about a given command.
Use "kubectl options" for a list of global command-line options (applies to all commands).

```

Q1: kubectl config use-context  context_name , context_name 的列表如何查询？

```
直接查看 config文件 ？

```
Q2：如何在多个集群之间进行切换？


```
kubectl config use-context
```
[https://kubernetes.io/zh/docs/tasks/access-application-cluster/configure-access-multiple-clusters/](https://kubernetes.io/zh/docs/tasks/access-application-cluster/configure-access-multiple-clusters/)

Q3: 如何生成一个 Config 类型文件的模板 ？


```
todo
```


##  set-cluster

```shell

kubectl config \
--kubeconfig=config-demo set-cluster development \
--server=https://1.2.3.4 \
--certificate-authority=fake-ca-file


```
![set-cluster](https://raw.githubusercontent.com/latermonk/latermonk.github.io/master/_posts/_images/set-cluster.png)



## set 

```

	kubectl config 
	--kubeconfig=config-demo  set-credentials developer \
	--client-certificate=fake-cert-file \
	--client-key=fake-key-seefile

```


## set-context


```
kubectl config --kubeconfig=config-demo set-credentials developer --client-certificate=fake-cert-file --client-key=fake-key-seefile
```
![set-credentials](https://raw.githubusercontent.com/latermonk/latermonk.github.io/master/_posts/_images/set-credentials.png)
