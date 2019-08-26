# 步骤4：配置IPv6地址 {#concept_jpl_cd2_lgb .concept}

本文描述如何为 Windows 实例自动配置 IPv6 地址和手动配置 IPv6 地址，推荐您使用更高效的自动配置工具配置 IPv6 地址。

## 自动配置 IPv6 地址 {#section_wcs_yfy_wgb .section}

**背景信息**

ecs-util-ipv6 能为已分配 IPv6 地址的 ECS 实例一键配置 IPv6 地址，或者为没有分配 IPv6 地址的 ECS 实例一键清理 IPv6 配置。

**使用限制** 

-   ecs-util-ipv6 工具仅适用于 VPC 类型实例，依赖实例元数据服务，使用前请勿将网络禁用或者将相关出口 IP 端口（100.100.100.200:80）禁用。详情请参见[实例元数据](cn.zh-CN/实例/管理实例/使用实例元数据/什么是实例元数据.md#)。
-   ecs-util-ipv6 工具运行时会自动重启网卡、网络服务，短时间内网络可能会不可用，请慎重执行。

**下载地址** 

-   [Windows Server 2003/2008/2012/2016（32位）](http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/win/32/ecs-utils-ipv6.exe)
-   [Windows Server 2003/2008/2012/2016（64位）](http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/win/64/ecs-utils-ipv6.exe)

**执行方式**

下载与系统版本相对应的脚本到目标系统，使用管理员权限执行：

``` {#codeblock_q3a_xlo_l5b}
ecs-utils-ipv6.exe
```

**执行效果**

如果当前 ECS 已绑定 IPv6 地址，则会自动配置；否则会自动清理原有 IPv6 地址配置。

**自动化脚本示例**

对于需要自动化配置 IPv6 实例的需求，比如大批量配置，建议您使用[云助手](../../../../cn.zh-CN/部署与运维/云助手/云助手概述.md#)或者[实例自定义数据](cn.zh-CN/实例/管理实例/使用实例自定义数据/生成实例自定义数据.md#)配合脚本的方式来调用。以下为脚本示例（假设是 64 位，PowerShell 脚本）。

``` {#codeblock_hlu_83f_du8}
#powershell
$install_dir="C:\Windows\system32"
$install_path = "$install_dir\ecs-utils-ipv6.exe"

if(-not (Test-Path -Path $install_path)){
    # download the tool
    $tool_url = 'http://ecs-image-utils.oss-cn-hangzhou.aliyuncs.com/ipv6/win/64/ecs-utils-ipv6.exe' 
    Invoke-WebRequest -uri $tool_url -OutFile $install_path
    Unblock-File $install_path
}

# run the tool
Start-Process -FilePath "$install_path" -ArgumentList "--noenterkey" -NoNewWindow
```

## 手动配置 IPv6 地址 {#section_hln_xpg_ygb .section}

**检查实例是否已开启 IPv6 服务**

1.  远程连接实例。
2.  打开 Windows 命令处理程序 CMD。
3.  运行 ipconfig，若返回 IPv6 地址相关内容，表示实例已成功开启 IPv6 服务。

若实例还未开启 IPv6 服务，请根据下文描述操作。

**开启 IPv6 服务**

Windows Server 2008/2012/2016 操作步骤

1.  远程连接实例。
2.  选择**控制面板** \> **网络和共享中心** \> **网络连接**。
3.  单击当前网络连接名，打开状态界面，再单击**属性**。
4.  检查 IPv6 协议这一行是否被勾选。如果没有勾选则需要选中，然后单击**确定**。

Windows Server 2003 操作步骤

1.  远程连接实例。
2.  选择**控制面板** \> **网络和共享中心** \> **网络连接**。
3.  单击当前网络连接名，打开状态界面，再单击**属性**。
4.  根据 IPv6 协议是否存在，执行不同操作。
    -   如果存在 IPv6 协议，则勾选**Internet 协议版本 6 （TCP/IPv6）**，再单击**确定**。
    -   如果不存在 IPv6 协议，您需要手动安装 IPv6 协议后勾选**Internet 协议版本 6 （TCP/IPv6）**，再单击**确定**。以下为手动安装 IPv6 协议的操作步骤：
        1.  在本地连接属性页面，单击**安装**，在网络组件类型页面单击**协议** \> **添加**。
        2.  在选择网络协议页面，选择**Microsoft TCP/IP 版本 6** \> **确定**完成安装。

**查询实例的 IPv6 地址**

您可以通过控制台和实例元数据查看实例分配的 IPv6 地址。

-   控制台：请参见[分配 IPv6 地址](cn.zh-CN/网络/配置IPv6地址/Windows实例配置IPv6地址/步骤2：分配IPv6地址.md#)。
-   实例元数据：通过以下元数据项获取 IPv6 地址。详情请参见[实例元数据](cn.zh-CN/实例/管理实例/使用实例元数据/什么是实例元数据.md#)。
    -   IPv6 地址：network/interfaces/macs/\[mac\]/ipv6s
    -   IPv6 网关：network/interfaces/macs/\[mac\]/ipv6-gateway
    -   IPv6 虚拟交换机 CIDR 地址段：network/interfaces/macs/\[mac\]/vswitch-ipv6-cidr-block

**手动配置 IPv6 地址**

Windows Server 2008/2012/2016 操作步骤

1.  远程连接实例。
2.  选择**控制面板** \> **网络**。
3.  单击当前网络连接名，打开状态界面，再单击**属性**。
4.  选择**IPv6协议** \> **属性**。
5.  勾选**使用以下IPv6地址**，并填入 IPv6 地址、子网前缀长度和 IPv6 网关，单击**确定**。
6.  （可选）绑定多个 IPv6 地址：在Internet 协议版本 6（TCP/IP）属性，单击 **高级**打开高级设置界面，单击**添加** 做批量处理。完成后单击 **确定**。

Windows Server 2003 操作步骤

1.  远程连接实例。
2.  选择**控制面板** \> **网络连接**，查看当前网络连接名，假设为**本地连接 2**。
3.  打开 Windows 命令处理程序 CMD。
4.  添加 IPv6 地址。
    -   单个 IPv6 地址运行以下命令：

        ``` {#codeblock_gbu_7el_f82}
        netsh interface ipv6 add address "本地连接 2" <IPv6 地址>
        ```

    -   多个 IPv6 地址运行以下命令：

        ``` {#codeblock_0qf_iap_16e}
        netsh interface ipv6 add address "本地连接 2" <IPv6 地址 1>
        netsh interface ipv6 add address "本地连接 2" <IPv6 地址 2>
        ```

5.  运行以下命令添加默认路由：

    ``` {#codeblock_262_9s4_cf2}
    netsh interface ipv6 add route ::/0 "本地连接 2" <IPv6 网关>
    ```


