---
layout: post
title:  "ICCD 2018"
date:   2019-06-25 7:30:00
categories: conference
tags: conference ICCD
excerpt: 记录ICCD 2018会议文章的摘要和主要内容，方便日后的检索。
---

* content
{:toc}
> 死亡是活过的生命，生活是在路上的死亡。
>
> <p align="right">——博尔赫斯　　</p>



**目录：**

> Session 1: Best Papers Session  
> Session 2A: SSD  
> Session 2B: Side Channels  
> Session 3A: Security and Capability  
> Session 3B: Microarchitecture  
> Session 4A: Logic and Circuit Design 1  
> Session 4B: Design Automation  
> Session 5A: Novel Architectures  
> Session 5B: Memory 1  
> Session 6A: Memory 2  
> Session 6B: Logic and Circuit Design 2  
> Session 7A: Accelerators and GPUs  
> Session 7B: Potpouri 1  
> Session 8A: NVM  
> Session 8B: Test and Verification  
> Session 9A: Network on Chip and Synchronization  
> Session 9B: Potpouri 2  
> Session 10A: File System and Cloud  
> Session 10B: FPGA and Machine Learning  



## **1: Best Papers Session**

**Composable Template Attacks Using Templates for Individual Architectural Components**

> ​	Bozhi Liu, Roman Lysecky, Janet Meiling Wang Roveda

With embedded systems and IoT devices being widely deployed nowadays, their **security** becomes a major concern. Among all possible attacks, **side channel attacks (SCA)** represent a major source of threats. For power side channels, template attacks have been proven to be efficient and widely applicable. Traditional template attacks require physical access to an identical target device for extensive profiling to construct the attack template. In this paper, we present a composable template attack that relaxes this requirement by constructing the attack template as a composition of templates from individual architectural components, including processor, caches, and memories. The proposed approach enables an attacker to construct a template using only information of a system's components and device models thereof.

----

**Thermal-Aware 3D Symmetrical Buffered Clock Tree Synthesis**

> ​	Deok Keun Oh, Mu Jun Choi, Juho Kim

The semiconductor industry has accepted **three dimensional integrated circuits (3D ICs)** as a possible solution to address speed and power management problems. In addition, 3D ICs have recently demonstrated a huge potential in reducing wire length and increasing the density of a chip. However, the growing density in chips such as TSV-based 3D ICs has brought increased temperature on chip and temperature gradients depending on location. Thus, through silicon via (TSV)-based 3D clock tree synthesis (CTS) causes **thermal problem** leading to large clock skew. We propose a novel 3D symmetrical buffered clock tree synthesis considering thermal variation. First, 3D abstract tree topology based on nearest neighbor selection with median cost (3D-NNM) is constructed by pairing sinks that have similar power consumption. Second, the layer assignment of internal nodes is determined for uniform TSV distribution. Third, in thermal-aware 3D deferred merging embedding (DME), the exact location of TSV is determined and wire routing/buffer insertion are performed after thermal profiles based on grid are obtained. The proposed method is verified using a 45nm process technology and utilized a predictive technology model (PTM) with HSPICE. Also, our CTS is evaluated for IBM and ISPD'09 benchmarks with no blockages. In experimental results, we can achieve average 18% of clock skew reduction compared to existing thermal-aware 3D CTS. Therefore, thermal-aware 3D symmetrical buffered clock tree synthesis presented in this work is very efficient for circuit reliability.

----

**Low-Overhead Microarchitectural Patching for Multicore Memory Subsystems**

> ​	Doowon Lee, Opeoluwa Matthews, Valeria Bertacco

