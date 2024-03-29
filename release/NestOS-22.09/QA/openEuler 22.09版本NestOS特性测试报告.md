![avatar](../images/openEuler.png)

版权所有 © 2022  openEuler社区
您对“本文档”的复制、使用、修改及分发受知识共享(Creative Commons)署名—相同方式共享4.0国际公共许可协议(以下简称“CC BY-SA 4.0”)的约束。为了方便用户理解，您可以通过访问[*https://creativecommons.org/licenses/by-sa/4.0/*](https://creativecommons.org/licenses/by-sa/4.0/) 了解CC BY-SA 4.0的概要 (但不是替代)。CC BY-SA 4.0的完整协议内容您可以访问如下网址获取：[*https://creativecommons.org/licenses/by-sa/4.0/legalcode*](https://creativecommons.org/licenses/by-sa/4.0/legalcode)。

修订记录

| 日期 | 修订   版本 | 修改描述 | 作者 |
| ---- | ----------- | -------- | ---- |
|    2022/9/29  |       1.1.0      |     初始     |   fushanqing   |

 关键词： 

 openEuler NestOS iSulad docker podman rpm-ostree zincati

摘要：

 文本主要描述NestOS 22.09版本的整体测试过程，详细叙述测试覆盖情况，并通过问题分析对版本整体质量进行评估和总结。

缩略语清单：

| 缩略语 | 英文全名 | 中文解释 |
| ------ | -------- | -------- |
|    OS    |     Operating system     |    操作系统      |
|    iSulad    |     iSulad     |     轻量级容器引擎     |
|    Docker    |     Docker     |     Docker容器引擎     |
|    Podman    |     Podman     |     Podman容器引擎     |
|    rpm-ostree    |     rpm-ostree     |     混合镜像/包系统     |
|    zincati    |     zincati     |     自动更新引擎     |

# 1     特性概述

NestOS 是一款基于openEuler开发的自动更新的最小化操作系统。Nestos搭载了docker、iSulad、podman等常见容器引擎，将ignition配置、rpm-ostree、OCI支持、SElinux强化等技术集成在一起，采用基于双系统分区、容器技术和集群架构的设计思路，可以适配云场景下多种基础运行环境。同时NestOS针对Kubernetes进行优化，在IaaS生态构建方面，针对openStack、oVirt等平台提供支持；在PaaS生态构建方面，针对OKD、Rancher等平台提供支持，使系统具备十分便捷的集群组件能力，可以更安全的运行大规模的容器化工作负载。

本文主要描述NestOS 22.09版本的总体测试活动，按照社区开发模式进行运作，结合CloudNative/QA社区制定的版本计划规划相应的测试计划及活动。
# 2     特性测试信息

NestOS 22.09 版本是基于5.10内核22年创新版本，软件包原则上取用 openEuler-22.09分支，部分修改软件包如shadow、crypto-policies已在master提相关pr，暂未合入openEuler-22.09分支，但均已在该环境下编译。其关键特性如下：

 1. ignition自定义配置
 2. nestos-installer安装
 3. zincati自动升级
 4. rpm-ostree原子化更新

| 版本名称 | 测试起始时间 | 测试结束时间 |
| -------- | ------------ | ------------ |
|     NestOS Test Round 1     |       2022/8/25       |        2022/8/19     |
|     NestOS Test Round 2     |       2022/9/1        |        2022/9/3      |
|     NestOS Test Round 3     |       2022/9/4        |        2022/9/10     |

描述特性测试的硬件环境信息
NestOS 在以下硬件进行安装适配和基本功能验证

| **硬件型号**  |
|:-|
| 飞腾FT2000+ |
| 飞腾S2500 |
| 鲲鹏920 |

# 3     测试结论概述

## 3.1   测试整体结论

NestOS 22.09 版本整体测试按照计划共完成了一轮重点特性测试+一轮专项测试+一轮回归测试；其中第一轮重点特性测试聚焦在ignition自定义配置、nestos-installer安装、容器引擎、zincati自动升级、rpm-ostree原子化更新+双系统分区的特性验证；一轮专项测试开展版本交付的各类专项测试；一轮回归测试重点覆盖特性测试，验证问题的修复程度。
NestOS 22.09 版本共发现问题 6 个，有效问题 6 个，0个遗留问题，6个问题已修复，回归测试结果正常，版本整体质量较好。


## 3.2   特性测试结论
| 测试活动 | 活动评价 |
| -------- | -------- |
| ignition自定义配置 |    共执行2轮测试，通过配置不同ignition文件，覆盖了ignition提供的网络、存储、文件、内核参数、容器、用户和组、主机名、系统外部软件包安装、时区设置等功能，保证可以远程/本地获取ign文件、通过ignition配置系统安装成功，且配置生效。      |
| nestos-installer安装 |    共执行1轮测试，重点验证了通过nestos-installer安装操作系统到目标磁盘的功能。     |
| zincati自动更新 |     共执行2轮测试，测试修改zincati配置、检测更新源、自动下载部署新版本、更新后自动重启功能。重点验证了zincati完成新版本的自动下载和部署、更新重启后服务不中断的测试。     |
| rpm-ostree原子化更新+双系统分区 |     共执行2轮测试，验证手动使用rpm-ostree检测、下载、部署新版本，同时测试了更新版本后双系统分区的验证。     |

## 3.2   专项测试结论
| 测试活动 | 活动评价 |
| -------- | -------- |
| 基础功能测试 |    对系统管理、系统服务、常用命令（文件系统、进程监控、网络、用户管理）进行测试，系统基础功能稳定。      |
| 容器功能测试 |    测试iSulad、podman、docker容器引擎基本功能，测试K8S+iSulad 搭建，iSulad和docker功能均能正常运行。      |
| 可靠性测试 |   对NestOS进行稳定测试，测试操作系统稳定运行168 小时。     |
| 性能测试 |     对网络性能、容器性能进行了测试，重点测试了iSulad、docker、podman容器引擎对容器启停时间的消耗，测试结果表明iSulad性能优于docker、podman。     |
| 安全性测试 |     对身份鉴别、安全审计、用户登录、用户权限、远程连接，测试结果符合预期。     |

## 3.2   约束说明

 - 内存：4GB及以上
 - 架构：x86_64、aarch64
 - 使用zincati自动更新和rpm-ostree手动更新特性时，需保证当前NestOS版本不是最新版本，若当前NestOS是最新版本，则无法使用该功能。

## 3.3   遗留问题分析

### 3.3.1 遗留问题影响以及规避措施

| 问题单号 | 问题描述 | 问题级别 | 问题影响和规避措施 | 当前状态 |
| -------- | -------- | -------- | ------------------ | -------- |

### 3.3.2 问题统计

|        | 问题总数 | 严重 | 主要 | 次要 | 不重要 |
| ------ | -------- | ---- | ---- | ---- | ------ |

# 4     测试执行

## 4.1   测试执行统计数据


| 版本名称 | 测试用例数 | 用例执行结果 | 发现问题单数 |
| -------- | ---------- | ------------ | ------------ |
|     NestOS Test Round 1     |      16      |       4 FAIL       |       4       |
|     NestOS Test Round 2     |      32      |       2 FAIL       |       2       |
|     NestOS Test Round 3     |      48      |       ALL PASS     |       0       |

*数据项说明：*

*测试用例数－－到本测试活动结束时，所有可用测试用例数；*

*发现问题单数－－本测试活动总共发现的问题单数。*

## 4.2   后续测试建议

后续测试需要关注点(可选)

# 5     附件

*此处可粘贴各类专项测试数据或报告*

 



 

 
