---
layout: post
title:  "blktrace、blkparse和btt使用"
date:   2019-09-17 07:01:01
categories: linux
tags: linux io
thumbnail: "assets/img/post/linux.jpg"
feature-img: "assets/img/post/linux.jpg"
excerpt: Linux IO性能分析blktrace
---

* content
{:toc}
> Linux内核中提供了跟踪Block层操作的手段，可以通过blk跟踪器、或者使用blktrace/blkparse/btt工具抓取分析、或者使用block相关trace events记录。



## 工具使用

> - blktrace 跟踪块设备的统计信息，每个CPU会有一个文件存储，
> - 通过blkparse可以将这些文件整合成一个文件来显示。
> - 通过btt分析后会发现监控数据



### 1、使用blktrace捕获trace。

> blktrace+设备名      (默认参数是  -d  <dev>)

```python
sudo blktrace /dev/nvme0n1
```

使用`Ctrl+c`结束收集结果；输出为N个文件。和测试的IO线程数目有关，为二进制文件

```bash
nvme0n1.blktrace.0
nvme0n1.blktrace.1
nvme0n1.blktrace.2
nvme0n1.blktrace.3
```

### 2、使用blkparse只是将blktrace数据转成可以人工阅读的格式

> (-i 输入   -o 标准输出   -d二进制输出)，同时会把标准输出在屏幕上进行显示

```bash
blkparse -i nvme0n1 -d nvme0n1.bin
```

由于上面的命令带有打印的功能，这样子的速度会非常慢，所以要抑制屏幕上的打印

```bash
blkparse -i nvme0n1 -d nvme0n1.bin > nvme0n1.stdout
```

### 3、使用btt分析blktrace或者是blkparse合并的单个二进制文件

```bash
btt -i nvme0n1.bin > nvme0n1.sta
```

### 4、IO延时

```
btt -i nvme0n1.bin -l nvme0n1.d2c_latency
btt -i nvme0n1.bin -q nvme0n1.q2c_latency
```



## blktrace的原理

**一个I/O请求，从应用层到底层块设备，路径如下图所示：**

<center>
<img src="https://i.loli.net/2019/11/18/9JFAr5iDoU4u2Ip.png" border="0">
</center>

**一个I/O请求进入block layer之后，可能会经历下面的过程：**

- **Remap**: 可能被DM(Device Mapper)或MD(Multiple Device, Software RAID) remap到其它设备
- **Split**: 可能会因为I/O请求与扇区边界未对齐、或者size太大而被分拆(split)成多个物理I/O
- **Merge**: 可能会因为与其它I/O请求的物理位置相邻而合并(merge)成一个I/O
- 被IO Scheduler依照调度策略发送给driver
- 被driver提交给硬件，经过HBA、电缆（光纤、网线等）、交换机（SAN或网络）、最后到达存储设备，设备完成IO请求之后再把结果发回。

**blktrace 能够记录下IO所经历的各个步骤:**

<center>
<img src="https://i.loli.net/2019/11/18/CoAp5y2zBtSwIR1.png" border="0">
</center>

**我们一起看下blktrace的输出长什么样子：**

<center>
<img src="https://i.loli.net/2019/11/18/sCAvSzlXUBxqeOj.png" border="0">
</center>

- 第一个字段：8,0 这个字段是设备号 major device ID和minor device ID。
- 第二个字段：3 表示CPU
- 第三个字段：11 序列号
- 第四个字段：0.009507758 Time Stamp是时间偏移
- 第五个字段：PID 本次IO对应的进程ID
- 第六个字段：Event，这个字段非常重要，反映了IO进行到了那一步
- 第七个字段：R表示 Read， W是Write，D表示block，B表示Barrier Operation
- 第八个字段：223490+56，表示的是起始block number 和 number of blocks，即我们常说的Offset 和 Size
- 第九个字段： 进程名

其中第六个字段非常有用：每一个字母都代表了IO请求所经历的某个阶段。

```python
Q – 即将生成IO请求
|
G – IO请求生成
|
I – IO请求进入IO Scheduler队列
|
D – IO请求进入driver
|
C – IO请求执行完毕
```

## btt输出信息

### 一、平均时间

> 第一部分中得到设备的平均延时，单位是秒

```python
==================== All Devices ====================

            ALL           MIN           AVG           MAX           N
--------------- ------------- ------------- ------------- -----------

Q2Q               0.000000001   0.000067762   4.902880182     1063492
Q2G               0.000000120   0.000000848   0.045202306     1063497
G2I               0.000000374   0.000019883   4.881094326     1063462
I2D               0.000000170   0.000001103   0.000044844     1063462
D2C               0.000067070   0.068852508   4.961615752     1063493
Q2C               0.000080046   0.068874342   4.961619413     1063493
```

说明：

- D2C: time the I/O is “active” in the driver and on the device
- Q2C: Total processing time of the I/O；客户发起请求到收到响应的时间

### 二、设备损耗

> 第二部分得到各个阶段消耗比例得到定性分析

```python
==================== Device Overhead ====================

       DEV |       Q2G       G2I       Q2M       I2D       D2C
---------- | --------- --------- --------- --------- ---------
 (259,  0) |   0.0012%   0.0289%   0.0000%   0.0016%  99.9683%
---------- | --------- --------- --------- --------- ---------
   Overall |   0.0012%   0.0289%   0.0000%   0.0016%  99.9683%
```

