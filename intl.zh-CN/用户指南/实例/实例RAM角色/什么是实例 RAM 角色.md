# 什么是实例 RAM 角色 {#concept_kbp_r1t_xdb .concept}

ECS 实例 RAM（Resource Access Management） 角色（以下简称实例 RAM 角色）是 RAM 角色的一种，它让 ECS 实例扮演具有某些权限的角色，从而赋予实例一定的访问权限。

实例 RAM 角色允许您将一个 [角色](../../../../intl.zh-CN/用户指南/身份管理/角色.md#) 关联到 ECS 实例，在实例内部基于 STS （Security Token Service）临时凭证（临时凭证将周期性更新）访问其他云产品的 API。一方面可以保证 AccessKey 安全，另一方面也可以借助 RAM 实现权限的精细化控制和管理。

## 背景信息 {#section_rsm_x1t_xdb .section}

一般情况下，ECS 实例的应用程序是通过用户账号或者 [RAM 用户](../../../../intl.zh-CN/用户指南/身份管理/用户.md#) 的 AccessKey （AccessKeyId + AccessKeySecret）访问阿里云各产品的 API。

为了满足调用需求，需要直接把 AccessKey 固化在实例中，如写在配置文件中。但是这种方式权限过高，存在泄露信息和难以维护等问题。因此，阿里云推出了实例 RAM 角色解决这些问题。

## 功能优势 {#section_ssm_x1t_xdb .section}

使用实例 RAM 角色，您可以：

-   借助实例 RAM 角色，将 [角色](../../../../intl.zh-CN/用户指南/身份管理/角色.md#) 和 ECS 实例关联起来。

-   安全地在 ECS 实例中使用 STS 临时凭证访问阿里云的其他云服务，如 OSS、ECS、RDS 等。

-   为不同的实例赋予包含不同授权策略的角色，使它们对不同的云资源具有不同的访问权限，实现更精细粒度的权限控制。

-   无需自行在实例中保存 AccessKey，通过修改角色的授权即可变更权限，快捷地维护 ECS 实例所拥有的访问权限。


## 费用详情 {#section_usm_x1t_xdb .section}

赋予云服务器 ECS 实例 RAM 角色不会产生额外的费用。

## 使用限制 {#section_vsm_x1t_xdb .section}

使用实例 RAM 角色存在如下限制：

-   只有专有网络 （VPC） 网络类型的实例才能使用实例角色。

-   一个 ECS 实例一次只能授予一个实例 RAM 角色。


## 使用实例 RAM 角色 {#section_xsm_x1t_xdb .section}

目前有两种使用 RAM 角色的方式：

-   [通过控制台使用实例 RAM 角色](intl.zh-CN/用户指南/实例/实例RAM角色/通过控制台使用实例 RAM 角色.md#)

-   [通过 API 使用实例 RAM 角色](intl.zh-CN/用户指南/实例/实例RAM角色/通过 API 使用实例 RAM 角色.md#)


## 参考链接 {#section_vwf_kbt_xdb .section}

-   您可以参阅 [支持 RAM 的云服务](../../../../intl.zh-CN/产品简介/支持 RAM 的云服务.md#) 了解支持 STS 临时凭证的云服务。

-   您可以参阅 [借助于实例 RAM 角色访问其他云产品](../../../../intl.zh-CN/最佳实践/借助于实例 RAM 角色访问其他云产品.md#) 了解如何访问其他云产品的 API 。


