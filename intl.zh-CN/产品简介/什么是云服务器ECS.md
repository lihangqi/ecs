# 什么是云服务器ECS {#concept_rhf_xgv_tdb .concept}

通过本文档，您可以了解什么是阿里云云服务器ECS，以及它所涉及的资源和服务。

云服务器Elastic Compute Service（ECS）是阿里云提供的一种基础云计算服务。使用云服务器ECS就像使用水、电、煤气等资源一样便捷、高效。您无需提前采购硬件设备，而是根据业务需要，随时创建所需数量的云服务器ECS实例。在使用过程中，随着业务的扩展，您可以随时扩容磁盘、增加带宽。如果不再需要云服务器，也能随时释放资源，节省费用。



下图列出了ECS涉及的所有资源，包括实例规格、块存储、镜像、快照、带宽和安全组。您可以通过 [云服务器管理控制台](https://ecs.console.aliyun.com/#/home) 配置您的ECS资源。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9543/15404527794795_zh-CN.png)

## 相关概念 {#section_jkn_4qj_ydb .section}

在使用ECS之前，您需要了解以下概念：

-   [地域和可用区](https://www.alibabacloud.com/help/doc-detail/40654.htm)：指ECS实例所在的物理位置。

-   [实例](intl.zh-CN/产品简介/实例/实例概述.md#)：等同于一台虚拟机，包含CPU、内存、操作系统、网络、磁盘等最基础的计算组件。

-   [实例规格](intl.zh-CN/产品简介/实例规格族.md#)：指实例的配置，包括vCPU核数、内存、网络性能等。实例规格决定了ECS实例的计算和存储能力。

-   [镜像](intl.zh-CN/产品简介/镜像.md#)：指ECS实例运行环境的模板，一般包括操作系统和预装的软件。操作系统支持多种Linux发行版本和不同的Windows版本。

-   [块存储](intl.zh-CN/产品简介/块存储/什么是块存储.md#)：包括基于分布式存储架构的 [云盘和共享块存储](intl.zh-CN/产品简介/块存储/云盘和共享块存储.md#)，以及基于物理机本地硬盘的 [本地存储](intl.zh-CN/产品简介/块存储/本地盘.md#)。

-   [快照](intl.zh-CN/产品简介/快照/快照概述.md#)：指某一个时间点上一块弹性块存储的数据备份。

-   [网络类型](intl.zh-CN/产品简介/网络和安全性/网络类型.md#)：

    -   专有网络：基于阿里云构建的一个隔离的网络环境，也称为VPC，VPC之间逻辑上彻底隔离。更多信息，请参考 [专有网络VPC](../../../../intl.zh-CN/产品简介/什么是专有网络.md#)。

    -   经典网络：统一部署在阿里云公共基础设施内，规划和管理由阿里云负责。

-   [安全组](intl.zh-CN/产品简介/网络和安全性/安全组.md#)：由同一地域内具有相同保护需求并相互信任的实例组成，是一种虚拟防火墙，用于设置实例的网络访问控制。


## 使用ECS {#section_lsd_yqj_ydb .section}

您可以通过如下方式对云服务器ECS进行管理：

-   管理控制台：阿里云提供的Web服务页面，方便您管理云服务器ECS。关于管理控制台的操作，请参考 [操作指南](../../../../intl.zh-CN/用户指南/常用操作导航.md#)。

-   API接口：阿里云也提供了API接口方便您管理云服务器ECS。关于API说明，请参考 [API参考](../../../../intl.zh-CN/API 参考/简介.md#)。

-   命令行工具：您可以使用阿里云命令行工具CLI（Alibaba Cloud CLI）调用API管理ECS，更多信息，请参考 [命令行工具CLI](https://www.alibabacloud.com/help/product/29991.htm)。

-   Terraform：您可以使用开源工具Terraform来预配和管理ECS资源。Terraform提供一种简单机制，能够将配置文件部署到阿里云以及其他支持的云，并对其进行版本控制。更多信息，请参考 [Terraform文档](../../../../intl.zh-CN/最佳实践/Terraform/什么是Terraform.md#)。


## ECS定价 {#section_vq5_brj_ydb .section}

ECS支持预付费和按量付费。更多信息，请参考 [产品定价](../../../../intl.zh-CN/产品定价/计费概述.md#) 文档。

ECS及相关资源的价格信息，请参考 [云产品定价页](https://www.alibabacloud.com/product/ecs)。

## 学习路径图 {#section_flx_zwp_52b .section}

您可以通过 [ECS 学习路径图](https://www.alibabacloud.com/getting-started/learningpath/ecs) 快速了解产品，由浅入深学习使用和运维 ECS。

## 相关服务 {#section_ogy_tqj_ydb .section}

使用ECS的同时，您还可以使用以下服务：

-   您可以从 [云市场](https://www.alibabacloud.com/marketplace) 获取由第三方服务商提供的基础软件、企业软件、网站建设、代运维、云安全、数据及API、解决方案等相关的各类软件和服务。您也可以成为云市场服务供应商。更多信息，请参考 [云市场文档](https://www.alibabacloud.com/help/product/30488.htm)。

-   您可以根据业务需求和策略的变化自动调整ECS资源。更多信息，请参考 [弹性伸缩文档](https://www.alibabacloud.com/help/product/25855.htm)。

-   您可以在一组云服务器ECS上通过Docker容器管理应用生命周期。更多信息，请参考 [容器服务（Container Service）文档](https://www.alibabacloud.com/help/product/25972.htm)。

-   您可以对多台云服务器ECS实现流量分发的负载均衡服务。更多信息，请参考 [负载均衡（Server Load Balancer）文档](https://www.alibabacloud.com/help/product/27537.htm)。

-   您可以监控ECS实例、系统盘和公网带宽等。更多信息，请参考 [云监控（CloudMonitor）文档](https://www.alibabacloud.com/help/product/28572.htm)。

-   您可以使用安骑士保障云服务器ECS的安全。更多信息，请参考 [安骑士文档](https://www.alibabacloud.com/help/product/28449.htm)。

-   对于部署在云服务器ECS上的应用，阿里云为您提供了免费的DDoS基础防护，您也可以使用DDoS高防IP保障源站的稳定可靠。更多信息，请参考 [DDoS基础防护文档](https://www.alibabacloud.com/help/doc-detail/28399.htm) 和 [DDoS高防IP文档](https://www.alibabacloud.com/help/doc-detail/28464.htm)。

-   您可以编写代码调用阿里云开发者工具包（SDK）访问阿里云的产品和服务，更多信息，请参考 [阿里云开发工具包\(SDK\)](https://www.alibabacloud.com/support/developer-resources)。您可以使用 [OpenAPI Explorer](https://api.aliyun.com/) 在线调试ECS API，并生成对应SDK Demo代码。


