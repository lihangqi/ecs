# IPv6使用导航 {#concept_bwl_slp_fgb .concept}

本文介绍了IPv6的使用流程及常用配置，便于您参考。

## 流程图 {#section_sl1_lqp_fgb .section}

在分配IPv6地址前，请先了解[IPv6地址](cn.zh-CN/网络/实例IP地址介绍/IPv6地址.md#)。

使用IPv6的流程图如下：

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/82533/155141993135066_zh-CN.png)

1.  搭建 IPv6 VPC。

    仅 VPC 类型的 ECS 实例支持 IPv6 地址。要在创建实例时分配 IPv6 地址，必须先搭建 IPv6 VPC。

2.  为实例分配 IPv6 地址。

    默认情况下，您在新建实例时只分配私网 IPv4 地址，不分配 IPv6 地址。如需使用 IPv6 地址，您需为实例分配 IPv6 地址。

3.  开通公网带宽。

    创建实例时配置的 IPv6 地址默认是 VPC 内网通信。如果您想通过 IPv6 地址访问公网或被公网访问，需要开通 IPv6 公网带宽。

4.  配置 IPv6 地址。

    您可以为实例自动配置 IPv6 地址和手动配置 IPv6 地址，推荐您使用更高效的自动配置工具配置 IPv6 地址。

5.  添加安全组规则。

    您可以通过添加安全组规则，允许或禁止安全组内的 ECS 实例对公网或私网的访问，常用案例请参见[安全组应用案例](../../../../../cn.zh-CN/安全/安全组/安全组应用案例.md#)。

6.  （可选）删除 IPv6 地址。

    如果您的实例不再需要 IPv6 地址，您可以删除 IPv6 地址。删除 IPv6 地址后，您仍然可以使用 IPv4 地址。


