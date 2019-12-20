---
layout: post
title:  "btt出错：Segmentation fault (core dumped)"
date:   2019-12-18 07:01:01
categories: linux
tags: linux io
thumbnail: "assets/img/post/linux.jpg"
feature-img: "assets/img/post/linux.jpg"
excerpt: btt在使用过程中出错
---

* content
{:toc}
> 问题：在使用`blktrace`采集数据的时候，采集了一晚上，虽然晚上没有io产生，但是进程开启的时间比较久，在第二天早上使用`btt`进行trace分析的是报错了



## 错误

使用`btt`的时候报错：

```c++
Segmentation fault (core dumped)
```



## 解决

`btt`是属于`blktrace`的一个子命令，`btt`不能使用，~~猜测是一整天的开启`blktrace`导致的奔溃~~，所以想重新安装。

> 根据后续的使用来看不是blktrace的奔溃导致的（20191220补）；
>
> 是用`btt`出错，原因应该在两个地方，一个是使用方法有问题，另外一个是软件有问题；**前者**：我把`blktrace`监听了一个晚上，这个可能导致了`btt`的无法使用，我又重新把之前检测的数据使用`btt`进行分析后发现是可以正常使用的，所以可以判断`btt`本身是没有问题的，但是由于使用（检测了一个晚上）是`btt`无法进行处理的。
>
> 本文作为`blktrace`的安装继续保留。



### 源码安装

**1、下载**

blktrace代码下载地址：

```ruby
git clone git://git.kernel.dk/blktrace.git
```

或者从快照站点下载：

[http://brick.kernel.dk/snaps/](https://yq.aliyun.com/go/articleRenderRedirect?spm=a2c4e.11153940.0.0.3d84ab36Ehakqa&url=http%3A%2F%2Fbrick.kernel.dk%2Fsnaps%2F)

**2、执行命令**

```c
make
make install
```

**输出内容：**

```c++
root@tester:~/guyibin_test_gc/blktrace-1.2.0# make
...
gcc -Wall -W -O2 -g -I. -I.. -D_GNU_SOURCE -D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64 -c -o output.o output.c
...
make -C btreplay
make[1]: Entering directory '/root/guyibin_test_gc/blktrace-1.2.0/btreplay'
...
gcc -o plot.o -c -Wall -O2 -g -W -Wunused-result -D_GNU_SOURCE -D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64 plot.c
...
gcc -o fio.o -c -Wall -O2 -g -W -Wunused-result -D_GNU_SOURCE -D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64 fio.c
gcc -Wall -O2 -g -W -Wunused-result -D_GNU_SOURCE -D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64 -o iowatcher blkparse.o plot.o main.o tracers.o mpstat.o fio.o -lm -lrt
make[1]: Leaving directory '/root/guyibin_test_gc/blktrace-1.2.0/iowatcher'
```

```c
root@tester:~/guyibin_test_gc/blktrace-1.2.0# make install
install -m 755 -d /usr/local/bin
install -m 755 -d /usr/local/man/man1
install -m 755 -d /usr/local/man/man8
install -m 755 blkparse blktrace verify_blkparse blkrawverify blkiomon btrace btt/btt btreplay/btrecord btreplay/btreplay btt/bno_plot.py iowatcher/iowatcher /usr/local/bin
install -m 644 doc/*.1 /usr/local/man/man1
install -m 644 doc/*.8 /usr/local/man/man8
root@tester:~/guyibin_test_gc/blktrace-1.2.0# 
```

PS:需要安装`libaio-dev`包。如果提示需要安装就执行下面的命令，如果没有提示就不需要再次安装了

```c
sudo apt-get install libaio-dev
```

### 3、重新启动电脑

```c++
shutdown -r now
```



## 参考文献

[blktrace源码]( http://brick.kernel.dk/snaps/ )

[blktrace：git](https://git.kernel.dk/cgit/blktrace/)