### 三、设备合并信息

```python
==================== Device Merge Information ====================

       DEV |       #Q       #D   Ratio |   BLKmin   BLKavg   BLKmax    Total
---------- | -------- -------- ------- | -------- -------- -------- --------
 (259,  0) |  1063497  1063497     1.0 |        8        8      256  8511432
```

>   Q表示传入的IO请求，D表示合并后发出的请求,此外还能看到平均IO块大小为8。

### 四、磁盘寻道讯息

用于显示连续队列和提交IO之间的扇区距离。NSEEKS表示提交到驱动的IO寻道次数，　MEAS表示IO之间距离，MEDIA为０表示向前和向后寻道次数一样，MODE中数值表示块IO中连续的扇区，这部分比较晦涩。

包含`Q2Q`和`D2D`两部分，`Q2Q`是到达的IO请求之间，`D2D`是驱动中处理的IO.请求

```python
==================== Device Q2Q Seek Information ====================

       DEV |          NSEEKS            MEAN          MEDIAN | MODE           
---------- | --------------- --------------- --------------- | ---------------
 (259,  0) |         1063493    1042641801.3               0 | 8(29)
---------- | --------------- --------------- --------------- | ---------------
   Overall |          NSEEKS            MEAN          MEDIAN | MODE           
   Average |         1063493    1042641801.3               0 | 8(29)

==================== Device D2D Seek Information ====================

       DEV |          NSEEKS            MEAN          MEDIAN | MODE           
---------- | --------------- --------------- --------------- | ---------------
 (259,  0) |         1063497    1042638814.0               0 | 8(29)
---------- | --------------- --------------- --------------- | ---------------
   Overall |          NSEEKS            MEAN          MEDIAN | MODE           
   Average |         1063497    1042638814.0               0 | 8(29)
```

### 五、请求队列阻塞信息

队列不是无限的的，必然存在队列阻塞情况，这个就是现实队列阻塞，不能被驱动处理。这里的统计信息就是现实不能被处理的比例，如下图：

```python
==================== Plug Information ====================

       DEV |    # Plugs # Timer Us  | % Time Q Plugged
---------- | ---------- ----------  | ----------------

       DEV |    IOs/Unp   IOs/Unp(to)
---------- | ----------   ----------
 (259,  0) |        0.0          0.0
```

### 六、队列中IO调度

有时候需要关注请求在IO调度上花费的时间。

```python
==================== Active Requests At Q Information ====================

       DEV |  Avg Reqs @ Q
---------- | -------------
 (259,  0) |           0.3
```

**详细数据**

使用--all-data或-A可以显示更详细信息。

可以显示每个设备的在各个阶段的统计数据。

### 七、活动数据文件

活动数据文件的格式容易被画图和分析，如下：

```python
# Total System
#     Total System : q activity
  0.000000000   0.0
  0.000000000   0.4
  3.255723298   0.4
  3.255723298   0.0
  8.137471916   0.0
  8.137471916   0.4
 10.881109703   0.4
 10.881109703   0.0
 15.761898578   0.0
 15.761898578   0.4
 18.934806695   0.4
 18.934806695   0.0
 ...
 ...
```

文件中数据是划分成对的，每对包含**队列信息**和**完成信息**。



## btt参数说明

```python
Usage: btt 
[ -a               | --seek-absolute ]
[ -A               | --all-data ]
[ -B <output name> | --dump-blocknos=<output name> ]
[ -d <seconds>     | --range-delta=<seconds> ]
[ -D <dev;...>     | --devices=<dev;...> ]
[ -e <exe,...>     | --exes=<exe,...>  ]
[ -h               | --help ]
[ -i <input name>  | --input-file=<input name> ]
[ -I <output name> | --iostat=<output name> ]
[ -l <output name> | --d2c-latencies=<output name> ]
[ -L <freq>        | --periodic-latencies=<freq> ]
[ -m <output name> | --seeks-per-second=<output name> ]
[ -M <dev map>     | --dev-maps=<dev map>
[ -o <output name> | --output-file=<output name> ]
[ -p <output name> | --per-io-dump=<output name> ]
[ -P <output name> | --per-io-trees=<output name> ]
[ -q <output name> | --q2c-latencies=<output name> ]
[ -Q <output name> | --active-queue-depth=<output name> ]
[ -r               | --no-remaps ]
[ -s <output name> | --seeks=<output name> ]
[ -S <interval>    | --iostat-interval=<interval> ]
[ -t <sec>         | --time-start=<sec> ]
[ -T <sec>         | --time-end=<sec> ]
[ -u <output name> | --unplug-hist=<output name> ]
[ -V               | --version ]
[ -v               | --verbose ]
[ -X               | --easy-parse-avgs ]
[ -z <output name> | --q2d-latencies=<output name> ]
[ -Z               | --do-active
```

**重点有：**

```python
[ -i <input name>  | --input-file=<input name> ]
[ -l <output name> | --d2c-latencies=<output name> ]
[ -q <output name> | --q2c-latencies=<output name> ]
```



## 参考文献

[blktrace分析IO](http://bean-li.github.io/blktrace-to-report/)

[linux中btt工具详解](https://yq.aliyun.com/articles/613509?utm_content=m_1000019749)