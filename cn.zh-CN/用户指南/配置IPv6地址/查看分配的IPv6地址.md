# 查看分配的IPv6地址 {#concept_jpl_cd2_lgb .concept}

如果您已为新建实例或已有实例分配了IPv6地址，您可以查看系统分配的IPv6地址。

## 前提条件 {#section_gvw_td2_lgb .section}

您已经在[新建实例时分配了IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/新建实例分配IPv6地址.md#)或已经[为已有实例分配了IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/为已有实例分配IPv6地址.md#)。

## 操作步骤 {#section_vhx_1s4_yfb .section}

1.  登录[云服务器ECS管理控制台](https://ecs.console.aliyun.com/#/home)。

2.  在左侧导航栏中，单击 **实例**。

3.  找到已创建的ECS实例，在 **操作** 列，单击 **管理**。

4.  在 **配置信息** 区域中，可以查看实例分配的 IPv6地址。

    ![查看IPv6地址](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/100331/154872706437113_zh-CN.png)


## 后续步骤 {#section_upd_t22_lgb .section}

-   创建实例时配置的IPv6地址默认是VPC内网通信。如果您想通过IPv6地址访问公网或被公网访问，需要[开通IPv6公网带宽](../../../../../cn.zh-CN/用户指南/管理IPv6公网带宽/开通IPv6公网带宽.md#)。
-   如果您的实例已经分配了IPv6地址但未配置IPv6服务，您必须开通IPv6服务：
    -   [为Windows实例开通IPv6服务](cn.zh-CN/用户指南/配置IPv6地址/为Windows实例开通IPv6服务.md#)。
    -   [为Linux实例开通IPv6服务](cn.zh-CN/用户指南/配置IPv6地址/为Linux实例开通IPv6服务.md#)。

