# 新建实例分配IPv6地址 {#concept_dnn_jh4_yfb .concept}

如果您还未创建实例，您可以在新建实例时分配一个IPv6地址。本文为您介绍如何在新建实例时分配IPv6地址。

## 背景信息 {#section_hf1_t32_lgb .section}

默认情况下，您在新建实例时只分配私有IPv4地址，不分配IPv6地址。

## 前提条件 {#section_h4r_4k4_yfb .section}

-   ECS实例的IPv6功能目前处于公测阶段，您需要先 [申请公测](https://page.aliyun.com/form/act608662110/index.htm)。

-   实例所在的VPC和交换机已经开通IPv6网段，详情请参见 [搭建IPv6专有网络](../../../../../cn.zh-CN/快速入门/搭建IPv6专有网络.md#)。


## 操作步骤 {#section_dyh_4k4_yfb .section}

您可以按照 [使用向导创建实例](cn.zh-CN/用户指南/实例/创建实例/使用向导创建实例.md#) 的描述创建实例。在选择配置时，您需要注意以下几点：

-   在 基础配置 页面，筛选出 **支持IPv6** 的实例规格，并选择一个实例规格。

    ![选择实例](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65336/154769554833467_zh-CN.png)

-   在 网络和安全组 页面，选择已开通IPv6的专有网络和交换机，并勾选 **免费分配 IPv6 地址**。

**说明：** 新建实例分配的IPv6地址默认是VPC内网通信。要使用IPv6地址进行公网通信，请 [开通IPv6公网带宽](../../../../../cn.zh-CN/用户指南/管理IPv6公网带宽/开通IPv6公网带宽.md#)。

![配置网络和安全组](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65336/154769554833531_zh-CN.png)

-   在 确认订单 页面，确认已选择IPv6地址。

    ![确认选择IPv6地址](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65336/154769554833488_zh-CN.png)


## 后续步骤 {#section_cyt_vh2_lgb .section}

-   （可选）您可以[查看分配的IPv6地址](cn.zh-CN/.md#)。
-   创建实例时配置的IPv6地址默认是VPC内网通信。如果您想通过IPv6地址访问公网或被公网访问，需要[开通IPv6公网带宽](../../../../../cn.zh-CN/用户指南/管理IPv6公网带宽/开通IPv6公网带宽.md#)。

