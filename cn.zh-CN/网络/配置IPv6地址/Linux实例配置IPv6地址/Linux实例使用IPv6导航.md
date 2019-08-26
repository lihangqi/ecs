# Linux实例使用IPv6导航 {#concept_bwl_slp_fgb .task}

本文介绍了如何为Linux系统的ECS实例使用和配置IPv6的大致流程，供您参考。

ECS实例的网络类型必须是专有网络VPC。在分配IPv6地址前，请先了解[IPv6地址](cn.zh-CN/网络/实例IP地址介绍/IPv6地址.md#)。

## 使用导航 {#section_jep_xe1_529 .section}

使用IPv6的流程图如下所示：

![使用IPv6的流程图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/82533/156585026235066_zh-CN.png)

使用IPv6的步骤如下所示：

1.  搭建IPv6 VPC。详情请参见[步骤1：搭建IPv6 VPC](cn.zh-CN/网络/配置IPv6地址/Linux实例配置IPv6地址/步骤1：搭建IPv6 VPC.md#)。 要在创建ECS实例时分配IPv6地址，您必须先搭建IPv6 VPC。
2.  为ECS实例分配IPv6地址。详情请参见[步骤2：分配IPv6地址](cn.zh-CN/网络/配置IPv6地址/Linux实例配置IPv6地址/步骤2：分配IPv6地址.md#)。 默认情况下，您在新建ECS实例时只分配私网IPv4地址，不分配IPv6地址。如需使用IPv6地址，您需为ECS实例分配IPv6地址。
3.  开通公网带宽。详情请参见[步骤3：开通IPv6公网带宽](cn.zh-CN/网络/配置IPv6地址/Linux实例配置IPv6地址/步骤3：开通IPv6公网带宽.md#)。 创建ECS实例时配置的IPv6地址默认是专有网络VPC内网通信。如果您想通过IPv6地址访问公网或被公网访问，需要开通IPv6公网带宽。
4.  配置IPv6地址。详情请参见[步骤4：配置IPv6地址](cn.zh-CN/网络/配置IPv6地址/Linux实例配置IPv6地址/步骤4：配置IPv6地址.md#)。 您可以为ECS实例自动配置IPv6地址或手动配置IPv6地址，推荐您使用更高效的自动配置工具配置IPv6地址。
5.  添加安全组规则。详情请参见[步骤5：添加IPv6安全组规则](cn.zh-CN/网络/配置IPv6地址/Linux实例配置IPv6地址/步骤5：添加IPv6安全组规则.md#)。 您可以通过添加安全组规则，允许或禁止安全组内的ECS实例对公网或私网的访问。常用案例请参见[安全组应用案例](../../../../cn.zh-CN/安全/安全组/安全组应用案例.md#)。
6.  （可选）删除IPv6地址。详情请参见[步骤6：（可选）删除IPv6地址](cn.zh-CN/网络/配置IPv6地址/Linux实例配置IPv6地址/步骤6：（可选）删除IPv6地址.md#)。 如果您的ECS实例不再需要IPv6地址，您可以删除IPv6地址。删除IPv6地址后，您仍然可以使用IPv4地址。

