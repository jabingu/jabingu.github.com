---
layout: post
title:  "EuroSys 2019"
date:   2019-06-25 7:30:00
categories: conference
tags: conference EuroSys
excerpt: 记录EuroSys 2019会议文章的摘要和主要内容，方便日后的检索。
---

* content
{:toc}
> 死亡是活过的生命，生活是在路上的死亡。
>
> <p align="right">——博尔赫斯　　</p>



**目录：**

> Security  
> Exploiting CPU Architecture  
> OS Kernel  
> Storage Systems  
> Datacenter Systems  
> Networking  
> Big Data   
> Distributed Systems  
> Cloud Computing  
> Programming Languages and Verification  
> Systems for Machine Learning  



## Security





## Exploiting CPU Architecture





## OS Kernel



## Storage Systems

**Project Almanac: A Time-Traveling Solid-State Drive.**

> Xiaohao Wang, Yifan Yuan, You Zhou, Chance C. Coats, Jian Huang:
>
> Systems and Platform Research Group, Department of Electrical and Computer Engineering, **University of Illinois at Urbana-Champaign**

Preserving the history of storage states is critical to ensuring system reliability and security. It facilitates system functions such as debugging, data recovery, and forensics. Existing software-based approaches like data journaling, logging, and backups not only introduce performance and storage cost, but also are vulnerable to malware attacks, as adversaries can obtain kernel privileges to terminate or destroy them.

In this paper, we present Project Almanac, which includes (1) a time-travel solid-state drive (SSD) named **TimeSSD** that retains a history of storage states in hardware for a window of time, and (2) a toolkit named TimeKits that provides <u>storage-state query</u> and <u>rollback functions</u>. TimeSSD tracks the history of storage states in the hardware device, without relying on explicit backups, by exploiting the property that the flash retains old copies of data when they are updated or deleted. We implement TimeSSD with a programmable SSD and develop TimeKits for several typical system applications. Experiments, with a variety of real-world case studies, demonstrate that TimeSSD can retain all the storage states for eight weeks, with negligible performance overhead, while providing the device-level time-travel property.

------

**ShieldStore: Shielded In-memory Key-value Storage with SGX**

> Taehoon Kim, Joongun Park, Jaewook Woo, Seungheun Jeon, Jaehyuk Huh
>
> School of Computing, **KAIST**

The shielded computation of hardware-based trusted execution environments such as **Intel Software Guard Extensions (SGX)** can provide secure cloud computing on remote systems under untrusted privileged system software. However, hardware overheads for securing protected memory restrict its capacity to a modest size of several tens of megabytes, and more demands for protected memory beyond the limit cause costly demand paging. Although one of the widely used applications benefiting from the enhanced security of SGX, is the in-memory key-value store, its memory requirements are far larger than the protected memory limit. Furthermore, the main data structures commonly use fine-grained data items such as pointers and keys, which do not match well with the coarse-grained paging of the SGX memory extension technique. To overcome the memory restriction, this paper **proposes a new in-memory key-value store designed** for SGX with application-specific data security management. The proposed key-value store, called **ShieldStore**, maintains the main data structures in unprotected memory with each key-value pair individually encrypted and integrity-protected by its secure component running inside an enclave. Based on the enclave protection by SGX, ShieldStore provides secure data operations much more efficiently than the baseline SGX key-value store, achieving 8--11 times higher throughput with 1 thread, and 24--30 times higher throughput with 4 threads.

 **In-memory**；**索引**

------

**URSA: Hybrid Block Storage for Cloud-Scale Virtual Disks.** 

> Huiba Li	**Alibaba**, Beijing, China
> Yiming Zhang	NiceX Lab, PDL, NUDT, Changsha, Hunan, China
> Dongsheng Li	NUDT, Changsha, Hunan, China
> Zhiming Zhang	mos.meituan.com, Beijing, China
> Shengyun Liu	NUDT, Changsha, Hunan, China
> Peng Huang	Johns Hopkins University, Baltimore, Maryland, USA
> Zheng Qin	NUDT, Changsha, Hunan, China
> Kai Chen	HKUST, Hong Kong, China
> Yongqiang Xiong	Microsoft, Beijing, China

