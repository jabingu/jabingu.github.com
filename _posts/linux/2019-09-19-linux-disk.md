---
layout: post
title:  "ubuntu系统增加新的硬盘"
date:   2019-09-19 07:01:01
categories: linux
tags: linux 
thumbnail: "assets/img/post/linux.jpg"
feature-img: "assets/img/post/linux.jpg"
excerpt: ubuntu系统增加新的硬盘
---

* content
{:toc}
> 我们在使用 Ubuntu 作为服务器系统时，会有一个常用的操作情景，就是为服务器添加新硬盘。



## 格式化分区

我们可以使用 `mkfs` 命令格式化分区，具体命令如下：

```python
root@tester:~# sudo mkfs -t ext4 /dev/sdb
mke2fs 1.42.13 (17-May-2015)
Found a gpt partition table in /dev/sdb
Proceed anyway? (y,n) y
Creating filesystem with 244190646 4k blocks and 61054976 inodes
Filesystem UUID: 81a6b2a7-d220-48be-acd1-a4c4beb304e2
Superblock backups stored on blocks: 
	32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208, 
	4096000, 7962624, 11239424, 20480000, 23887872, 71663616, 78675968, 
	102400000, 214990848

Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done     
```

## 挂载分区

分区我们需要先创建一个目录，然后再把这个新分区挂载到目录上。具体操作如下：

```python
# 我们在 ~ 目录下创建一个 extenddisk 的目录，并将新分区挂载到这里
mkdir ~/newdisk    
sudo mount /dev/sdb ~/newdisk    
```

挂载后，我们再通过 `df -l` 命令查看是否挂载成功：

```python
root@tester:~# df -l
Filesystem     1K-blocks     Used Available Use% Mounted on
udev             3931840        0   3931840   0% /dev
tmpfs             790680     1140    789540   1% /run
/dev/sda1      114797128 22697716  86245000  21% /
tmpfs            3953388      188   3953200   1% /dev/shm
tmpfs               5120        4      5116   1% /run/lock
tmpfs            3953388        0   3953388   0% /sys/fs/cgroup
tmpfs             790680       20    790660   1% /run/user/108
tmpfs             790680        0    790680   0% /run/user/0
/dev/sdb       961303584    73364 912375708   1% /root/newdisk    
```

这里可以看到最后一条记录，我们的`sdb`已经挂载带`extenddisk`文件中了

## 开机自动挂载设置

查看磁盘的UUID编号

```python
root@tester:~# sudo blkid
/dev/sda1: UUID="9354be21-7668-4faf-910e-0640ac2ec8c2" TYPE="ext4" PARTUUID="311cea07-01"
/dev/sdb: UUID="16be2f96-3169-4be1-b168-c6bfffd9aef1" TYPE="ext4"
```

在`/etc/fstab`配置文件中添加挂载信息：

```python
sudo vim /etc/fstab
```

> UUID="16be2f96-3169-4be1-b168-c6bfffd9aef1"     /root/newdisk    ext4     defaults       0 0





## 参考文献

[Ubuntu环境下挂载新硬盘](https://blog.51cto.com/12348890/2092339)

[Ubuntu 挂载新硬盘](https://www.jianshu.com/p/ac37d1f6fdeb)