In this work, we present **μMemPatch**, a comprehensive, efficient patching solution to overcome escaped design flaws in multicore memory subsystems at runtime. Unlike conventional microcode patching, μMemPatch strives to accurately pinpoint bug-prone microarchitectural states at runtime, by using a small programmable-logic fabric. μMemPatch comprises two main components: **a bug-anticipation module** and **a bug-elusion module**. The bug-anticipation module tracks, at runtime, the progress of microarchitectural events related to memory operations. Specifically, we model event sequences as finite state machines (FSM), where some of the FSM states represent bug-prone microarchitectural states. Upon detection of a bug-prone state, the bug-elusion module limits reorderings of instructions or memory accesses, so as to avoid falling into the bug state. We propose a few different bug-elusion methods, including squashing instructions, delaying cache evictions, and dynamically inserting fence operations. We implemented μMemPatch in a cycle-accurate full-system **simulator**. We then embedded eleven design bugs that span a wide range of bug types, which had been disclosed in product errata documents. Our evaluation with an in-house micro-benchmark suite and the SPLASH-2 suite shows that μMemPatch's bug-elusion methods successfully bypass all bugs at a performance impact of less than 1% on average (SPLASH-2). The area overhead in our setup is approximately 6% for an ARM Cortex-A9 core on average, over all bugs we considered.

----

**Power Grab in Aggressively Provisioned Data Centers: What is the Risk and What Can Be Done About It**

> ​	Xiaofeng Hou, Luoyao Hao, Chao Li, Quan Chen, Wenli Zheng, Minyi Guo

Aggressively provisioned **data centers** achieve great cost savings by over-committing the very expensive **power** distribution infrastructure. However, <u>existing proposals</u> for managing load power demand in such a data center are largely <u>utilization-driven</u>, overlooking power-related interferences among users. An important observation is that some tasks can impact existing power budget management framework and disrupt normal operation by taking away the precious public power capacity. This vulnerability exposes data centers to a new type of risk that we call power grab, which is essentially hostile power resource competition. It could worsen the performance-utilization tradeoff in a power-constrained computing environment. Anticipating a growing case for power-oriented competition, we propose **CFP**, a resilient power capacity management frame-work for improving the <u>fairness</u> and service <u>quality</u> in scale-out data centers. Our solution features a market-based power re-source allocation and billing scheme that involves users in the loop. It allows the data center to bypass the formidable task of identifying malicious users and defend against power grab with reward and punishment incentives. We build a proof-of-concept system and also evaluate our design with realistic Google cluster traces. Compared to prior arts, CFP can increase the average performance-cost ratio by 1.8X. It can boost the total throughput in an APDC by 15% under severe power contention. Our design allows scale-out data centers to safely exploit the benefits that power over-subscription may provide, with minor overhead.

**数据中心**；**能耗调度**

## 2A: SSD

**Pensieve: a Machine Learning Assisted SSD Layer for Extending the Lifetime**

> ​	Te I, Murtuza Lokhandwala, Yu-Ching Hu, Hung-Wei Tseng

As the capacity per unit cost dropping, flash-based SSDs become popular in various computing scenarios. However, the restricted program-erase cycles still severely limit cost-effectiveness of flash-based storage solutions. This paper proposes **Pensieve**, a **machine-learning** assisted SSD firmware layer that transparently helps <u>reduce the demand for programs and erases</u>. Pensieve efficiently <u>classifies writing data into different compression categories without hints from software systems</u>. Data with the same category may use a shared dictionary to **compress** the content, allowing Pensieve to further avoid duplications. As Pensieve does not require any modification in the software stack, Pensieve is compatible with existing applications, file systems and operating systems. With modern SSD architectures, implementing a Pensieve-compliant SSD also requires no additional hardware, providing a drop-in upgrade for existing storage systems. The experimental result on our prototype Pensieve SSD shows that Pensieve can reduce the amount of program operations by 19%, while delivering competitive performance.

**机器学习**；**ssd**；**数据压缩**

----

**Selective Compression Scheme for Read Performance Improvement on Flash Devices**

> ​	Qiao Li, Liang Shi, Riwei Pan, Cheng Ji, Xiaoqiang Li, Chun Jason Xue

The increasing density and capacity of NAND flash memory leads to degraded reliability. To address the **reliability** issue, **low-density parity-check code (LDPC)** has been deployed in NAND flash memories due to its strong error correction capability. The drawback of LDPC is that, to correct data with high raw bit error rate (RBER), read latency will be amplified. To improve read performance, this paper proposes to apply <u>lossless compression to reduce RBER on data pages</u>. However, compression and decompression incur time overheads. Compressing all the data pages for RBER reduction will degrade write performance. In addition, the variation of compression ratio leads to variation of RBER reduction, thus varied read latency reduction. In this work, a selective data compression scheme is proposed for read performance improvement. Both read frequency and compression ratio of data are taken into consideration. Data in a flash page with high read frequency and good compressibility are prioritized for compression. Experimental results show that the proposed scheme can improve read performance by 42% on average, without impacting write performance.

