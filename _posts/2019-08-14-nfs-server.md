---
layout: post
title:  " NFS server "
date:   2019-08-14 10:07:14 +0800
categories: jekyll update
---
# NFS server 

##  install NFS server 

```
apt update 

apt install -y nfs-kernel-server   
```


```
mkdir  /opt/sfw

chmod 1777 /opt/sfw


echo software > /opt/swf/hello.txt
```

**vim  /etx/exports**


```
/opt/sfw/  *(rw,sync,no_root_squash,subtree_check)


exportsfs  -ra
```
##  install NFS client


```
apt install nfs-common
```

```
showmount -e  NFS_SERVER_IP
```

```
mount  NFS_IP:/opt/sfw    /mnt


ls -l /mnt


cat  /mnt/hello.txt
```

