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


## securityContext


```
 securityContext: # insert this line
    runAsUser: 101 # UID for the user




```

```
securityContext: # insert this line
      capabilities: # and this
        add: ["NET_ADMIN", "SYS_TIME"] # this as well
```


### 查看

```
 k explain pod.spec.securityContext --recursive |less
```
result：

```
KIND:     Pod
VERSION:  v1

RESOURCE: securityContext <Object>

DESCRIPTION:
     SecurityContext holds pod-level security attributes and common container
     settings. Optional: Defaults to empty. See type description for default
     values of each field.

     PodSecurityContext holds pod-level security attributes and common container
     settings. Some fields are also present in container.securityContext. Field
     values of container.securityContext take precedence over field values of
     PodSecurityContext.

FIELDS:
   fsGroup      <integer>
   runAsGroup   <integer>
   runAsNonRoot <boolean>
   runAsUser    <integer>
   seLinuxOptions       <Object>
      level     <string>
      role      <string>
      type      <string>
      user      <string>
   supplementalGroups   <[]integer>
   sysctls      <[]Object>
      name      <string>
      value     <string>
```
## Secret 

注意关键字：  generic
```
Create a secret called mysecret with the values password=mypass
```

```
kubectl create secret generic mysecret --from-literal=password=mypass
```
### Get the value of mysecret2

```
kubectl get secret mysecret2 -o yaml --export
```


```
echo YWRtaW4K | base64 -d # shows 'admin'
```


### Create an nginx pod that mounts the secret mysecret2 in a volume on path /etc/foo


```
k explain pods.spec.volumes --recursive |less
```


```
 secret       <Object>
      defaultMode       <integer>
      items     <[]Object>
         key    <string>
         mode   <integer>
         path   <string>
      optional  <boolean>
      secretName        <string>

```
最终结果：

```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
spec:
  volumes: # specify the volumes
  - name: foo # this name will be used for reference inside the container
    secret: # we want a secret
      secretName: mysecret2 # name of the secret - this must already exist on pod creation
  containers:
  - image: nginx
    imagePullPolicy: IfNotPresent
    name: nginx
    resources: {}
    volumeMounts: # our volume mounts
    - name: foo # name on pod.spec.volumes
      mountPath: /etc/foo #our mount path
  dnsPolicy: ClusterFirst
  restartPolicy: Never
status: {}
```
### Delete the pod you just created and mount the variable 'username' from secret mysecret2 onto a new nginx pod in env variable called 'USERNAME'


```
？？？

```

![Configuration ](https://raw.githubusercontent.com/latermonk/latermonk.github.io/master/_posts/_images//Configuration%20.png)