**数据压缩**；**LDPC**

----

**OSPADA: One-Shot Programming Aware Data Allocation Policy to Improve 3D NAND Flash Read Performance**

> **Fei Wu**, Zuo Lu, You Zhou, Xubin He, Zhi-hu Tan, **Changsheng Xie**:

Charge trap (CT) based **3D NAND flash** is predominating the flash storage market due to higher density, better performance and endurance than planar flash. CT-based 3D flash programs multiple pages in a word line at a time, called <u>one-shot programming</u>, unlike planar flash which programs one page at a time. Solid state drives (SSDs) utilize the internal parallelism to improve the performance, but one-shot programming is likely to program logically sequential data into one parallel unit (i.e., a plane) and thus degrades the read parallelism. In this paper, we propose a <u>*one-shot programming aware data allocation policy*</u>, called **OSPADA**, to improve the read performance of CT flash based SSDs by enhancing read parallelism. OSPADA reorders written data to distribute logically sequential data into different parallel units using the distance aware round-robin strategy. Experimental results show that OSPADA improves the read performance by up to 22.8% compared with traditional dynamic data allocation policies.

由于读写单元和擦除的单元的大小问题

----

**Cap: Exploiting Data Correlations to Improve the Performance and Endurance of SSD RAID**

> ​	Gaoxiang Xu, Zhipeng Tan, Dan Feng, Yifeng Zhu, Xinyan Zhang, Jie Xu

**Parity-based RAID** provides system-level fault tolerance. However, parity updates caused by small writes introduce lots of extra I/Os, degrading I/O performance and wearing SSDs out. It has been proposed to use **Non-Volatile Memory (NVM) as a parity cache** on an SSD **RAID** to postpone parity updates until the whole stripe has been updated. However, this often fails because of skewed distribution of <u>hot data chunks within a stripe.</u> In real workloads, it is often difficult to achieve a full-stripe update even after a long delay. In this paper, we propose a <u>*Correlation aware parity caching scheme*</u>, called **Cap**, for SSD-based RAIDs. The key idea behind Cap is to periodically reconstruct correlated hot data chunks into a new stripe. Since these data chunks have a strong correlation, they tend to be updated together within a short time span. This co-update within a stripe more efficiently utilizes the parity cache to convert partial-stripe updates into a full-stripe update. We have implemented Cap on a RAID-5 SSD array in Linux Kernel 4.3. Experimental results show that Cap improves the I/O bandwidth by 54%~145% compared with the Linux software RAID. Compared with the state-of-the-art parity caching scheme PPC, Cap improves the I/O bandwidth by 14%~31%.

RAID;data chunk；

## 2B: Side Channels



## 3A: Security and Capability

**CheriRTOS: A Capability Model for Embedded Devices**

> ​	Hongyan Xia, Jonathan Woodruff, Hadrien Barral, Lawrence Esswood, Alexandre Joannou, Robert Kovacsics, David Chisnall, Michael Roe, Brooks Davis, Edward Napierala, John Baldwin, Khilan Gudka, Peter G. Neumann, Alexander Richardson, Simon W. Moore, Robert N. M. Watson:

**Embedded systems** are deployed ubiquitously among various sectors including automotive, medical, robotics and avionics. As these devices become increasingly connected, the **attack** surface also increases tremendously; new mechanisms must be deployed to defend against more sophisticated attacks while not violating resource constraints. In this paper we present **CheriRTOS** on <u>CHERI-64</u>, a hardware-software platform atop Capability Hardware Enhanced RISC Instructions (CHERI) for embedded systems. Our system provides efficient and scalable task isolation, fast and secure inter-task communication, fine-grained memory safety, and real-time guarantees, using hardware capabilities as the sole protection mechanism. We **summarize** <u>state-of-the-art security and memory safety</u> for embedded systems for comparison with our platform, illustrating the superior substrate provided by CHERI's capabilities. Finally, our evaluations show that a capability system can be implemented within the constraints of embedded systems.

