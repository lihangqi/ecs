# 实例RAM角色概述 {#concept_kbp_r1t_xdb .concept}

ECS实例RAM（Resource Access Management）角色让ECS实例扮演具有某些权限的角色，从而赋予实例一定的访问权限。

## 背景信息 {#section_rsm_x1t_xdb .section}

实例RAM角色允许您将一个角色关联到ECS实例，在实例内部基于STS（Security Token Service）临时凭证（临时凭证将周期性更新）访问其他云产品的API。一方面可以保证AccessKey安全，另一方面也可以借助RAM实现权限的精细化控制和管理。关于角色的详细描述，请参见[角色](../../../../cn.zh-CN/用户指南/（隐藏）旧版用户指南/身份管理/角色.md#)。

一般情况下，ECS实例的应用程序是通过用户账号或者RAM用户的AccessKey访问阿里云各产品的API。详情请参见[RAM用户](../../../../cn.zh-CN/用户指南/（隐藏）旧版用户指南/身份管理/用户.md#)。

为了满足调用需求，需要直接把AccessKey固化在实例中，如写在配置文件中。但是这种方式权限过高，存在泄露信息和难以维护等问题。因此，阿里云推出了实例RAM角色解决这些问题。

## 功能优势 {#section_ssm_x1t_xdb .section}

使用实例RAM角色，您可以：

-   借助实例RAM角色，将角色和ECS实例关联起来。
-   安全地在ECS实例中使用STS临时凭证访问阿里云的其他云服务，例如OSS、ECS、RDS等。
-   为不同的实例赋予包含不同授权策略的角色，使它们对不同的云资源具有不同的访问权限，实现更精细粒度的权限控制。
-   无需自行在实例中保存AccessKey，通过修改角色的授权即可变更权限，快捷地维护ECS实例所拥有的访问权限。

## 费用详情 {#section_usm_x1t_xdb .section}

赋予云服务器ECS实例RAM角色不会产生额外的费用。

## 使用限制 {#section_vsm_x1t_xdb .section}

使用实例RAM角色存在如下限制：

-   只有专有网络（VPC）类型的实例才能使用实例RAM角色。
-   一个ECS实例一次只能授予一个实例RAM角色。

## 相关链接 {#section_vwf_kbt_xdb .section}

-   如果您要了解支持STS临时凭证的云服务，请参见[支持RAM的云服务](../../../../cn.zh-CN/产品简介/支持RAM的云服务.md#)。
-   如果您要了解如何访问其他云产品的API，请参见[借助于实例RAM角色访问其他云产品](../../../../cn.zh-CN/最佳实践/借助于实例RAM角色访问其他云产品.md#)。

