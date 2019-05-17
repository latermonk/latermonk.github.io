---
layout: post
title:  " available docker accelerator china "

categories: jekyll update
---

# available docker accelerator china


## DaoCloud:    
https://www.daocloud.io/mirror

Linux:    

```
curl -sSL https://get.daocloud.io/daotools/set_mirror.sh | sh -s http://f1361db2.m.daocloud.io
```


## USTC
https://lug.ustc.edu.cn/wiki/mirrors/help/docker

Linux:

```
vim /etc/docker/daemon.json
```

```
{
  "registry-mirrors": ["https://docker.mirrors.ustc.edu.cn"]
}
```

