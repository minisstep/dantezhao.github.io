---
layout: post
title:  "漫谈数据仓库之基本概念总结（不断更新）"
categories: 数据为王
tags:  Hive 数据仓库
---

* content
{:toc}

## 0x00 前言

> 整理一些数据仓库中的常用概念。大部分概念不是照搬书上的准确定义，会加入很多自己的理解。




## 0x01 概念

### 数据仓库（Data Warehouse）

> 数据仓库，英文名称为Data Warehouse，可简写为DW或DWH。数据仓库，是为企业所有级别的决策制定过程，提供所有类型数据支持的战略集合。


*个人理解，数据仓库不单单是一个概念，其实算是对数据管理和使用的一种方法论，它包括了如何合理地收集数据、如何规范的管理数据、如何优雅地使用数据，以及任务调度、数据血统分析等一系列内容。 在大数据时代这些概念依旧没有过时，相反，它更加重要。*

利用数据仓库的方式存放的资料，具有一旦存入，便不会随时间发生变动的特性，此外，存入的资料必定包含时间属性，通常一个数据仓库中会含有大量的历史性资料，并且它可利用特定的分析方式，从其中发掘出特定的资讯。

### 联机分析处理（OLAP, Online Analytical Process）

> OLAP（Online Analytical Process），联机分析处理，以多维度的方式分析数据，而且能够弹性地提供 **上卷（Roll-up）** 、**下钻（Drill-down）** 和透视分析（Pivot）等操作，它是呈现集成性决策信息的方法，多用于决策支持系统、商务智能或数据仓库。其主要的功能在于方便大规模数据分析及统计计算，可对决策提供参考和支持。与之相区别的是联机交易处理（OLTP），联机交易处理，更侧重于基本的、日常的事务处理，包括数据的增删改查。

OLAP需要以大量历史数据为基础，再配合上时间点的差异，对多维度及汇整型的信息进行复杂的分析。

OLAP的概念，在实际应用中存在广义和狭义两种不同的理解方式。广义上的理解与字面上的意思相同，泛指一切不会对数据进行更新的分析处理。但更多的情况下OLAP被理解为其狭义上的含义，即与多维分析相关，基于立方体（Cube）计算而进行的分析。



### 商务智能（BI, Business Intelligence）


BI（Business Intelligence），即商务智能，指用现代数据仓库技术、在线分析技术、数据挖掘和数据展现技术进行数据分析以实现商业价值。

*大致上来讲，BI就是利用各种技术来辅助于商业决策，它需要以数据仓库的数据为基础，通过Olap系统来做分析，必要时还需要一些数据挖掘的方法来挖掘更深层次的价值。*

### 元数据（Metadata）


管理元数据的系统。网上没找到定义，个人对它的理解如下：

> 一个管理元数据信息的系统
> 能够提供方便的元数据的操作和查询操作

它会有下面这些功能：

![](http://dantezhao.oss-cn-shanghai.aliyuncs.com/data/metadata_1.png?x-oss-process=style/blog_dantezhao)

详细的内容请参照这篇博客[Google和Linkedin的老司机是如何管理海量数据的](http://dantezhao.com/2017/05/30/data-metadata/)

### 数据分层

其实数据分层的意思就是对数据按照一定的层级来存储，这样做的好处很多，在下面列了几个，详细的请参考这篇博客：[大数据环境下该如何优雅地设计数据分层](http://dantezhao.com/2017/05/14/data-layer/)

1. 清晰数据结构：每一个数据分层都有它的作用域，这样我们在使用表的时候能更方便地定位和理解。
2. 数据血缘追踪：简单来讲可以这样理解，我们最终给业务诚信的是一能直接使用的张业务表，但是它的来源有很多，如果有一张来源表出问题了，我们希望能够快速准确地定位到问题，并清楚它的危害范围。
3. 减少重复开发：规范数据分层，开发一些通用的中间层数据，能够减少极大的重复计算。
4. 把复杂问题简单化。讲一个复杂的任务分解成多个步骤来完成，每一层只处理单一的步骤，比较简单和容易理解。而且便于维护数据的准确性，当数据出现问题之后，可以不用修复所有的数据，只需要从有问题的步骤开始修复。
5. 屏蔽原始数据的异常。
6. 屏蔽业务的影响，不必改一次业务就需要重新接入数据。

### 维度建模

*维度建模是一种数据仓库的建模方法，这样讲吧，它的作用就是帮你更好的组织和使用数据。* 详细的讲解请看这篇博客：[漫谈数据仓库之维度建模](http://dantezhao.com/2017/01/05/data-warehouse-dimension-modeling/)

维度模型是数据仓库领域大师Ralph Kimall所倡导，他的《The DataWarehouse Toolkit-The Complete Guide to Dimensona Modeling，中文名《数据仓库工具箱》，是数据仓库工程领域最流行的数仓建模经典。维度建模以分析决策的需求出发构建模型，构建的数据模型为分析需求服务，因此它重点解决用户如何更快速完成分析需求，同时还有较好的大规模复杂查询的响应性能。

典型的代表是我们比较熟知的星形模型，以及在一些特殊场景下适用的雪花模型。


### ETL （Extract-Transform-Load）

*ETL 在数据开发的工作中主要是数据清洗，它包括数据的接入，初步的清洗，数据导入Hive或者Mysql中等一系列操作，目前比较火的大数据技术在很大程度上就是解决了大数据量下的数据清洗工作。*

**另外，很多写sql的任务也可以理解是数据清洗，比如使用sql对原始数据做一部分的业务处理、过滤掉一些特殊记录等，因此ETL的范围相对来讲比较广，很多数据开发的工作都可以归结到ETL中。**

ETL，是英文 Extract-Transform-Load 的缩写，用来描述将数据从来源端经过抽取（extract）、转换（transform）、加载（load）至目的端的过程。ETL一词较常用在数据仓库，但其对象并不限于数据仓库。

ETL是构建数据仓库的重要一环，用户从数据源抽取出所需的数据，经过数据清洗,最终按照预先定义好的数据仓库模型，将数据加载到数据仓库中去。

## 参考

- https://research.google.com/pubs/pub45390.html
- http://baike.baidu.com/item/%E6%95%B0%E6%8D%AE%E4%BB%93%E5%BA%93
- http://dantezhao.com/2017/05/30/data-metadata/
- http://dantezhao.com/2017/05/14/data-layer/
- http://dantezhao.com/2017/01/05/data-warehouse-dimension-modeling/
- http://baike.baidu.com/item/ETL/1251949

***
2017-06-15 21:13:00 lkds