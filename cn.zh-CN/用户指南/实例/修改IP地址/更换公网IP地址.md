# 更换公网IP地址 {#concept_emj_v2n_xdb .concept}

如果您的实例分配了公网IP地址，无论是经典网络还是专有网络（VPC），在创建后6小时内，您可以更换公网IP地址。

## 限制条件 {#section_pv5_w2n_xdb .section}

更换分配的公网IP地址有以下限制：

-   实例必须分配了公网IP地址，即在 **实例列表** 里，实例的 **IP地址** 列会显示公网IP地址，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9656/15433990175458_zh-CN.png)

    **说明：** 

    -   如果在创建预付费实例时未分配公网IP地址，实例创建成功后，您可以通过升降公网带宽配置分配公网IP地址，更多信息，请参考 [升降配概述](intl.zh-CN/用户指南/实例/升降配/升降配概述.md#)。
    -   如果在创建按量付费实例时未分配公网IP地址，实例创建成功后，无法再分配公网IP地址，只能 [绑定弹性公网IP（EIP）地址](https://www.alibabacloud.com/help/doc-detail/27714.htm)。
-   实例必须处于 **已停止** 状态。

-   实例创建后不足6小时。

    **说明：** 6小时以后，VPC实例可以通过 [公网IP转换为弹性公网IP](intl.zh-CN/用户指南/实例/修改IP地址/公网IP转换为弹性公网IP.md#) 功能更换公网IP地址，经典网络实例不能再更换公网IP地址。

-   每个实例最多只能更换3次公网IP地址。


## 前提条件 {#section_tv5_w2n_xdb .section}

在更换公网IP地址前，您必须先停止实例。

## 操作步骤 {#section_uv5_w2n_xdb .section}

按以下步骤更换公网IP地址：

1.  登录 [ECS管理控制台](https://ecs.console.aliyun.com/?spm=a2c4g.11186623.2.9.FNEORG#/home)。
2.  在左侧导航栏中，单击 **实例**。
3.  选择地域。
4.  找到更换公网IP地址的实例，在 **操作** 列，选择 **更多** \> **网络和安全组** \> **更换公网IP**。

    **说明：** 如果您的实例创建后已经超过6小时，控制台上不会显示 **更换公网IP** 选项。

5.  在 更换公网IP 对话框中，单击 **开始更换**。

    更换成功后，对话框会显示新的公网IP地址，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9656/15433990175460_zh-CN.png)

6.  单击 **确定** 关闭对话框。

## 相关操作 {#section_yv5_w2n_xdb .section}

您可以 [修改私有IP地址](intl.zh-CN/用户指南/实例/修改IP地址/修改私有IP地址.md#)，但是不能修改经典网络实例的私有IP地址。

