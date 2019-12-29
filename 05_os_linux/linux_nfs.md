
## NFS 网络文件系统

[root@node4 ~]# df
文件系统                          1K-块     已用      可用 已用% 挂载点
/dev/mapper/centos_node2-root  52403200 21544536  30858664   42% /
devtmpfs                        1894268        0   1894268    0% /dev
tmpfs                           1913200        0   1913200    0% /dev/shm
tmpfs                           1913200     9772   1903428    1% /run
tmpfs                           1913200        0   1913200    0% /sys/fs/cgroup
/dev/sda6                       1038336   190228    848108   19% /boot
/dev/mapper/centos_node2-home 216683140  2406648 214276492    2% /home
tmpfs                            382640       12    382628    1% /run/user/42
tmpfs                            382640        0    382640    0% /run/user/1000
tmpfs                            382640        0    382640    0% /run/user/0
[root@node4 ~]# 


### Node4 检查安装

[root@node4 mac]# rpm -qa | grep -i nfs
nfs4-acl-tools-0.3.3-19.el7.x86_64
nfs-utils-1.3.0-0.61.el7.x86_64
libnfsidmap-0.25-19.el7.x86_64
[root@node4 mac]# 

[root@node4 mac]# rpm -qa | grep -i rpcbind
rpcbind-0.2.0-47.el7.x86_64
[root@node4 mac]# 

### Master/Node1/Node2/Node3 检查安装

[root@master mac]# yum install -y nfs-utils rpcbind

[root@master mac]# rpm -qa | grep -i nfs
libnfsidmap-0.25-19.el7.x86_64
nfs-utils-1.3.0-0.61.el7.x86_64
[root@master mac]# 

[root@master mac]# rpm -qa | grep -i rpcbind
rpcbind-0.2.0-47.el7.x86_64
[root@master mac]# 

### Node4 配置成NFS服务器

#### 简单配置

[root@node4 mac]# cat /etc/exports
/nfsshare *.*(rw)
[root@node4 mac]# 

#### 重启服务

[root@node4 /]# systemctl restart rpcbind && systemctl restart nfs-server
[root@node4 mac]# 

#### 确认NFS是否已经启动

[root@node4 nfsshare]# rpcinfo -p
   program vers proto   port  service
	...
    100003    3   tcp   2049  nfs
    100003    4   tcp   2049  nfs
    100227    3   tcp   2049  nfs_acl
    100003    3   udp   2049  nfs
    100003    4   udp   2049  nfs
    100227    3   udp   2049  nfs_acl
	...
	
#### 查看挂载

[root@node4 ~]# showmount -e 127.0.0.1
Export list for 127.0.0.1:
/nfsshare *.*
[root@node4 ~]# 


### Master 配置NFS客户端

#### 挂载

[root@master /]# mount -t nfs -o rw 192.168.0.112:/nfsshare /nfsdata
[root@master /]# 

[root@master nfsdata]# touch s
touch: cannot touch ‘s’: Permission denied
[root@master nfsdata]# 

#### 问题解决

返回到Node4, 检查mac所在的组ID和用户ID

[root@node4 mac]# id mac
uid=1000(mac) gid=1000(mac) 组=1000(mac),10(wheel),1001(docker)
[root@node4 mac]# 


修改为指定的用户和用户组

[root@node4 /]# vi /etc/exports
/nfsshare *(rw,all_squash,sync,anonuid=1000,anongid=1000)
[root@node4 mac]# 

[root@node4 /]# chown -R mac:mac /nfsshare
[root@node4 mac]# 

重启NFS服务

[root@node4 /]# systemctl restart rpcbind && systemctl restart nfs-server
[root@node4 mac]# 

#### 其他节点的挂载

[root@node2 ~]# yum install -y nfs-utils
[root@node2 ~]# 

[root@node2 ~]# rpm -qa | grep -i nfs
libnfsidmap-0.25-19.el7.x86_64
nfs-utils-1.3.0-0.61.el7.x86_64
[root@node2 ~]# 

[root@node2 ~]# rpm -qa | grep -i rpcbind
rpcbind-0.2.0-47.el7.x86_64
[root@node2 ~]# 

[root@node2 ~]# mkdir /nfsdata
[root@node2 ~]# chown -R mac:mac /nfsshare
[root@node2 ~]# 

[root@node2 ~]# mount -t nfs -o rw 192.168.0.112:/nfsshare /nfsdata
[root@node2 ~]# systemctl restart rpcbind
[root@node2 ~]# 


#### 利用NFS共享文件

[mac@node4 nfsshare]$ docker save -o mysql.tar mysql:5.6
[mac@node2 nfsdata] $ docker load < mysql.tar


#### 解决MYSQL编排的问题


[root@node4 mysql-pv]# more /etc/exports
#/nfsshare *(rw,all_squash,sync,anonuid=1000,anongid=1000)
/nfsshare 192.168.0.0/24(insecure,rw,sync,no_root_squash,fsid=0)
[root@node4 mysql-pv]# 


