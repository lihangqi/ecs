# 创建SCC实例 {#concept_vrp_mr1_ydb .concept}

本文介绍如何创建SCC实例。

## 操作步骤 {#section_h2m_pr1_ydb .section}

您可以参见[创建ECS实例](intl.zh-CN/实例/创建实例/使用向导创建实例.md#)的描述创建超级计算集群实例。

在配置参数时，您需要注意以下几点：

-   **地域**：请根据表格[提供SCC实例的地域和可用区](intl.zh-CN/实例/选择实例规格/超级计算集群（SCC）/创建SCC实例.md#section_ycz_mnl_jhb)选择地域和可用区。如果售卖页显示的地域和可用区和表格不一致，以售卖页为准。
-   **网络**：仅支持专有网络（VPC 网络）。
-   **实例**：支持scch5（高主频型超级计算集群实例规格族）、sccg5（通用型超级计算集群实例规格族）和sccgn6（GPU计算型超级计算集群实例规格族）。
-   **镜像**：选择**公共镜像**。目前支持定制版的Linux CentOS 7.5。

    **说明：** 定制版镜像支持 RDMA RoCE 驱动和 OFED 堆栈。您可以通过 IB verbs 编程使用 RDMA 功能或者通过 MPI 进行 RDMA 通讯。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9637/15667773135118_zh-CN.png)

-   **存储**：超级计算集群支持最多挂载 16 块数据盘。您可以在这里添加数据盘，也可以在实例创建成功后再单独创建并挂载数据盘。具体操作，请参见[创建按量付费云盘](../../../../intl.zh-CN/块存储/云盘/创建云盘/创建按量付费云盘.md#)和[挂载云盘](../../../../intl.zh-CN/块存储/云盘/挂载云盘.md#)。

## 提供SCC实例的地域和可用区 {#section_ycz_mnl_jhb .section}

提供各SCC实例规格族的地域和可用区如下表所示：

|实例规格|地域和可用区|
|----|------|
|scch5|华东2（上海）可用区D、可用区B|
|sccg5|华东2（上海）可用区D、可用区B|
|sccgn6| -   华东2（上海）
-   华北2（北京）
-   华北3（张家口）

 |

## 相关操作 {#section_g2m_pr1_ydb .section}

如果您不仅需要使用 RDMA 功能，还需要使用 HPC 调度器以及集群扩容缩容服务，可以通过[E-HPC 控制台](https://ehpc.console.aliyun.com/)创建 SCC 集群来创建 SCC 实例。

**说明：** 目前 SCC 集群在售区域请参见[提供SCC实例的地域和可用区](intl.zh-CN/实例/选择实例规格/超级计算集群（SCC）/创建SCC实例.md#section_ycz_mnl_jhb)，付费类型只支持包年包月。

