---
title: 5g/NR的部署场景
abbrlink: 8923add9
date: 2022-05-09 21:26:47
categories:
  - [3gpp, NR]
tags:
  - 3gpp
  - NR
---



《TR 38.801 V14.0.0 (2017-03) Study on new radio  access technologyRadio access architecture and interfaces》文章的第5章介绍了5G RAN需要考虑的几种场景。

这里，我们需要假设 gNB 和其他 gNB 或 (e)LTE eNB 之间可以支持基站间接口。

<!--more-->

# 相关定义

**gNB**是支持NR无线接口，并可以连接到NGC的通信节点。在《TS 38.300 V15.6.0》文中，gNB被定义为可以向UE提供NR数据面和控制面协议，并通过NG接口连接到5GC的终端。

**eLTE eNB**是既可以连接到NGC，又可以连接到EPC的通信节点。

5GC（5G Core Network）和NGC（Next Generation Core Network）都表示5G系统的核心网。

RAN：Radio Access Network，无线接入网络。



# 非集中式部署（Non-centralised deployment）

该场景中，gNB支持所有的协议栈。这里的gNB可以是宏站，也可以是公共或者企业的室内热点。gNB可以连接到任意的传输，并假设gNB可以通过RAN接口连接到其他的gNB或者 eLTE eNB。

<img src="https://cdn.jsdelivr.net/gh/xiaorangood/myImage/images/202205092230121.png"/>

<p style=align:center >sdfsd </p>

# 与EUTRAN共址部署（Co-sited deployment with E-UTRA）

在这种情况下，NR 功能与 E-UTRA 功能共址，可以作为同一基站的一部分，也可以作为同一站点的多个基站。共站部署可适用于所有NR部署场景，例如城市宏站。在这种情况下，希望通过负载均衡或者通过多种无线接入技术，使得频率资源被充分应用。

<img src="https://cdn.jsdelivr.net/gh/xiaorangood/myImage/images/202205092234712.png"/>

# 集中部署（Centralized deployment）

NR 应支持上层 NR 无线协议栈的集中化。CU（Centralized Unit，集中单元）和 gNB 底层协议具有多种不同的切分选项，其功能划分取决于传输层。CU和gNB底层协议间的高性能传输（例如光纤传输），可以实现高级CoMP和调度优化。这种部署在高容量场景或跨小区协调有益的场景中可能很有用。

高层协议栈在带宽、延迟、同步、抖动这些方面的性能要求比较低，所以可以CU可以支持。

与E-UTRA共址部署和非共址部署都可以支持几种部署。

<img src="https://cdn.jsdelivr.net/gh/xiaorangood/myImage/images/202205092235469.png"/>

# 共享 RAN 部署（Shared RAN deployment）

NR 应支持共享 RAN 部署，以支持多个核心网运营商。共享 RAN 可以覆盖较大的地理区域，例如国家或区域网络共享；可以是异构的，也就是被限制在较小的区域里，例如Shared in-building RAN；可以高效的与非共享 RAN进行互操作。

每个核心网运营商可能有自己的，且与可以与其他共享 RAN 相邻的非共享 RAN。共享 RAN 和非共享 RAN之间的移动性，不能比LTE差。

共享 RAN 既可以在共享频谱上，也可以在运行商的频谱上运行。

<img src="https://cdn.jsdelivr.net/gh/xiaorangood/myImage/images/202205092236282.png"/>
