# 在移动设备上连接Windows实例 {#concept_smr_xnw_wgb .concept}

本文介绍了如何在移动设备上连接Windows实例，以微软公司发行的Microsoft Remote Desktop为例，介绍如何在iOS设备或Android设备上连接Windows实例。

## 前提条件 {#section_unw_brq_pgb .section}

在连接之前，您应先确认以下事项：

-   实例处于 **运行中** 状态。
-   实例拥有公网 IP 地址，允许公网访问。
-   您应该已经设置了实例的登录密码。如果密码丢失，您需要 [重置实例登录密码](cn.zh-CN/实例/管理实例资源/重置实例登录密码.md#)。
-   实例所在的安全组里，您已经 [添加安全组规则](../../../../../cn.zh-CN/安全/安全组/添加安全组规则.md#)：

    |网络类型|网卡类型|规则方向|授权策略|协议类型|端口范围|授权类型|授权对象|优先级|
    |:---|:---|:---|:---|:---|:---|:---|:---|:--|
    |VPC 网络|不需要配置|入方向|允许|SSH\(22\)|22/22|地址段访问|0.0.0.0/0|1|
    |经典网络|公网|


## 操作步骤 {#windows .section}

请确保已经安装了 Microsoft Remote Desktop。

1.  启动 RD Client。在页面右上角，单击 **+**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/15510766285327_zh-CN.PNG)

2.  在 Add New 页面，选择 **桌面**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/15510766285329_zh-CN.PNG)

3.  在 编辑桌面 页面，设置连接信息后，单击 **保存**。需要设置的连接信息包括：
    -   **PC 名称**：输入需要连接的 Windows 实例的公网 IP 地址。
    -   **用户帐户**：输入 Windows 实例账号 **administrator**，并输入实例登录密码。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/15510766285330_zh-CN.PNG)

4.  在 远程桌面 页面，单击需要连接的 Windows 实例图标。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/15510766285331_zh-CN.PNG)

5.  在验证确认页面，确认信息后，单击 **接受**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/15510766285332_zh-CN.PNG)


至此，您已经成功连接到 Windows 实例。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/15510766285333_zh-CN.PNG)

