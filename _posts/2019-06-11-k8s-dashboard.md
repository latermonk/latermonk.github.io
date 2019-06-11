---
layout: post
title:  "k8s dash-board"
date:   2019-06-11 09:07:14 +0800
categories: jekyll update
---


使用代理访问 kube-dashboard

**设置代理**
```
`kubectl proxy --address='0.0.0.0' --accept-hosts='^*$'`
```

**访问kube-dashboard**

[http://x.x.x.x:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy](http://x.x.x.x:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy)
```
http://x.x.x.x:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy
```

