# 为Windows实例开通IPv6服务 {#concept_ps2_g4w_yfb .concept}

本文描述了如何在Windows实例系统内查询IPv6服务状态、开通IPv6服务或者禁用IPv6服务。

## 背景信息 {#Background .section}

云服务器ECS支持创建带有IPv6地址的实例。更多详情，请参见 [ECS实例支持IPv6协议](../../../../../cn.zh-CN/产品简介/网络和安全性/IPv6.md#) 和 [新建实例分配IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/新建实例分配IPv6地址.md#)。

## 前提条件 {#section_ffg_cm2_lgb .section}

您已经在 [新建实例分配IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/新建实例分配IPv6地址.md#)或已经 [为已有实例分配IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/为已有实例分配IPv6地址.md#)，但未开通IPv6服务。

## 检查实例是否已开通IPv6服务 {#section_gsy_3sv_yfb .section}

1.  远程连接实例。

2.  打开Windows命令处理程序CMD。

3.  运行 ipconfig，若返回IPv6地址格式相关内容，表示实例已成功开通IPv6服务。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65976/154769550833459_zh-CN.png)


若实例还未开通IPv6服务，请根据下文描述操作。

## 为Windows实例开通IPv6服务 {#section_csy_3sv_yfb .section}

**Windows Server 2008/2012/2016实例**

1.  远程连接实例。

2.  选择 **控制面板** \> **网络和共享中心** \> **网络连接**。

3.  单击当前网络连接名，打开状态界面，再单击 **属性**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65976/154769550833462_zh-CN.png)

4.  检查IPv6协议这一行是否存在并被勾选。如果没有勾选则需要选中，然后单击 **确定**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65976/154769550833463_zh-CN.png)


**Windows Server 2003实例**

1.  参见 [Windows Server 2008/2012/2016实例](cn.zh-CN/用户指南/配置IPv6地址/为Windows实例开通IPv6服务.md#ol_tqk_yqw_yfb) 第1至3步，查看IPv6协议是否存在并被勾选。
2.  如果没有IPv6协议出现，您需要手动安装。
    1.  在本地连接属性页面，单击 **安装**，在网络组件类型页面单击 **协议** \> **添加**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65976/154769550833464_zh-CN.png)

    2.  在 选择网络协议 页面，选择 **Microsoft TCP/IP 版本 6** \> **确定** 完成安装。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65976/154769550833465_zh-CN.png)

3.  勾选 **Internet 协议版本 6 （TCP/IPv6）**，单击 **确定**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65976/154769550833463_zh-CN.png)


## 禁用IPv6服务 {#section_zkn_25w_yfb .section}

1.  远程连接实例。

2.  参阅上文为Windows实例开启IPv6服务，并作反向配置。


## 后续步骤 {#section_dm1_lnx_yfb .section}

您需要为Windows实例配置IPv6地址：

-   [手动配置IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/为Windows实例手动配置IPv6地址.md#)。
-   [自动配置IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/为Windows和Linux实例自动配置IPv6地址.md#)。

