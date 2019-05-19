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

### Create a busybox pod that runs 'i=0; while true; do echo "$i: $(date)"; i=$((i+1)); sleep 1; done'. Check its logs


```
kubectl run busybox --image=busybox --restart=Never -- /bin/sh -c 'i=0; while true; do echo "$i: $(date)"; i=$((i+1)); sleep 1; done'
kubectl logs busybox -f # follow the logs
```

### Create a busybox pod that runs 'notexist'. Determine if there's an error (of course there is), see it. In the end, delete the pod forcefully with a 0 grace period


```
kubectl run busybox --restart=Never --image=busybox -- notexist
kubectl logs busybox # will bring nothing! container never started
kubectl describe po busybox # in the events section, you'll see the error
# also...
kubectl get events | grep -i error # you'll see the error here as well
kubectl delete po busybox --force --grace-period=0
```


### Get CPU/memory utilization for nodes (heapster must be running)

```
kubectl top nodes
```


