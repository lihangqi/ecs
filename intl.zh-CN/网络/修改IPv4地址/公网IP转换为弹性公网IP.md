# 公网IP转换为弹性公网IP {#concept_l2l_jgn_xdb .concept}

本文档描述了如何将专有网络（VPC）类型的ECS实例分配的公网IP转换为弹性公网IP（EIP），使公网IP地址可以保留，同时又能随时与实例解绑或绑定。

## 约束限制 {#section_asc_kgn_xdb .section}

VPC类型的ECS实例的公网IP转为EIP有以下限制：

-   仅支持分配了公网IP地址的VPC类型的ECS实例。
-   仅支持处于**已停止**（**Stopped**）或**运行中**（**Running**）的VPC类型的ECS实例。其他状态的VPC类型的ECS实例不支持此操作。
-   如果VPC类型的ECS实例有未生效的变更配置任务，不支持此操作。
-   包年包月的VPC类型的ECS实例到期前24小时内，不支持此操作。
-   此功能只支持将公网IP转为EIP，不支持其他转换。

## 使用说明 {#section_mj3_qgn_xdb .section}

-   转换过程不会影响VPC类型的ECS实例的公网接入，不会造成网络闪断。
-   转换前后，公网带宽计费方式不变。
-   转换后EIP将单独计费，单独产生账单。关于EIP计费，请参见[EIP定价](../../../../../intl.zh-CN/产品定价/后付费.md#)。您可以在**费用中心**的[使用记录](https://billing.console.aliyun.com/#/usage/record)，选择导出**弹性公网IP**产品的消费记录。

## 操作步骤 {#section_fsc_kgn_xdb .section}

按以下步骤将VPC类型的ECS实例的公网IP转为EIP：

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。
2.  在左侧导航栏，选择**实例与镜像** \> **实例**。
3.  在顶部状态栏处，选择地域。
4.  找到网络类型为**专有网络**，而且需要转换IP地址的ECS实例，在**操作**列，选择**更多** \> **网络和安全组** \> **公网IP转换为弹性公网IP**。
5.  在弹出的对话框中，确认信息后，单击**确定**。
6.  刷新实例列表。

转换成功后，原来的公网IP地址后面会标注为**弹性**。

您可以单击这个IP地址前往[IP管理控制台](https://vpcnext.console.aliyun.com/eip/cn-shanghai/eips)查看并操作弹性公网IP。

## 后续操作 {#section_jsc_kgn_xdb .section}

转换成功后，您可以解绑EIP并绑定其他实例，也可以释放EIP。具体操作，请参见[解绑EIP](../../../../../intl.zh-CN/用户指南/解绑EIP.md#)。

## API操作 {#section_lsc_kgn_xdb .section}

您可以使用[ConvertNatPublicIpToEip](../intl.zh-CN/API参考/网络/ConvertNatPublicIpToEip.md#)接口将公网IP转换为EIP。目前仅SDK 4.3.0及以上版本支持该功能，请[下载](../intl.zh-CN/SDK参考/SDK.md#)最新版的SDK。

