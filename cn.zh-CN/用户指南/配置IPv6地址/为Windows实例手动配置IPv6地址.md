# 为Windows实例手动配置IPv6地址 {#concept_s2s_4fx_yfb .concept}

本文描述了如何通过网络连接管理为Windows实例手动配置IPv6 地址。

## 前提条件 {#section_z1h_2ww_yfb .section}

您已经为实例开通了IPv6服务。更多详情，请参见 [为Windows实例开通IPv6服务](cn.zh-CN/用户指南/配置IPv6地址/为Windows实例开通IPv6服务.md#)。

## 步骤 1：查询实例的IPv6地址 {#section_nw4_lww_yfb .section}

您可以通过控制台和实例元数据查看实例分配的IPv6地址。

控制台操作请参阅 [新建实例分配IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/新建实例分配IPv6地址.md#)。

实例元数据请参阅 [实例元数据](cn.zh-CN/用户指南/实例/实例自定义数据和元数据/实例元数据.md#)，并通过以下元数据项获取IPv6地址：

-   IPv6地址：network/interfaces/macs/\[mac\]/ipv6s

-   IPv6网关：network/interfaces/macs/\[mac\]/ipv6-gateway

-   IPv6虚拟交换机CIDR地址段：network/interfaces/macs/\[mac\]/vswitch-ipv6-cidr-block


## 步骤 2：手动配置IPv6地址 {#section_lxr_2jx_yfb .section}

**Windows Server 2008/2012/2016操作步骤**

本文以Windows Server 2008实例为例，为您示范如何加载IPv6服务组件。同样的配置流程适用于Windows Server 2012和Windows Server 2016：

1.  远程连接实例。

2.  选择 **控制面板** \> **网络**。

3.  单击当前网络连接名，打开状态界面，再单击 **属性**。

    ![本地连接属性](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65976/154769548933462_zh-CN.png)

4.  选择 **IPv6协议** \> **属性**。

    ![IPv6协议](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/66243/154769548933501_zh-CN.png)

5.  勾选 **使用以下IPv6地址**，并填入IPv6地址、子网前缀长度和IPv6网关，点击 **确定**。

    ![配置IPv6地址](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/66243/154769548933502_zh-CN.png)

6.  （可选）绑定多个IPv6地址：在Internet 协议版本 6（TCP/IP）属性，点击 **高级** 打开高级设置界面，单击 **添加** 做批量处理。完成后单击 **确定**。

    ![配置多个IPv6地址](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/66243/154769548933503_zh-CN.png)


**Windows Server 2003操作步骤**

1.  远程连接实例。

2.  选择 **控制面板** \> **网络连接**，查看当前网络连接名，假设为 **本地连接 2**。

3.  打开Windows命令处理程序CMD。

4.  添加IPv6地址。

    -   单个IPv6地址运行以下命令：

        ```
        netsh interface ipv6 add address "本地连接 2" <IPv6地址>
        ```

    -   多个IPv6地址运行以下命令：

        ```
        netsh interface ipv6 add address "本地连接 2" <IPv6地址1>
        netsh interface ipv6 add address "本地连接 2" <IPv6地址2>
        ```

5.  运行以下命令添加默认路由：

```
netsh interface ipv6 add route ::/0 "本地连接 2" <IPv6网关>
```


## 相关操作 {#section_emq_n42_lgb .section}

-   如果您不希望手动配置多个IPv6地址，您可以 [为Windows实例自动配置IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/为Windows和Linux实例自动配置IPv6地址.md#)。
-   如果您创建的是Linux实例，您可以 [为Linux实例手动配置IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/为Linux实例手动配置IPv6地址.md#)。
-   如果您的实例不需要IPv6地址，您可以 [删除实例的IPv6地址](cn.zh-CN/用户指南/配置IPv6地址/删除实例的IPv6地址.md#)。删除IPv6地址后，您仍然可以使用IPv4地址。

