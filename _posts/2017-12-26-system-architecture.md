---
layout: post
title: 集中式 vs. 分布式系统架构
key: 20171226
tags: 集中式 分布式 系统架构
category: blog
date: 28-12-2017
modify_date: 03-01-2018
---

## 一、前言

随着计算机系统规模变得越来越大，将所有业务单元集中部署在一个或者若干个大型机上的体系结构物，已经越来越不能满足当今计算机系统，尤其是大型互联网系统的快速发展，各种灵活多变的系统架构模型层出不穷。同时，随着微型计算机的出现，越来越多廉价的PC机成为了各大IT企业架构的首选，分布式的处理方式越来越受到业界的青睐。计算机系统正在经历一场前所未有的从集中式到分布式架构的变革。

从集中式到分布式

自从20世纪60年代大型主机被发明出来以后，凭借其超强的计算和I/O处理能力以及在稳定性和安全性方面的卓越表现，在很长一段时间内，大型主机引领了计算机行业以及商业计算领域的发展。在大型主机的研发上最知名的当属IBM，其主导研发的革命性产品System/360系列大型主机，是计算机发展史上的一个里程碑，与波音707和福特T型车齐名，被誉为20世纪最重要的三大商业成就，IT界进入了大型主机时代。
<!--more-->

伴随着大型主机时代的到来，集中式的计算机系统架构也成为了主流。在那个时候，由于大型主机卓越的性能和良好的稳定性，其在单机处理能力方面的优势非常明显，使得IT系统快速进入了集中式处理阶段，其对应的计算机系统称为集中式系统。但从20世纪80年代以来，计算机系统向网络化和微型化的发展日趋明显，传统的集中式处理模型越来越不能适应人们的需求，具体表现在：

1、大型主机的人才培养成本非常高，通常一台大型主机汇集了大量精密的计算机组件，操作非常复杂，这对一个运维人员掌握其技术细节提出了非常高的要求。

2、大型主机也是非常昂贵的，通常一台配置较好的IBM大型主机，其售价达到上百万美元甚至更高，因此也只有像政府、金融和电信等企业才有能力采购大型主机。

3、集中式有非常明显的单点问题，大型主机虽然在性能和稳定性方面表现卓越，但并不代表其永远不会出故障。一旦一台大型主机出现了故障，那么整个系统将处于不可用的状态，后果相当严重。最后，随着业务的不断发展，用户访问量迅速提高，计算机系统的规模也在不断扩大，在单一大型主机上进行扩容往往比较困难。

4、随着PC机性能的不断提升和网络技术的快速普及，大型主机的市场份额变得越来越小，很多企业开始放弃原来的大型主机，而改用小型机和普通PC服务器来搭建分布式计算机。

对业内新闻比较关注的，一定知道阿里巴巴在2009年发起了一项"去IOE"运动。因为阿里巴巴从2008年开始各项业务都进入了井喷式的发展阶段，这对于后台IT系统的计算与存储能力提出了非常高的要求，一味地针对小型机和高端存储进行不断扩容，无疑会产生巨大的成本。同时，集中式的系统架构体系也存在着诸多单点问题，完全无法满足互联网应用爆炸式的发展需求。因此，为了解决业务快速发展给IT系统带来的巨大挑战，从2009年开始，阿里集团启动了"去IOE"计划，其电商系统开始正式迈入了分布式系统时代。

## 二、集中式系统架构

所谓集中式系统就是指由一台或多台主计算机组成中心节点，数据集中存储于这个中心节点中，并且整个系统的所有业务单元都集中部署在这个中心节点上，系统所有的功能均由其集中处理。也就是说，集中式系统中，每个终端或客户端及其仅仅负责数据的录入和输出，而数据的存储与控制处理完全交由主机来完成。

集中式系统最大的特点就是部署结构简单，由于集中式系统往往基于底层性能卓越的大型主机，因此无需考虑如何对服务进行多个节点的部署，也就不用考虑多个节点之间的分布式协作问题。

## 三、分布式系统架构

在《分布式系统概念与设计》注一书中，对分布式系统做了如下定义：

分布式系统是一个硬件或软件组件分布在不同的网络计算机上，彼此之间仅仅通过消息传递进行通信和协调的系统。