嵌入式设备

----

**ReadPRO: Read Prioritization Scheduling in ORAM for Efficient Obfuscation in Main Memories**

> ​	Joydeep Rakshit, Kartik Mohanram:

Modern memory systems are susceptible to **data confidentiality attacks** that leverage memory access pattern information to obtain secret data. Oblivious RAM (ORAM) is a secure cryptographic construct that effectively thwarts **access-pattern-based attacks**. However, in Path ORAM (state-of-the-art efficient ORAM for main memories) and its variants, each memory request (read or write) is transformed to an ORAM access, which is a sequence of read and write operations, increasing the latency of the memory requests and degrading system performance. In practice, the ORAM access for a read request is on the critical path of program execution, blocked by ORAM accesses for older write requests. Although modern memory controllers (MCs) realize read prioritization through write buffering, the ORAM access translation of each memory request to multiple memory read and write operations results in frequent MC write buffer overflow, decreasing its efficiency. ReadPRO (Read Prioritization) scheduling in ORAM addresses this challenge by promoting read requests over write requests in the ORAM controller prior to their ORAM access translation, while preserving all data dependencies. ReadPRO complements read promotion with staggered writes, wherein ORAM accesses for write requests can be paused securely to serve ORAM accesses for read requests. Full-system evaluations on composite SPEC CPU2006 workloads show that ReadPRO decreases the average ORAM read latency by 75%, improving system performance by 40%.

**内存攻击**

-----

**SGXlinger: A New Side-Channel Attack Vector Based on Interrupt Latency Against Enclave Execution.** 

> ​	Wenjian He, Wei Zhang, Sanjeev Das, Yang Liu

**Software Guard Extension** (**SGX**) is a new security feature that has been released in recent Intel commodity processors. It is designed to provide a user program with a strongly shielded environment against other components in the system, including the OS, firmware and hardware peripherals. With SGX, developers can securely deploy critical applications on untrusted remote platforms without the concern of information leakage. However, researchers have found several attacks against SGX, suggesting blind reliance on SGX is inadvisable, and promoting the need for a comprehensive study on the security property of SGX. In this paper, we discover a new attack vector SGXlinger to disclose information inside the protected program. Our attack monitors the interrupt latency of the SGX-protected program, and it is the first time that the interrupt latency is leveraged as a side-channel. We develop a framework to repeatedly measure the interrupt latency of an enclave program, and the evaluation shows we can learn coarse-grained information inside the shielded environment. In an experimental setting, we measure that the information leakage rate of the proposed side-channel can reach up to 35 Kbps.

----

**Breaking the Oblivious-RAM Bandwidth Wall.**

> Hamza Omar, Syed Kamran Haider, Ling Ren, Marten van Dijk, Omer Khan

**PathORAM** is a popular security primitive for obfuscating memory access patterns from a secure processor to an insecure main memory. Emerging throughput multicore and GPU processors provide immense memory bandwidth via multiple on-chip memory controllers. PathORAM translates a single off-chip cache line access into ~100 cache lines, thereby stressing the available memory bandwidth. However, current PathORAM scheme shows degradation of bandwidth utilization with an increase in the number of memory controllers. This deprivation in bandwidth utilization is primarily due to the fact that PathORAM falls short in proportionate distribution of memory accesses among all available on-chip memory controllers. This paper presents a novel ORAM path distribution scheme that ensures balanced load distribution among parallel on-chip memory controllers, and consequently improves secure processor performance by ~24% over state-of-the-art PathORAM scheme.

## 3B: Microarchitecture

## 4A: Logic and Circuit Design 1

## 4B: Design Automation

## 5A: Novel Architectures

## 5B: Memory 1

**CART: Cache Access Reordering Tree for Efficient Cache and Memory Accesses in GPUs.**

> ​	Yongbin Gu, Lizhong Chen

