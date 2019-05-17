---
layout: post
title:  " kubectl explain "

categories: jekyll update
---

# kubectl explain

## 
execute:

```
k explain
```

```

error: You must specify the type of resource to explain. Use "kubectl api-resources" for a complete list of supported resources.

```
## 常用


```
k explain po.spec

k explain job.spec
```
### 举例：


```
k explain job.spec.completions

```

```
KIND:     Job
VERSION:  batch/v1

FIELD:    completions <integer>

DESCRIPTION:
     Specifies the desired number of successfully finished pods the job should
     be run with. Setting to nil means that the success of any pod signals the
     success of all pods, and allows parallelism to have any positive value.
     Setting to 1 means that parallelism is limited to 1 and the success of that
     pod signals the success of the job. More info:
     https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/
```


```
k explain job.spec.parallelism
```

```
KIND:     Job
VERSION:  batch/v1

FIELD:    parallelism <integer>

DESCRIPTION:
     Specifies the maximum desired number of pods the job should run at any
     given time. The actual number of pods running in steady state will be less
     than this number when ((.spec.completions - .status.successful) <
     .spec.parallelism), i.e. when the work left to do is less than max
     parallelism. More info:
     https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/

```


