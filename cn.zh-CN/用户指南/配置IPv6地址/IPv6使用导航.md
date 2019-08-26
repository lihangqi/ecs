# IPv6使用导航 {#concept_bwl_slp_fgb .concept}

本文介绍了IPv6的使用流程及常用配置，便于您参考。

## 流程图 {#section_sl1_lqp_fgb .section}

在分配IPv6地址前，请先了解[IPv6](../../../../../cn.zh-CN/产品简介/网络和安全性/IPv6.md#)。

使用IPv6的流程图如下：

![IPv6使用导航](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/82533/154769556835066_zh-CN.png)

1.  搭建IPv6 VPC。

    仅VPC类型的ECS实例支持IPv6地址。要在创建实例时分配IPv6地址，必须先搭建IPv6 VPC。

    -   如果您还未创建VPC，您可以[在创建VPC时开通IPv6](../../../../../cn.zh-CN/用户指南/使用IPv6/开通IPv6.md#section_ngq_1xd_2gb)。
    -   如果您已经创建了VPC，您可以[为已有VPC开通IPv6](../../../../../cn.zh-CN/用户指南/使用IPv6/开通IPv6.md#section_a3d_bk2_2gb)。
2.  为实例分配IPv6地址。
    -   如果您还未创建实例，您可以[新建实例时分配IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/新建实例分配IPv6地址.md#)。
    -   如果您已经创建了实例，您可以[为已有实例分配IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/为已有实例分配IPv6地址.md#)。
3.  开通公网带宽。

    创建实例时配置的IPv6地址默认是VPC内网通信。如果您想通过IPv6地址访问公网或被公网访问，需要[开通IPv6公网带宽](../../../../../cn.zh-CN/用户指南/管理IPv6公网带宽/开通IPv6公网带宽.md#)。

4.  开通IPv6服务。

    如果您的实例已经分配了IPv6地址但未配置IPv6服务，您必须开通IPv6服务：

    -   [为Windows实例开通IPv6服务](cn.zh-CN/用户指南/配置IPv6地址/为Windows实例开通IPv6服务.md#)。
    -   [为Linux实例开通IPv6服务](cn.zh-CN/用户指南/配置IPv6地址/为Linux实例开通IPv6服务.md#)。
5.  配置IPv6地址。

    开通IPv6服务之后，您还需为实例配置IPv6地址：

    -   自动配置：[为Windows和Linux实例自动配置 IPv6 地址](cn.zh-CN/用户指南/配置IPv6地址/为Windows和Linux实例自动配置IPv6地址.md#)。
    -   手动配置：
        -   [为Windows实例手动配置IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/为Windows实例手动配置IPv6地址.md#)。
        -   [为Linux实例手动配置IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/为Linux实例手动配置IPv6地址.md#)。
6.  添加安全组规则。

    您可以通过[添加安全组规则](cn.zh-CN/用户指南/安全组/添加安全组规则.md#)，允许或禁止安全组内的ECS实例对公网或私网的访问，常用案例请参见[安全组规则的典型应用](cn.zh-CN/用户指南/安全组/安全组规则的典型应用.md#)。

7.  （可选）删除IPv6地址。

    如果您的实例不再需要IPv6地址，您可以[删除IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/删除实例的IPv6地址.md#)。删除IPv6地址后，您仍然可以使用IPv4地址。