**Graphics processing units (GPUs)** have been increasingly used to accelerate general purpose computing. Thousands of concurrently running threads in a GPU demand a highly efficient memory subsystem for data supply. *<u>A key factor that affects the memory subsystem is the order of memory accesses</u>*. While reordering memory accesses at L2 cache has large potential benefits to both cache and DRAM, little work has been conducted to exploit this. In this paper, we investigate the largely unexplored opportunity of L2 cache access reordering. We propose **Cache Access Reordering Tree** (**CART**), a novel architecture that can improve memory subsystem efficiency by actively reordering memory accesses at L2 cache to be cache-friendly and DRAM-friendly. Evaluation results using a wide range of benchmarks show that, the proposed CART is able to improve the average IPC of memory intensive benchmarks by 34.2% with only 1.7% area overhead.

在cache中进行访问模式的修改

----

**ArchSampler: Architecture-Aware Memory Sampling Library for In-Memory Applications.**

> Jian Zhou, Jun Wang:

With the explosive rate of data growth, the limited scalability of the DRAM technology defies the performance potentials for **in-memory applications**. Fortunately, emerging non-volatile memory (NVM) technologies, such as Phase-Change Memory (PCM) and Memristor, are promising candidates for replacing DRAM. Emerging NVMs are very dense, hence promise large capacities. Additionally, NVMs are non-volatile, thus enable persistent applications and byte-addressable files. Both density and persistency are key enablers for in-memory applications. On the other side, emerging NVMs are slower than DRAM, thus optimizing for locality and avoiding contentions are key aspects to unlock the NVM performance. In this paper, we study the impact of memory contentions and architecture-oblivious implementations on the performance of sampling based in-memory approximation. **Sampling** <u>has become an imperative technique used to accelerate big data processing</u>, especially in today's emerging in-memory computing. However, we observe multiple times slow-down for nave and default implementations of in-memory data sampling. Accordingly, we propose **ArchSampler**, an architecture-aware sampling library. The main idea is to exploits the free choice of data samples to dynamically select which bank as a host to serve memory requests. Hence, ArchSampler enables efficient and high performing sampling through employing its knowledge of the NVM architectural details to maximize data locality and avoiding interthread contentions. Our evaluation shows that ArchSampler can achieve up to 1.62 speed up (1.20 on average) for different in-memory applications.

**In-memory**

----

**PIM-TGAN: A Processing-in-Memory Accelerator for Ternary Generative Adversarial Networks.**

> ​	Adnan Siraj Rakin, Shaahin Angizi, Zhezhi He, Deliang Fan

**Generative Adversarial Network** (**GAN**) has emerged as one of the most promising semi-supervised learning methods where two neural nets train themselves in a competitive environment. In this paper, as far as we know, we are the first to present a statistically trained Ternarized Generative Adversarial Network (TGAN) with fully ternarized weights (i.e. -1,0,+1) to massively reduce the need for computation and storage resources in the conventional GAN structures. In the proposed **TGAN**, the computationally expensive convolution operations (i.e. Multiplication and Accumulation) in both generator and discriminator's forward path are converted into hardware-friendly Addition/Subtraction operations. Accordingly, we propose a **Processing-in-Memory accelerator for TGAN called (PIM-TGAN)** based on Spin-Orbit Torque Magnetic Random Access Memory (SOT-MRAM) computational sub-arrays to efficiently accelerate the training process of GAN within non-volatile memory. In addition, we propose a **parallelism** technique to further enhance the training efficiency of TGAN. Our device-to-architecture co-simulation results show that, with almost the same inception score to the baseline GAN with floating point number weights on different data-sets, the proposed PIM-TGAN can obtain ~25.6× better energy-efficiency and 22× speedup compared to GPU platform averagely, and, 9.2× better energy-efficiency and 5.4× speedup over the best processing-in-ReRAM accelerators.

**PIM加速GAN网络**

----

**Path Prefetching: Accelerating Index Searches for In-Memory Databases.**

> ​	Shuo Li, Zhiguang Chen, Nong Xiao, Guangyu Sun