This paper presents **URSA**, a **hybrid block store** that provides virtual disks for various applications to run efficiently on **cloud VMs**. Trace analysis shows that the I/O patterns served by block storage have limited locality to exploit. Therefore, instead of using SSDs as a cache layer, URSA proposes an **SSD-HDD-hybrid storage structure** that directly <u>stores primary replicas on SSDs</u> and <u>replicates backup replicas on HDDs</u>, using journals to bridge the performance gap between SSDs and HDDs. URSA integrates the hybrid structure with designs for high reliability, scalability, and availability. Experiments show that URSA in its hybrid mode achieves almost the same performance as in its SSD-only mode (storing all replicas on SSDs), and outperforms other block stores (Ceph and Sheepdog) even in their SSD-only mode while achieving much higher CPU efficiency (performance per core). We also discuss some practical issues in our deployment.

------

**VStore: A Data Store for Analytics on Large Videos**

> Tiantu Xu, Luis Materon Botelho, Felix Xiaozhu Lin
>
> Purdue ECE

We present **VStore**, a data store for supporting fast, resource-efficient analytics over large archival **videos**. VStore manages video ingestion, storage, retrieval, and consumption. It controls video formats along the video data path. It is challenged by i) the huge combinatorial space of video format knobs; ii) the complex impacts of these knobs and their high profiling cost; iii) optimizing for multiple resource types. It explores an idea called **backward derivation of configuration**: in the opposite direction along the video data path, VStore passes the video quantity and quality expected by analytics backward to retrieval, to storage, and to ingestion. In this process, VStore derives an optimal set of video formats, optimizing for different resources in a progressive manner.

VStore automatically derives large, complex configurations consisting of more than one hundred knobs over tens of video formats. In response to queries, VStore selects video formats catering to the executed operators and the target accuracy. It streams video data from disks through decoder to operators. It runs queries as fast as 362x of video realtime.

## **Datacenter Systems**

**Managing Tail Latency in Datacenter-Scale File Systems Under Production Constraints.**

> Pulkit A. Misra	Duke University
> María F. Borge	University of Sydney
> Íñigo Goiri	Microsoft Research
> Alvin R. Lebeck	Duke University
> Willy Zwaenepoel	University of Sydney and EPFL
> Ricardo Bianchini	Microsoft Research

**Distributed** file systems often exhibit high **tail** latencies, especially in large-scale datacenters and in the presence of competing (and possibly higher priority) workloads. This paper introduces techniques for **managing tail latencies** in these systems, while addressing the practical challenges inherent in production datacenters (e.g., hardware heterogeneity, interference from other workloads, the need to maximize simplicity and maintainability). We implement our techniques in a scalable distributed file system (an extension of **HDFS**) used in production at Microsoft. Our evaluation uses 70k servers in 3 datacenters, and shows that our techniques <u>reduce tail latency significantly for production workloads</u>.

----

**Wormhole: A Fast Ordered Index for In-memory Data Management**

> Xingbo Wu	University of Illinois at Chicago
> Fan Ni	University of Texas at Arlington
> **Song Jiang**	University of Texas at Arlington

**In-memory** data management systems, such as key-value stores, have become an essential infrastructure in today's big-data processing and cloud computing. They rely on efficient index structures to access data. While unordered indexes, such as hash tables, can perform point search with O(1) time, they cannot be used in many scenarios where range queries must be supported. Many ordered indexes, such as B+ tree and skip list, have a O(log N) lookup cost, where N is number of keys in an index. For an ordered index hosting billions of keys, it may take more than 30 key-comparisons in a lookup, which is an order of magnitude more expensive than that on a hash table. With availability of large memory and fast network in today's data centers, this O(log N) time is taking a heavy toll on applications that rely on ordered indexes.

In this paper we introduce a new ordered index structure, named **Wormhole**, that takes **O(log L)** worst-case time for looking up a key with a <u>length of L</u>. The low cost is achieved by simultaneously leveraging strengths of three indexing structures, namely **hash table, prefix tree, and B+ tree**, to orchestrate a single fast ordered index. Wormhole's range operations can be performed by a linear scan of a list after an initial lookup. This improvement of access efficiency does not come at a price of compromised space efficiency. Instead, Wormhole's index space is comparable to those of B+ tree and skip list. Experiment results show that Wormhole outperforms skip list, B+ tree, ART, and Masstree by up to 8.4x, 4.9x, 4.3x, and 6.6x in terms of key lookup throughput, respectively.

