---
layout: post
title:  "linux文件压缩解压"
date:   2019-11-01 07:01:01
categories: linux
tags: linux 
thumbnail: "assets/img/post/linux.jpg"
feature-img: "assets/img/post/linux.jpg"
excerpt: ubuntu文件加压解压
---

* content
{:toc}


## tar

解包：

```python
tar zxvf filename.tar
```


打包：

```python
tar czvf filename.tar dirname
```

## gz

解压1：

```python
gunzip filename.gz
gzip -d filename.gz
```


压缩：

```python
gzip filename
```

## .tar.gz 和 .tgz

解压：

```python
tar zxvf filename.tar.gz
```


压缩：

```python
tar zcvf filename.tar.gz dirname
```


压缩多个文件：

```python
tar zcvf filename.tar.gz dirname1 dirname2 dirname3…..
```

## bz2命令

解压1：

```python
bzip2 -d filename.bz2
bunzip2 filename.bz2
```

压缩：

```python
bzip2 -z filename
```

## .tar.bz2

解压：

```python
tar jxvf filename.tar.bz2
```


压缩：

```python
tar jcvf filename.tar.bz2 dirname
```

## bz命令

解压1：

```python
bzip2 -d filename.bz
bunzip2 filename.bz
```

## .tar.bz

解压：

```python
tar jxvf filename.tar.bz
```



## z命令

解压：

```python
uncompress filename.z
```


压缩：

```python
compress filename
```



## .tar.z

解压：

```python
tar zxvf filename.tar.z
```


压缩：

```python
tar zcvf filename.tar.z dirname
```







## 参考文献

[linux tar.gz zip 解压缩 压缩命令](https://www.cnblogs.com/wangluochong/p/7194037.html)

[linux下各种压缩文件的加压与解压](https://blog.csdn.net/u014730842/article/details/81166594)