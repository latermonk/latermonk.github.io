---
layout: post
title:  "k8s  CronJob Intro "
date:   2019-07-24 10:07:14 +0800
categories: jekyll update
---
#  k8s  CronJob

**every 5 minues start a pod and do one computer **

```
kubectl run pi --schedule="0/5 * * * ?" --image=perl --restart=OnFailure -- perl -Mbignum=bpi -wle 'print bpi(2000)'
```

the cron:

```
--schedule="0/5 * * * *"

```

```
定时任务中的时间格式:
* * * * * 五个*号代表的意思分别是分，时，日，月，周

如果想每分钟都执行一次的话就采用默认的 * * * * *，
如果想每五分钟执行一次可以 */5 * * * * ，
如果是每两个小时执行一次的话

那就是 *  */2 * * *来设置;  
```

## cron-jobs

https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/



