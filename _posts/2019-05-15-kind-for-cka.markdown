---
layout: post
title:  "install kind for cka exam on ubuntu 18.04"

categories: jekyll update
---

# kind for cka exam

## install docker

```
apt install docker.io
```


## install golang

```
apt install golang
```

### configure golang path

```

mkdir $HOME/go

vim ~/.bashrc
&& add the following lines:

export GOPATH=$HOME/go
export PATH=$PATH:$GOPATH/bin

source ~/.bashrc


```
##  Down kind and cluster config file


```
wget   https://github.com/kubernetes-sigs/kind/releases/download/0.2.1/kind-linux-amd64


mv  ./kind-linux-amd64    ~/go/kind

chmod +x  ~/go/kind

```

```
download config file

wget https://raw.githubusercontent.com/kubernetes-sigs/kind/master/site/content/docs/user/kind-example-config.yaml
```

## Create kind cluster 


```
kind create cluster --config kind-example-config.yaml
```