**In-memory databases** (**IMDBs**) store all working data in main memory, which makes memory accesses become the dominant factor of the whole system performance. Micro-architectural studies of mainstream in-memory on-line transaction processing (OLTP) systems show that more than half of the execution time goes to memory stalls. Moreover, for IMDBs that adopt aggressive transaction compilation optimizations, data misses from the last-level cache (LLC) are responsible for the majority of the overall stall time. In this paper, through profiling analysis of IMDBs we observe that **index access misses** dominate LLC data misses. Based on the key observation that adjacent keys tend to follow similar traversal paths in ordered index searches, we propose the **path prefetching** to mitigate LLC misses induced by ordered index searches, which records mappings between keys and their traversal paths and then generate prefetches for future same/adjacent keys. Experimental results show that for ordered index searches the proposed path prefetcher provides an average speedup of 27.4% over the baseline with no prefetching.

----

**Reducing Inter-Application Interferences in Integrated CPU-GPU Heterogeneous Architecture.**

> ​	Hao Wen, Wei Zhang

Current heterogeneous CPU-GPU architectures integrate general purpose CPUs and highly thread-level parallelized GPUs (Graphic Processing Units) in the same die. The contention in shared resources between CPU and GPU, such as the last level cache (LLC), interconnection network and DRAM, may degrade both CPU and GPU performance. Our experimental results show that GPU applications tend to have much more power than CPU applications to compete for the shared resources in LLC and on-chip network, and therefore make CPU suffer from more performance loss. To reduce the GPU's negative impact on CPU performance, we propose a simple yet effective method based on probability to control the LLC replacement policy for reducing the CPU's inter-core conflict misses caused by GPU without significantly impacting GPU performance. In addition, we develop two strategies to combine the probability based method for the LLC and an existing technique called virtual channel partition (VCP) for the interconnection network to further improve the CPU performance. The first strategy statically uses an empirically pre-determined probability value associated with VCP, which can improve the CPU performance by 26% on average, but degrades GPU performance by 5%. The second strategy uses a sampling method to monitor the network congestion and dynamically adjust the probability value used, which can improve the CPU performance by 24%, and only have 1 or 2% performance overhead on GPU applications.

## 6A: Memory 2

**Solar-DRAM: Reducing DRAM Access Latency by Exploiting the Variation in Local Bitlines.**

> ​	Jeremie Kim, Minesh Patel, Hasan Hassan, Onur Mutlu:

**DRAM latency** is a major bottleneck for many applications in modern computing systems. In this work, we rigorously characterize the effects of reducing DRAM access latency on 282 state-of-the-art LPDDR4 DRAM modules. As found in prior work on older DRAM generations (DDR3), we show that regions of LPDDR4 DRAM modules can be accessed with latencies that are significantly lower than manufacturer-specified values without causing failures. We present novel data that 1) further supports the viability of such latency reduction mechanisms and 2) exposes a variety of new cases in which access latencies can be effectively reduced. Using our observations, we propose a new <u>low-cost mechanism</u>, **Solar-DRAM,** that 1) identifies failure-prone regions of DRAM at reduced latency and 2) robustly reduces average DRAM access latency while maintaining data correctness, by issuing DRAM requests with reduced access latencies to non-failure-prone DRAM regions. We evaluate Solar-DRAM on a wide variety of multi-core workloads and show that for 4-core homogeneous workloads, Solar-DRAM provides an average (maximum) system performance improvement of 4.31% (10.87%) compared to using the default fixed DRAM access latency.

----

**Scalable and Efficient Virtual Memory Sharing in Heterogeneous SoCs with TLB Prefetching and MMU-Aware DMA Engine.** 

> Andreas Kurth, Pirmin Vogel, Andrea Marongiu, Luca Benini:

**Shared virtual memory (SVM)** is key in heterogeneous systems on chip (**SoCs**), which combine a general-purpose host processor with a many-core accelerator, both for programmability and to avoid data duplication. However, SVM can bring a significant run time overhead when translation lookaside buffer (TLB) entries are missing. Moreover, allowing DMA burst transfers to write SVM traditionally requires buffers to absorb transfers that miss in the TLB. These buffers have to be overprovisioned for the maximum burst size, wasting precious on-chip memory, and stall all SVM accesses once they are full, hampering the scalability of parallel accelerators. In this work, we present our SVM solution that avoids the majority of TLB misses with prefetching, supports parallel burst DMA transfers without additional buffers, and can be scaled with the workload and number of parallel processors. Our solution is based on three novel concepts: To minimize the rate of TLB misses, the TLB is proactively filled by compiler-generated Prefetching Helper Threads, which use run-time information to issue timely prefetches. To reduce the latency of TLB misses, misses are handled by a variable number of parallel Miss Handling Helper Threads. To support parallel burst DMA transfers to SVM without additional buffers, we add lightweight hardware to a standard DMA engine to detect and react to TLB misses. Compared to the state of the art, our work improves accelerator performance for memory-intensive kernels by up to 4~ and by up to 60% for irregular and regular memory access patterns, respectively.

