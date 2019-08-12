---
layout: post
title:  "  cp-file-to-localhost   "
date:   2019-08-17 10:07:14 +0800
categories: jekyll update
---
#  copy file from pod to localhost



```
data]# k run nginx --image=nginx --restart=Never -o yaml --dry-run -- sh -c 'sleep 3600' -o   > 3600.yaml

```

```
k apply -f 3600.yaml
```

**Copy from Pod to localhost**
```
k cp nginx-3600:etc/passwd  ./passwd 

```



