# 为Windows实例配置IPv6服务 {#concept_ps2_g4w_yfb .concept}

本文描述了如何在 Windows 实例系统内查询 IPv6 服务状态、配置 IPv6 服务或者禁用 IPv6 服务。

## 背景信息 {#Background .section}

云服务器 ECS 支持创建带有 IPv6 地址的实例。更多详情，请参阅 [ECS 实例支持 IPv6 协议](../../../../cn.zh-CN/产品简介/网络和安全性/IPv6.md#) 和 [创建实例时配置 IPv6 地址](cn.zh-CN/用户指南/配置IPv6地址/创建实例时配置IPv6地址.md#)。

若您的实例已经分配了 IPv6 地址但未开启服务模块，可以根据本文描述为实例加载 IPv6 服务。

## 检查实例是否已开启 IPv6 服务 {#section_gsy_3sv_yfb .section}

1.  远程连接实例。

2.  打开 Windows 命令处理程序 CMD。

3.  运行 ipconfig，若返回 IPv6 地址格式相关内容，表示实例已成功开启 IPv6 服务。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65976/154390915933459_zh-CN.png)


若实例还未开启 IPv6 服务，请根据下文描述操作。

## 为 Windows 实例开启 IPv6 服务 {#section_csy_3sv_yfb .section}

本文以 Windows Server 2008 实例为例，为您示范如何加载 IPv6 服务组件。

1.  远程连接实例。

2.  选择 **控制面板** \> **网络和共享中心** \> **网络连接**。

3.  单击当前网络连接名，打开状态界面，再单击 **属性**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65976/154390915933462_zh-CN.png)

4.  检查 IPv6 协议这一行是否存在并被勾选。如果没有勾选则需要选中，然后点击 **确定**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65976/154390915933463_zh-CN.png)

5.  （Windows Server 2003系统）如果没有 IPv6 协议出现，您需要手动安装：在本地连接属性页面，单击 **安装**，在网络组件类型页面单击 **协议** \> **添加**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65976/154390915933464_zh-CN.png)

6.  （Windows Server 2003系统）在 选择网络协议 页面，选择 **Microsoft TCP/IP 版本 6** \> **确定** 完成安装。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65976/154390915933465_zh-CN.png)


## 禁用 IPv6 服务 {#section_zkn_25w_yfb .section}

1.  远程连接实例。

2.  参阅上文为 Windows 实例开启 IPv6 服务，并作反向配置。


## 下一步 {#section_dm1_lnx_yfb .section}

[为Windows实例配置静态IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/为Windows实例配置静态IPv6地址.md#)