----

**DR DRAM: Accelerating Memory-Read-Intensive Applications.** 

> ​	Yuhai Cao, Chao Li, Quan Chen, Jingwen Leng, Minyi Guo, Jing Wang, Weigong Zhang:

Today, **many data analytic workloads** such as **graph processing** and **neural network** desire efficient memory **read operation**. The need for preprocessing various raw data also demands enhanced memory read bandwidth. Unfortunately, due to the necessity of dynamic refresh, modern DRAM system has to stall memory access during each refresh cycle. As DRAM device density continues to grow, the refresh time also needs to extend to cover more memory rows. Consequently, DRAM refresh operation can be a crucial throughput bottleneck for **memory read intensive (MRI)** data processing tasks. To fully unleash the performance of these applications, we revisit conventional DRAM architecture and refresh mechanism. We propose **DR DRAM**, an application-specific memory design approach that makes a novel tradeoff between read and write performance. Simply put, DR has two layers of meaning: device refresh and data recovery. It aims at eliminating stall by enabling read and refresh operations to be done simultaneously. Unlike traditional schemes, DR explores device refresh that only refreshes a specific device at a time. Meanwhile, DR increases read efficiency by recovering the inaccessible data that resides on a device under refreshing. Our design can be implemented on existing redundant data storage area on DRAM. In this paper we detail DR's architecture and protocol design. We evaluate it on a cycle accurate simulator. Our results show that DR can nearly eliminate refresh overhead for memory read operation and brings up to 12% extra maximum read bandwidth and 50~60% latency improvement on present DRR4 device.

----

**Puzzle Memory: Multifractional Partitioned Heterogeneous Memory Scheme.** 

> ​	Jee Ho Ryoo, Shuang Song, Lizy K. John

As current main memory technology scaling is coming close to an end due to its physical limitations, many emerging memory technologies are coming to the market to fill the scaling gap. Future memory systems will require a heterogeneous memory architecture where one technology acts as a low latency memory whereas the other acts as a high capacity memory. This will allow the future main memory system to continue to scale in terms of capacity, yet have similar or slightly better latency than today's DRAM technology. Prior work on data management in heterogeneous memory has optimized one or a maximum of two components in the computing stack. However, different components are good at different tasks in data management, so in the era of heterogeneous memory, it is inevitable that cooperative multi-component data management will be adopted in future systems. We propose a heterogeneous memory layout where two memories are laid out asymmetrically. The operating system is aware of this layout and places pages with different locality characteristics in different regions of memory. Finally, a custom hardware performs the data remapping to optimize the data placement at finer granularity than what is visible to the operating system. In the end, we show that our multi-component cooperative data management scheme can improve the overall system performance by up to 40%.

## 6B: Logic and Circuit Design 2

## 7A: Accelerators and GPUs

## 7B: Potpouri 1

## 8A: NVM

**Breeze: User-Level Access to Non-Volatile Main Memories for Legacy Software**

> ​	Amirsaman Memaripour, Steven Swanson:

