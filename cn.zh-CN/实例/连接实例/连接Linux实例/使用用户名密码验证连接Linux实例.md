# 使用用户名密码验证连接Linux实例 {#concept_rsl_2vx_wdb .task}

本文仅介绍如何使用用户名和密码验证远程连接 Linux 实例。

-   实例必须处于**运行中**状态。如果实例未运行，请启动实例。具体步骤，请参见[启动实例](cn.zh-CN/实例/管理实例/启动和停止实例.md#)。
-   实例已经设置登录密码。如果未设置密码或密码丢失，请重置密码。具体步骤，请参见[重置密码](cn.zh-CN/实例/管理实例/重置实例登录密码.md#)。
-   实例能访问公网。
    -   专有网络（VPC）下，在创建实例时购买带宽从而分配到一个公网 IP 地址，或者在创建实例后绑定一个弹性公网IP地址。具体操作，请参见[绑定一个弹性公网 IP 地址](../../../../cn.zh-CN/快速入门/搭建IPv4专有网络.md#section_ux1_cmw_rdb)。
    -   经典网络下，您的实例必须分配了公网 IP 地址。以下是获取公网 IP 地址的方法：
        -   无论是包年包月实例还是按量付费实例，只要您在创建实例时购买了带宽就会被分配一个公网 IP 地址。
        -   如果您在创建包年包月实例时未设置带宽，可以通过升降配方式获取公网 IP 地址。详情请参见[升降配](cn.zh-CN/实例/升降配实例/升降配方式汇总.md#)。
-   实例所在的安全组必须添加以下安全组规则（具体操作，请参见[添加安全组规则](../../../../cn.zh-CN/安全/安全组/添加安全组规则.md#)）：

    |网络类型|网卡类型|规则方向|授权策略|协议类型|端口范围|授权类型|授权对象|优先级|
    |----|----|----|----|----|----|----|----|---|
    |VPC|不需要配置|入方向|允许|SSH\(22\)|22/22|地址段访问|0.0.0.0/0|1|
    |经典网络|公网|


## 操作方式 {#section_liu_n08_jmj .section}

根据本地设备的操作系统，您可以用不同的方式使用 SSH 协议远程连接 Linux 实例：

-   [本地设备使用 Windows 操作系统](#section_k1p_o74_bwm)
-   [本地设备使用 Linux 或 Mac OS X 系统](#section_zo7_ddd_8yk)
-   [本地设备使用 Android 或 iOS 系统](#section_x5j_164_ejd)

## 本地设备使用 Windows 操作系统 {#section_k1p_o74_bwm .section}

如果本地设备使用 Windows 操作系统，您可以使用远程连接软件（如 PuTTY）连接 Linux 实例。本文档以 PuTTY 为例说明如何远程连接 Linux 实例。执行以下操作前，请先下载Putty。下载路径：[下载 PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/)。

**说明：** 具体操作，您也可以观看视频：[小助手系列之如何远程连接 Linux 实例](https://help.aliyun.com/document_detail/62304.html)。

当 PuTTY 的界面上出现`Welcome to Alibaba Cloud Elastic Compute Service !`时，表示您已经成功连接到实例。

1.  双击putty.exe，启动程序，进入 PuTTY 主界面。
2.  配置**Session**。 
    -   **Host Name**：输入实例的公网 IP 地址或弹性公网 IP 地址。
    -   **Port**：输入 **22**。
    -   **Connection Type**：选择 **SSH**。
    -   （可选）**Saved Session**：如果您希望以后不再输入上述信息直接进入登录界面，可以在这里为这个会话指定一个便于识别的名称，再单击 **Save** 保存。

        ![](images/5249_zh-CN.gif)

3.  单击**Open**进入登录页面。 

    **说明：** 首次连接时会出现以下警告，表示PuTTY无法确认远程服务器（实例）的真实性，只能提供服务器的公钥指纹，需要您确认是否信任该服务器，并将其公钥指纹加入到本地机器的注册表中。一般选择**是**。之后，如果您登录时再次弹出这个警告，表示您的实例可能发生了[中间人攻击](https://yq.aliyun.com/articles/209748)。关于这个警告更详细的信息，请参见[PuTTY官网文档](https://the.earth.li/~sgtatham/putty/0.70/htmldoc/Chapter2.html#gs-hostkey)。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9621/15651333345251_zh-CN.png)

4.  根据提示，分别输入您 ECS 实例的用户名（默认为 root）和密码，并回车确认。 

    **说明：** 一般 Linux 系统不会显示密码的输入过程。

    当 PuTTY 的界面上出现`Welcome to Alibaba Cloud Elastic Compute Service !`时，表示您已经成功连接到实例。

    **说明：** 如果出现`Disconnected:No supported authentication methods available`错误，请单击 [此处](https://help.aliyun.com/knowledge_detail/41489.html)获取解决方法。


至此，您可以开始操作您的实例了。

## 本地设备使用 Linux 或 Mac OS X 系统 {#section_zo7_ddd_8yk .section}

1.  输入 SSH 命令连接：`ssh root@实例的(弹性)公网 IP`。
2.  输入实例登录密码。 

    当界面上出现`Welcome to Alibaba Cloud Elastic Compute Service !`时，表示您已经成功连接到实例。


至此，您可以开始操作您的实例了。

## 本地设备使用 Android 或 iOS 系统 {#section_x5j_164_ejd .section}

如果您需要从移动设备上远程连接 Linux 实例，您可以使用 app 连接。根据移动设备的操作系统不同，您可以有不同的选择。具体的操作描述，请参见[在移动设备上连接Linux实例](cn.zh-CN/实例/连接实例/连接Linux实例/在移动设备上连接Linux实例.md#)。

**相关文档**  


[使用SSH密钥对连接Linux实例](cn.zh-CN/实例/连接实例/连接Linux实例/使用SSH密钥对连接Linux实例.md#)

[使用管理终端连接Linux实例](cn.zh-CN/实例/连接实例/连接Linux实例/使用管理终端连接Linux实例.md#)

[无法连接Linux实例](https://help.aliyun.com/document_detail/34403.html)

