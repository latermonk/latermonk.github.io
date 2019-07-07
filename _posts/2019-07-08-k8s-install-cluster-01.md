---
layout: post
title:  "k8s install 00 - disclean and install tools "
date:   2019-07-08 10:07:14 +0800
categories: jekyll update
---
#  k8s install 00 - disclean and install tools

# CLEAN

## delete all binary files


```
rm -vfr tools/*
```

## delete all secret files

```
rm -vf certificates/*pem
rm -vf certificates/*csr
```

## delete all config files

```
rm -vf config/*kubeconfig
```


#  INSTALL TOOLS


## INSTALL CFSSL


```
wget -q --show-progress --https-only --timestamping \
  https://pkg.cfssl.org/R1.2/cfssl_linux-amd64 \
  https://pkg.cfssl.org/R1.2/cfssljson_linux-amd64

chmod +x cfssl_linux-amd64 cfssljson_linux-amd64

sudo mv cfssl_linux-amd64 /usr/local/bin/cfssl

sudo mv cfssljson_linux-amd64 /usr/local/bin/cfssljson

```

**check cfssl version**


```
cfssl version

```

## INSTALL KUBECTL


```
wget https://storage.googleapis.com/kubernetes-release/release/v1.12.0/bin/linux/amd64/kubectl    

chmod +x kubectl   

sudo mv kubectl /usr/local/bin/   

```


**check**


```
kubectl version --client
```