严格地讲，同一个分布式系统中的计算机在空间部署上是可以随意分布的，这些计算机可能被放在不同的机柜上，也可能在不同的机房中，甚至分布在不同的城市。无论如何，一个标准的分布式系统在没有任何特定业务逻辑约束的情况下，都会有以下几个特征：

### 1、分布性

分布式系统中的多台计算机都会在空间上随意分布，同时，及其的分布情况也会随时变动。

### 2、对等性

分布式系统中的计算机没有主从之分，既没有控制整个系统的主机，也没有被控制的从机，组成分布式系统的所有节点都是对等的。副本（Replica）是分布式系统最常见的概念之一，指的是分布式系统对数据和服务提供的一种冗余方式。在常见的分布式系统中，为了对外提高可用的服务，我们往往会对数据和服务进行副本处理。数据副本是指在不同的节点上持久化同一份数据，当某一个节点上存储的数据丢失时，可以从副本上读取到该数据，这是解决分布式系统数据丢失问题最为有效的手段。另一类副本是服务副本，指多个节点提供同样的服务，每个节点都有能力接收来自外部的请求并进行相应的处理。

### 3、并发性

在一个计算机网络中，程序运行过程中的并发性操作是非常常见的行为，例如同一个分布式系统的多个节点，可能会并发地操作一些共享的资源，诸如数据库或分布式存储等，如何准确并高效地协调分布式并发操作也成为了分布式系统架构与设计中最大的挑战之一。

### 4、缺乏全局时钟 

一个典型的分布式系统是由一系列空间上随意分布的多个进程组成的，具有明显的分布性，这些进程之间通过交换消息来进行相互通信。因此，在分布式系统中，很难定义两个事件究竟谁先谁后，原因就是因为分布式系统缺乏一个全局的始终控制序列。

### 5、故障总是会发生

组成分布式系统的所有计算机，都有可能发生任何形式的故障。一个被大量工程实践过的黄金定理是：任何在设计阶段考虑到的异常情况，一定会在系统实际运行中发生，并且，在系统实际运行中还会遇到很多在设计时未考虑到的异常故障。所以，除非需求指标允许，在系统设计时不能放过任何异常情况。

### 6、处理单点故障

在整个分布式系统中，如果某个角色或者功能只有某台单机在支撑，那么这个节点称为单点，其发生的故障称为单点故障，也就是通常说的SPoF（Single Point of Failure），避免单点而对关键就是把这个功能从单机实现变为集群实现，当然，这种变化一般会比较困难，否则就不会有单点问题了。如果不能把单点变为集群实现，那么一般还有两种选择：

（1）给这个单点做好备份，能够在出现问题时进行恢复，并且尽量做到自动恢复。

（2）降低单点故障的影响范围。

## 四、集中式与分布式系统架构之间的比较

目前，在IT系统架构设计中，对于服务器的配置方案主要有两种。
1. 分布式，即根据业务功能、模块设计或行政部门及机构的不同，采用相对分散的中小型服务器；
2. 集中式，即将所需的主机资源集中到少数的几台大型服务器中。

这两种方式，在投资成本、业务支撑及扩展能力、维护管理、方案拓展等方面，存在着比较显著的差异。

### 1. 业务支撑及扩展能力

采用三层结构设计的系统中，数据库层和应用层一般支持横向和纵向两种扩展方式。其中，横向指通过增加服务器台数来扩展某一层次的处理能力，纵向指通过对单台主机的CPU、内存等配件扩充来提高某一层次的处理能力。

分散式结构下，由于单台主机的处理能力比较有限，所以数据库层和应用层将主要依赖于横向扩充方式来支撑业务的扩展。横向扩充方式的实现，并不等同于简单地增加机器，有两个前提必须要满足。一是多台数据库服务器必须能够并行运行，这就要求使用并行版数据库软件。二是应用系统必须基于并行数据访问方式进行开发。在实际地使用中，由于并行版数据库软件使用较难、维护费用高、应用软件大多没有基于并行方式开发等原因，横向扩充方式实现起来相对较难。当业务处理需求发展到一定程度时，单台主机的处理能力，尤其是数据库服务的地处理能力，往往成为制约整体业务扩充能力的薄弱环节。

