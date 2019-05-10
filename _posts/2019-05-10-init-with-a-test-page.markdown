---
layout: post
title:  "This is a test page!!!"
date:   2019-05-10 09:07:14 +0800
categories: jekyll update
---
Hello ,World ,This is a test page !!!

```
controllers/job.yaml 

apiVersion: batch/v1
kind: Job
metadata:
  name: pi
spec:
  template:
    spec:
      containers:
      - name: pi
        image: perl
        command: ["perl",  "-Mbignum=bpi", "-wle", "print bpi(2000)"]
      restartPolicy: Never
  backoffLimit: 4
```

# TEST PAGE