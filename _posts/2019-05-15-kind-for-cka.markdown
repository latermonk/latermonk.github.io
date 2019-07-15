---
layout: post
title:  "install kind for cka exam on ubuntu 18.04"

categories: jekyll update
---

# kind for cka exam

## install docker

```
apt install docker.io -y
```

##  Down kind and cluster config file


```
cd /usr/local/bin

wget   https://github.com/kubernetes-sigs/kind/releases/download/0.2.1/kind-linux-amd64

mv  kind-linux-amd64   kind

chmod +x   kind

```

```
Then download config file

cd /usr/local/bin

wget https://raw.githubusercontent.com/kubernetes-sigs/kind/master/site/content/docs/user/kind-example-config.yaml

```

## Create kind cluster 


```

kind create cluster --config kind-example-config.yaml

```
## install kubectl

```
Install kubectl:

snap install kubectl  --classic

```


## Test the cluster 


```
kubectl cluster-info 


kubectl get cs [componentstatuses]

```


```
kubectl run nginx --image=nginx 
```

## config completion


```
apt install bash-completion
```


```
add kube config file:

export KUBECONFIG="$(kind get kubeconfig-path --name="kind")"

```


```
vim ~/.bashrc

add:

source <(kubectl completion bash)


```


```

vim ~/.bashrc
add:


alias k=kubectl
complete -F __start_kubectl k

```