Non-volatile main memory (**NVMM**) technologies, such as phase change memory and 3D XPoint, offer DRAM-like performance and byte-addressable access to persistent data. A wide range of applications (e.g., key-value stores and database systems) stand to benefit from the performance potential of these technologies. These potential benefits are greatest when applications can access memory directly via **load/store** instructions rather than conventional file-based interfaces. This approach presents several challenges. In particular, applications need guaranteed consistency and safety semantics to protect their data structures in the face of system failures and programming errors. Implementing data structures that meet these requirements is challenging and error-prone. Researchers have proposed several libraries and programming language extensions that simplify this task, but, to date, all the proposed solutions either require pervasive changes to existing software or rely on special hardware support. As a result, porting legacy applications to leverage NVMM is likely to be prohibitively difficult and time consuming. We propose **Breeze**, a NVMM toolchain that minimizes the changes necessary to enable legacy code to reap the benefits of directly accessing NVMM. Breeze guarantees data consistency and validity of persistent pointers regardless of failures. The toolchain transparently detects and logs writes to NVMM and provides a simple mechanism for identifying atomic sections while avoiding complications common in previous systems such as special persistent pointer types. Porting Memcached and MongoDB to use Breeze only requires changes to 5% of the source code compared to 7-14% for NVML and NVM-Direct. Breeze also provides equal or superior performance compared to NVML and NVM-Direct, outperforming them by up to 10x.

----

**R-Cache: A Highly Set-Associative In-Package Cache Using Memristive Arrays.** 

> ​	Payman Behnam, Arjun Pal Chowdhury, Mahdi Nazm Bojnordi:

Over the past decade, three-dimensional die stacking technology has been considered for building large-scale in-package memory systems. In particular, in-package DRAM cache has been considered as a promising solution for high band-width and large-scale cache architectures. There are, however, significant challenges such as limited energy efficiency, costly tag management, and physical limitations for scalability that need to be effectively addressed before one can adopt in-package caches in the real-world applications. This paper proposes **R-Cache,** an in-package cache made by 3D die stacking of memristive memory arrays to alleviate the above mentioned challenges. Our simulation results on a set of memory intensive parallel applications indicate that R-Cache outperforms the state-of-the-art proposals for in-package caches. R-Cache improves performance by 38% and 27% over the state-of-the-art direct mapped and set associative cache architectures, respectively. Moreover, R-Cache results in averages of 40% and 27% energy reductions as compared to the direct mapped and set-associative cache systems.

----

**A Highly Non-Volatile Memory Scalable and Efficient File System.**

> ​	Fan Yang, Junbin Kang, Shuai Ma, Jinpeng Huai:

With the rapid development of fast and byte-addressable non-volatile memories (NVMs), hybrid NVM/DRAM storage systems become promising for computer systems. Existing NVM file systems have already been optimized around the NVM properties. However, they inherit some design choices of block-oriented storage devices that lead to scalability bottlenecks and data copy overhead for ensuring data consistency. In this paper, we present **noseFS**, a highly non-volatile memory scalable and efficient File System. It is designed to achieve high performance through a bundle of novel techniques: (1) a scalable lightweight naming integrating VFS with the underlying file system namespace, (2) a fine-grained byte-unit file index tree avoiding redundant copy overhead introduced by Copy-On-Write, (3) a lightweight journaling providing atomicity and scalability on many-core platforms, and (4) a lightweight atomic-mmap providing strong consistency guarantee with low overhead by tracking dirty pages. Experimental results show that noseFS performs much better than the state-of-the-art file systems with equally strong data consistency guarantees, and achieves near-linear scalability on a 40-core machine.

----

**NVCool: When Non-Volatile Caches Meet Cold Boot Attacks.**

> ​	Xiang Pan, Anys Bacha, Spencer Rudolph, Li Zhou, Yinqian Zhang, Radu Teodorescu:

Non-volatile memories (NVMs) are expected to replace traditional DRAM and SRAM for both off-chip and on-chip storage. It is therefore crucial to understand their security vulnerabilities before they are deployed widely. This paper shows that NVM caches are vulnerable to so-called "**cold boot**" attacks, which involve physical access to the processor's cache. SRAM caches have generally been assumed invulnerable to cold boot attacks, because SRAM data is only persistent for a few milliseconds even at cold temperatures. Our study explores cold boot attacks on NVM caches and defenses against them. In particular, this paper demonstrates that hard disk encryption keys can be extracted from the NVM cache in multiple attack scenarios. We demonstrate a reproducible attack with very high probability of success. This paper also proposes an effective software-based countermeasure that can completely eliminate the vulnerability of NVM caches to cold boot attacks with a reasonable performance overhead.



## 8B: Test and Verification

## 9A: Network on Chip and Synchronization

## 9B: Potpouri 2

## 10A: File System and Cloud

## 10B: FPGA and Machine Learning

