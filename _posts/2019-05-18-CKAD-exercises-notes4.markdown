---
layout: post
title:  "CKAD-exercises Notes -4  Observability"

categories: jekyll update
---

# CKAD-exercises Notes 4


```
k explain pod.spec. --recursive|less
```
/liveness


```
 livenessProbe     <Object>
         exec   <Object>
            command     <[]string>
         failureThreshold       <integer>
         httpGet        <Object>
            host        <string>
            httpHeaders <[]Object>
               name     <string>
               value    <string>
            path        <string>
            port        <string>
            scheme      <string>
         initialDelaySeconds    <integer>
         periodSeconds  <integer>
         successThreshold       <integer>
         tcpSocket      <Object>
            host        <string>
            port        <string>
         timeoutSeconds <integer>
      name      <string>
      ports     <[]Object>
         containerPort  <integer>
         hostIP <string>
         hostPort       <integer>
         name   <string>
         protocol       <string>

```


