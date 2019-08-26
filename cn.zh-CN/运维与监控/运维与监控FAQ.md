# 运维与监控FAQ {#concept_zbs_spr_wgb .concept}

本文汇总了使用云服务器ECS运维与监控功能时的常见问题。

-   云助手问题
    -   [什么是云助手？](#section_os2_4bh_vgb)
    -   [我如何使用云助手？](#section_ss2_4bh_vgb)
    -   [云助手支持哪些操作系统类型？](#section_ts2_4bh_vgb)
    -   [我最多能保有多少条云助手命令？](#section_ws2_4bh_vgb)
    -   [我可以修改已经创建的命令吗？](#section_xs2_4bh_vgb)
    -   [在实例中执行命令有权限限制吗？](#section_ys2_4bh_vgb)
    -   [可以同时在多台实例上执行云助手命令吗？](#section_at2_4bh_vgb)
    -   [我如何查看是否成功执行了命令？](#section_bt2_4bh_vgb)

## 什么是云助手？ {#section_os2_4bh_vgb .section}

云助手是云服务器ECS原生的运维部署服务，支持可视化控制台和API操作。无需远程连接实例，云助手便能帮您批量执行Bat、PowerShell或者Shell命令。更多详情，请参见[云助手](../cn.zh-CN/运维与监控/云助手/云助手概述.md)。

## 我如何使用云助手？ {#section_ss2_4bh_vgb .section}

您可以通过[ECS管理控制台](https://ecs.console.aliyun.com/)或者[API](../cn.zh-CN/API参考/云助手/CreateCommand.md#)使用云助手。

## 云助手支持哪些操作系统类型？ {#section_ts2_4bh_vgb .section}

云助手支持主流Windows Server和类Unix操作系统，具体操作系统版本如下所示：

-   Windows：Windows Server 2008、2012和2016
-   类Unix：Ubuntu 12/14/16、CentOS 5/6/7、Debian 7/8/9、RedHat 5/6/7、SUSE Linux Enterprise Server 11/12、OpenSUSE、Aliyun Linux和CoreOS

**说明：** 

-   使用ECS公共镜像创建的实例会默认安装云助手客户端。
-   使用自定义镜像或者云市场镜像创建的实例需要您首先确认操作系统是否支持云助手，再自行[安装云助手客户端](../cn.zh-CN/运维与监控/云助手/配置云助手客户端.md#)。

## 我最多能保有多少条云助手命令？ {#section_ws2_4bh_vgb .section}

在一个阿里云地域下，根据您的云服务器使用情况而定，您可以保有100到10000条云助手命令。

## 我可以修改已经创建的命令吗？ {#section_xs2_4bh_vgb .section}

您可以修改云助手命令的名称和描述。为确保周期命令的一致性，不支持修改命令内容、超时时间和执行路径等信息。

如果您需要调整命令内容或执行路径，可以[克隆命令](../cn.zh-CN/运维与监控/云助手/使用云助手/管理命令.md#CopyCommands)，在目标命令的基础新建命令版本。

## 在实例中执行命令有权限限制吗？ {#section_ys2_4bh_vgb .section}

有。您需要以管理员的身份安装和使用云助手：

-   Windows实例的管理员为administrator。
-   Linux实例的管理员为root。

## 可以同时在多台实例上执行云助手命令吗？ {#section_at2_4bh_vgb .section}

可以。一次执行命令操作最多可以选择50台实例。在一个阿里云地域下，您每天最多能执行5000次云助手命令。

## 我如何查看是否成功执行了命令？ {#section_bt2_4bh_vgb .section}

执行云助手命令与您登录实例后执行命令一样，只有命令所需条件满足后才会执行成功。您可以选择以下任一方式查看命令结果：

-   [ECS管理控制台](https://ecs.console.aliyun.com/)
-   [DescribeInvocationResults](../cn.zh-CN/API参考/云助手/DescribeInvocationResults.md#)
-   远程连接实例后，查看日志文件：
    -   Windows：C:\\ProgramData\\aliyun\\assist\\$\{version\}\\log\\aliyun\_assist\_main.log
    -   Linux：/usr/local/share/aliyun-assist/$\{version\}/log/aliyun\_assist\_main.log 

        变量$\{version\}是云助手客户端在目标实例上的版本号，例如1.0.1.226。