in-memory；**索引**

----

**Scalable RDMA RPC on Reliable Connection with Efficient Resource Sharing.**

> Youmin Chen, Youyou Lu, Jiwu Shu
>
> Tsinghua University

**RDMA** provides extremely low latency and high bandwidth to distributed systems. Unfortunately, it fails to scale and suffers from performance degradation when transferring data to an increasing number of targets on Reliable Connection (RC). We observe that the above scalability issue has its root in the resource contention in the NIC cache, the CPU cache and the memory of each server. In this paper, we propose **ScaleRPC**, an efficient RPC primitive using one-sided RDMA verbs on reliable connection to provide scalable performance. To effectively alleviate the resource contention, ScaleRPC introduces 1) connection grouping to organize the network connections into groups, so as to balance the saturation and thrashing of the NIC cache; 2) virtualized mapping to enable a single message pool to be shared by different groups of connections, which reduces CPU cache misses and improve memory utilization. Such scalable connection management provides substantial performance benefits: By deploying ScaleRPC both in a distributed file system and a distributed transactional system, we observe that it achieves high scalability and respectively improves performance by up to 90% and 160% for metadata accessing and SmallBank transaction processing.

----

**FlyMC: Highly Scalable Testing of Complex Interleavings in Distributed Systems**

> Jeffrey F. Lukman	University of Chicago
> Huan Ke	University of Chicago
> Cesar A. Stuardo	University of Chicago
> Riza O. Suminto	University of Chicago
> Daniar H. Kurniawan	University of Chicago
> Dikaimin Simon	Surya University
> Satria Priambada	Bandung Institute of Technology
> Chen Tian	Huawei US R&D Center
> Feng Ye	Huawei US R&D Center
> Tanakorn Leesatapornwongsa	Samsung Research America
> Aarti Gupta	Princeton University
> Shan Lu	University of Chicago
> Haryadi S. Gunawi	University of Chicago

We present a fast and scalable **testing approach** for datacenter/cloud systems such as <u>Cassandra, Hadoop, Spark, and ZooKeeper</u>. The uniqueness of our approach is in its ability to **overcome the path/state-space explosion problem** in testing workloads with complex interleavings of messages and faults. We introduce three powerful algorithms: **state symmetry**, **event independence**, and **parallel flips**, which collectively makes our approach on average 16x (up to 78x) faster than other state-of-the-art solutions. We have integrated our techniques with 8 popular datacenter systems, successfully reproduced 12 old bugs, and found 10 new bugs --- all were done without random walks or manual checkpoints.

## **Networking**



## **Big Data**





## **Distributed Systems**





## **Cloud Computing**

**Resource Deflation: A New Approach For Transient Resource Reclamation**

> Prateek Sharma	Indiana University
> Ahmed Ali-Eldin	University of Massachusetts Amherst
> Prashant Shenoy	University of Massachusetts Amherst

Data centers and clouds are increasingly offering low-cost computational resources in the form of transient virtual machines. Whenever demand for computational resources exceeds their availability, transient resources can reclaimed by **preempting the transient VMs**. Conventionally, these transient VMs are used by low-priority applications that can tolerate the disruption caused by preemptions.

In this paper we propose an alternative approach for reclaiming resources, called **resource deflation**. Resource deflation allows applications to dynamically shrink (and expand) in response to resource pressure, instead of being preempted outright. Deflatable VMs allow applications <u>to continue running even under resource pressure</u>, and increase the utility of low-priority transient resources. Deflation uses a dynamic, **multi-level cascading** reclamation technique that allows applications, operating systems, and hypervisors to implement their own policies for handling resource pressure. For distributed data processing, **machine learning**, and deep neural network training, our multi-level approach reduces the performance degradation by up to 2x compared to existing preemption-based approaches. When deflatable VMs are deployed on a cluster, our policies allow up to 1.6x utilization without the risk of preemption.

------