集中式结构下，除了可以采用横向方式进行扩充外，由于单台主机具备较好的扩充能力，因此可以采用纵向方式进行处理能力的扩充。纵向扩充方式，仅涉及硬件配件的增加，数据库软件和应用软件不需调整，实现起来相对容易。

### 2. 投资成本 

#### （1）机房建设成本
       
采用分散方式进行系统建设，一般需要的主机数量从数台到数十台不等。这些主机，都需要基本的机房占地（包括主机自身面积和每台四周一米左右的维护空间）、承重设计、电力供应、制冷需求。累计到一起之后，通常对机房的基本建设提出很大的需求。尤其对于一些保密性要求较高的中心机房，机房建设成本往往不是以平面面积进行衡量，而是以立方面积进行计量的。这种情况下，每增加一台主机设备，将导致机房基本构建成本的大幅度上升。而采用集中方式进行系统建设，所需要的主机和存储设备大幅度减少，相应对占地面积、承重设计、电力供应、制冷设备等基本建设方面的要求都大大降低，从减少了机房建设成本。

#### （2）硬件成本 
 
过去，在硬件成本的采购上，采用集中式结构通常会比采用分散式结构投资略大一些。现在，随着主机上分区技术的普遍采用，主机的CPU、内存等资源能够很好地加以均衡和利用，减少每台机器的“浪费”空间和资源，两种结构的投资差异不大，甚至常常出现分散式的投资比集中式的投资更大的情况。

#### （3）软件成本 

集中式使用的CPU总数通常比分散式少。系统软件、数据库软件、应用软件等软件产品的采购费用是与CPU个数成正比的。因此，采用集中式，能够节约软件采购成本。

#### （4）运行成本 

集中式结构的运行成本较低。由于采用较少的设备，在机房个数、机房空间、电源功率、机房制冷、保修费用等方面，集中式都比分散式相对节约。

### 3. 使用灵活性 

分散式结构中，所有主机的功能单一，若需要变换功能，需要对系统进行较大调整。集中模式下，各分区的功能可以根据需要进行调整，如果将来有业务扩充或者功能增加时，实现起来比较容易。相比而言，集中模式的灵活性更强。

### 4. 资源利用有效性 

分散式结构下，每台主机的资源被限制用于某一个固定的功能。当某台主机资源紧张时，即使其它主机还有大量的空闲资源，也无法调配给这台主机使用。只能通过系统升级的方式解决问题。而集中模式下，主机资源可以在同一台主机的不同分区之间动态调配。当某个分区资源紧张时，如果同一主机的其它分区上有空闲资源，可以随时动态调配给这个分区使用。另一方面，分散模式需要对每台主机都配置本地磁带机、光驱、显卡、显示器等设备。而集中模式则可以根据需要对每台主机只配置一套这类设备。因此，集中模式对系统资源的利用更加有效。

### 5. 维护管理 

由于集中式采用服务器数量比分散式少，可以减少硬件的故障点，从而减少硬件维护的工作量，降低系统管理的繁琐程度。当然，由于设备相对比较集中，单台设备故障后的影响范围也就较大。因此，分散式结构下，单台设备故障导致的运行风险相对较小。集中式下，对选用主机的高可靠性要求更高。

### 6. 方案拓展 

数据处理中心建立后，随之而来的，就是对灾难备份的考虑。在这个方面，分散式结构下，要建立灾难备份系统，难度相对较大。由于设备数量多、地点可能分散、平台不一定一致，对灾备技术的选择比较受限制，可选方案相对较少，甚至没有可选方案。而集中式结构下，能够实现灾备的方式，相对较多。

另一方面，采用分散式结构，灾备中心需要配置的备份设备比较多，投资相对更大。

综上所述，分散式和集中式两种模式，各有利弊。对于大型的数据处理中心，通常集中式更为适合。

**参考文献:**  [https://wenku.baidu.com/view/7c9081e2524de518964b7d4e.html](https://wenku.baidu.com/view/7c9081e2524de518964b7d4e.html)

**参考博客:**  [http://www.cnblogs.com/szlbm/p/5588541.html](http://www.cnblogs.com/szlbm/p/5588541.html)
