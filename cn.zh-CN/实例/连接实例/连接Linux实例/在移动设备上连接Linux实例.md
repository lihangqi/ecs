# 在移动设备上连接Linux实例 {#concept_bln_hhz_wdb .task}

本文介绍了如何在移动设备上连接Linux实例，以SSH Control Lite为例介绍如何在iOS设备上连接Linux实例，以JuiceSSH为例介绍如何在Android设备上连接Linux实例。

-   实例处于**运行中**状态。
-   实例拥有公网IP地址，允许公网访问。
-   您应该已经设置了实例的登录密码。如果密码丢失，您需要重置实例的登录密码。具体步骤，请参见[重置实例登录密码](cn.zh-CN/实例/管理实例/重置实例登录密码.md#)。
-   实例所在的安全组里，您已经添加安全组。具体步骤，请参见[添加安全组规则](../../../../cn.zh-CN/安全/安全组/添加安全组规则.md#)。

    |网络类型|网卡类型|规则方向|授权策略|协议类型|端口范围|授权类型|授权对象|优先级|
    |:---|:---|:---|:---|:---|:---|:---|:---|:--|
    |VPC 网络|不需要配置|入方向|允许|SSH\(22\)|22/22|地址段访问|0.0.0.0/0|1|
    |经典网络|公网|


## 使用SSH Control Lite连接Linux实例 {#section_1k4_15a_pb8 .section}

如果您使用iOS设备，请确保已经安装了SSH Control Lite。本示例中使用用户名和密码进行认证。

1.  启动SSH Control Lite，单击**Hosts**。
2.  在Hosts页面的左上角，单击**+**图标。
3.  在弹出的对话框中，单击**Connection**。
4.  在Connection页面上，输入连接信息后，单击**Save**。输入以下连接信息： 
    -   **Name**：指定Host名称，本示例中，设置为**DocTest**。
    -   **Protocol**：采用默认值**SSH**。
    -   **Host**：输入需要连接的Linux实例的公网 IP 地址。
    -   **Port**：输入端口号**22**。
    -   **Username**：输入用户名**root**。
    -   **Password**：输入实例登录密码。
5.  在页面底部单击**Remote Controls**。
6.  在Remote Controls页面的左上角，单击**+**图标，创建一个新的远程连接会话，本示例中命名为**New remote**。 以上步骤1~步骤6的操作如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/15662663715317_zh-CN.png)

7.  在New remote页面上，单击**Host1**。
8.  在弹出的对话框中，单击**Bind**。
9.  选择刚添加的Linux实例，本示例中为**DocTest**。
10. 在New remote页面的右上角单击**Done**。进入**Edit**状态后，单击**DocTest**。
11. 在弹出菜单中，单击**Connect**。 以上步骤7~步骤11的操作如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/15662663715318_zh-CN.png)

12. 在弹出的提示信息中，根据您的需要，选择**Yes, Once**或**Yes, Permanently**。 连接成功后，**DocTest**前的指示图标会变为绿色。
13. 在New remote页面上，单击**DocTest**。
14. 在弹出的对话框中，单击**Console**，进入Linux实例的管理界面。 以上步骤12~步骤14的操作如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/15662663715319_zh-CN.png)


至此，您已经成功地连接了Linux实例。

## 使用JuiceSSH 连接Linux实例 {#section_euu_1ti_i0n .section}

如果您使用Android设备，请确保已经安装了JuiceSSH。本示例中使用用户名和密码进行认证。

1.  启动JuiceSSH，并单击**Connections**。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/15662663715320_zh-CN.png)

2.  在Connections页面上，单击**+**图标。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/15662663725321_zh-CN.png)

3.  在New Connection页面上，添加连接信息后，单击![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/58642/cn_zh/1503983576102/check%20icon.png)图标。需要添加的连接信息包括： 
    -   **Nickname**：指定连接会话的名称，本示例中，设置为**DocTest**。
    -   **Type**：采用默认值**SSH**。
    -   **Address**：输入需要连接的Linux实例公网 IP 地址。
    -   按以下步骤设置**Identity**：
        1.  单击**Identity**，在下拉列表里选择**New**。
        2.  在New Identity页面上，添加如下信息后，单击![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/58642/cn_zh/1503983576102/check%20icon.png)图标。需要添加的信息包括：
            -   **NickName**：可选项，您可以根据管理需要设置一个身份名称，方便后续管理。本示例中，设置为**DocTest**。
            -   **Username**：输入用户名root。
            -   **Password**：单击**SET\(OPTIONAL\)**后，输入实例登录密码

                ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/15662663725322_zh-CN.png)

    -   **Port**：输入端口号**22**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/15662663725323_zh-CN.png)

4.  确认提示信息后，单击**ACCEPT**。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/15662663725324_zh-CN.png)

5.  第一次连接时，app会提示您如何设置字体等。确认信息后，单击**OK - I’VE GOT IT!**。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/15662663725325_zh-CN.png)


至此，您已经成功连接了Linux实例。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/15662663735326_zh-CN.png)

