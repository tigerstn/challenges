### 1. Create a CDH Cluster on AWS

#### a. Linux setup
##### adduser training -u 3800
##### passwd training
##### groupadd skcc
##### usermod -a -G skcc training
##### chmod +w /etc/sudoers
##### vi /etc/sudoers
##### <<추가>>
##### training ALL=(ALL)   ALL

##### getent hosts 10.0.0.94 10.0.0.65 10.0.0.99 10.0.0.176 10.0.0.125
##### [root@ip-10-0-0-94 ~]# getent hosts 10.0.0.94 10.0.0.65 10.0.0.99 10.0.0.176 10.0.0.125
##### 10.0.0.94       cm.hsk.com cm
##### 10.0.0.65       ma.hsk.com ma
##### 10.0.0.99       dt1.hsk.com dt1
##### 10.0.0.176      dt2.hsk.com dt2
##### 10.0.0.125      dt3.hsk.com dt3

##### hostnamectl
##### [root@ip-10-0-0-94 ~]# hostnamectl
#####    Static hostname: cm.hsk.com
#####          Icon name: computer-vm
#####            Chassis: vm
#####         Machine ID: 3d5c05376530a2eb49e3e90576f83c5b
#####            Boot ID: cfcb628b2e4649489e5ac3dd128956cb
#####     Virtualization: kvm
#####   Operating System: CentOS Linux 7 (Core)
#####        CPE OS Name: cpe:/o:centos:centos:7
#####             Kernel: Linux 3.10.0-1127.19.1.el7.x86_64
#####       Architecture: x86-64

##### df -h
##### [root@ip-10-0-0-94 ~]# df -h
##### Filesystem      Size  Used Avail Use% Mounted on
##### devtmpfs        7.6G     0  7.6G   0% /dev
##### tmpfs           7.6G     0  7.6G   0% /dev/shm
##### tmpfs           7.6G   17M  7.6G   1% /run
##### tmpfs           7.6G     0  7.6G   0% /sys/fs/cgroup
##### /dev/nvme0n1p1  100G  1.5G   99G   2% /
##### tmpfs           1.6G     0  1.6G   0% /run/user/1000

##### yum repolist
[root@ip-10-0-0-94 ~]# yum repolist
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: d36uatko69830t.cloudfront.net
 * extras: d36uatko69830t.cloudfront.net
 * updates: d36uatko69830t.cloudfront.net
repo id                                                  repo name                                                 status
!base/7/x86_64                                           CentOS-7 - Base                                           10,070
!extras/7/x86_64                                         CentOS-7 - Extras                                            413
!updates/7/x86_64                                        CentOS-7 - Updates                                         1,134
repolist: 11,617

##### passwd |grep training
[root@ip-10-0-0-94 ~]# cat /etc/passwd |grep training
training:x:3800:3800::/home/training:/bin/bash

##### cat /etc/group |grep skcc
[root@ip-10-0-0-94 ~]# cat /etc/group |grep skcc
skcc:x:3801:training

##### getent group skcc
[root@ip-10-0-0-94 ~]# getent group skcc
skcc:x:3801:training

##### getent passwd training
[root@ip-10-0-0-94 ~]# getent passwd training
training:x:3800:3800::/home/training:/bin/bash

#### b.Install a MySQl server

##### the hostname of database server

##### the database server version
MariaDB [(none)]> select version();
+----------------+
| version()      |
+----------------+
| 5.5.65-MariaDB |
+----------------+
1 row in set (0.00 sec)

##### all the databases in the server
MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| amon               |
| hue                |
| mysql              |
| nav                |
| navms              |
| oozie              |
| performance_schema |
| rman               |
| scm                |
| sentry             |
+--------------------+
11 rows in set (0.00 sec)