**GrandSLAm: Guaranteeing SLAs for Jobs in Microservices Execution Frameworks**

> Ram Srivatsa Kannan	**University of Michigan**, Ann Arbor
> Lavanya Subramanian	Facebook and Intel Labs
> Ashwin Raju	University of Texas at Arlington
> Jeongseob Ahn	Ajou University
> Jason Mars	University of Michigan, Ann Arbor
> Lingjia Tang	University of Michigan, Ann Arbor

The **microservice** architecture has dramatically reduced user effort in adopting and maintaining servers by providing a catalog of functions as services that can be used as building blocks to construct applications. This has enabled datacenter operators to look at managing datacenter hosting microservices quite differently from traditional infrastructures. Such a paradigm shift calls for a need to rethink resource management strategies employed in such execution environments. We observe that the visibility enabled by a microservices execution framework can be exploited to achieve high throughput and resource utilization while still meeting Service Level Agreements, especially in multi-tenant execution scenarios.

In this study, we present **GrandSLAm**, a <u>microservice execution framework</u> that improves utilization of datacenters hosting microservices. GrandSLAm estimates time of completion of requests propagating through individual microservice stages within an application. It then leverages this estimate to drive a runtime system that dynamically batches and reorders requests at each microservice in a manner where individual jobs meet their respective target latency while achieving high throughput. GrandSLAm significantly increases throughput by up to 3x compared to the our baseline, without violating SLAs for a wide range of real-world AI and ML applications.

**Hourglass: Leveraging Transient Resources for Time-Constrained Graph Processing in the Cloud**

> Pedro Joaquim, Manuel Bravo, Luís E. T. Rodrigues, Miguel Matos
>
> INESC-ID, Instituto Superior Técnico, Universidade de Lisboa, Portugal

This paper addresses the key problems that emerge when one attempts to use transient resources to reduce the cost of running **time-constrained jobs** in the cloud. Previous works fail to address these problems and are either not able to offer significant savings or miss termination deadlines. First, the fact that transient resources can be evicted, requiring the job to be re-started (even if not from scratch) may lead provisioning policies to fall-back to expensive on-demand configurations more often than desirable, or even to miss deadlines. Second, when a job is restarted, the new configuration can be different from the previous, which might make eviction recovery costly, e.g., transferring the state of graph data between the old and new configurations. We present **HOURGLASS**, a system that addresses these issues by combining two novel techniques: **a slack-aware provisioning strategy** that selects configurations considering the remaining time before the job's termination deadline, and **a fast reload mechanism** to quickly recover from evictions. By switching to an on-demand configuration when (but only if) the target deadline is at risk of not being met, we are able to obtain significant cost savings while always meeting the deadlines. Our results show that, unlike previous work, HOURGLASS is able to significantly reduce the operating costs in the order of 60-70% while guaranteeing that deadlines are met.

云环境下的任务调度

------

**Efficient, Consistent Distributed Computation with Predictive Treaties**

> Tom Magrino	Cornell University, Ithaca, NY, USA
> Jed Liu	Barefoot Networks Ithaca, NY, USA
> Nate Foster	Cornell University, Ithaca, NY, USA
> Johannes Gehrke	Microsoft Corporation Redmond, WA, USA
> Andrew C. Myers	Cornell University, Ithaca, NY, USA

To achieve good performance, modern applications often partition their state across multiple geographically distributed nodes. While this approach reduces latency in the common case, it can be challenging for programmers to use correctly, especially in applications that require strong consistency. We introduce predictive treaties, a mechanism that can significantly reduce distributed coordination without losing strong consistency. The central insight behind our approach is that many **computations can be expressed in terms of predicates over distributed state that can be partitioned and enforced locally**. Predictive treaties improve on previous work by allowing the locally enforced predicates to depend on time. Intuitively, by predicting the evolution of system state, coordination can be significantly reduced compared to static approaches. We implemented predictive treaties in a distributed system that exposes them in an intuitive programming model. We evaluate performance on several benchmarks, including TPC-C, showing that predictive treaties can significantly increase performance by orders of magnitude and can even outperform customized algorithms.

## **Programming Languages and Verification**





## **Systems for Machine Learning**

