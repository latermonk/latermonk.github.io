---
layout: post
title:  "CKAD-exercises Notes -3  Configuration &&   Observability"

categories: jekyll update
---

# CKAD-exercises Notes 3


### Create a configMap called 'options' with the value var5=val5\. Create a new nginx pod that loads the value from variable 'var5' in an env variable called 'option'

使用kubectl explain查询env的位置：


```
k explain pods.spec --recursive |less
```
结果是：

```
containers   <[]Object>
      args      <[]string>
      command   <[]string>
      env       <[]Object>
         name   <string>
         value  <string>
         valueFrom      <Object>
            configMapKeyRef     <Object>
               key      <string>
               name     <string>
               optional <boolean>
            fieldRef    <Object>
               apiVersion       <string>
               fieldPath        <string>
            resourceFieldRef    <Object>
               containerName    <string>
               divisor  <string>
               resource <string>
            secretKeyRef        <Object>
               key      <string>
               name     <string>
               optional <boolean>
      envFrom   <[]Object>
         configMapRef   <Object>
            name        <string>
            optional    <boolean>
         prefix <string>
         secretRef      <Object>
            name        <string>
            optional    <boolean>
      image     <string>

```
## ConfigMaps

![configmap](https://raw.githubusercontent.com/latermonk/latermonk.github.io/master/_posts/_images/configmap.png)

