# Connect to an instance on a mobile device {#concept_bln_hhz_wdb .concept}

This documentation describes how to connect to an ECS instance on a mobile device. The procedure varies with the operating system of your instance.

-   [Connect to a Linux instance](#linux): We take SSH Control Lite as an example to describe how to connect to a Linux instance on an iOS device, and JuiceSSH to describe how to connect to a Linux instance on an Android device.
-   [Connect to Windows instances](#windows): We take Microsoft Remote Desktop as an example to describe how to connect to a Windows instance on an iOS or Android device.

## Connect to a Linux instance {#linux .section}

**Prerequisites**

Confirm the following before connecting to your instance:

-   The instance is **Running** .
-   The instance has a public IP address and is accessible from public network.
-   You have set the logon password for the instance. If the password is lost, you must [reset the instance password](intl.en-US/User Guide/Instances/Reset an instance password.md#).
-   The security group of the instance has the [the following security group rules](intl.en-US/User Guide/Security groups/Add security group rules.md#):

    |Network type|NIC|Rule direction|Authorization policy|Protocol type|Port range|Authorization type|Authorization object|Priority|
    |:-----------|:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
    |VPC |No configuration required|Inbound|Allow|SSH\(22\)|22/22|Address Field Access|0.0.0.0/0|1|
    |Classic |Internet|

-   You have downloaded and installed the appropriate app:
    -   The iOS device has SSH Control Lite installed.
    -   The Android device has JuiceSSH installed.

**Procedure**

For iOS devices, see [Use SSH Control Lite  to connect to a Linux instance](#SshControlLite). In this example, user name and password are used for authentication.

For Android devices, see  [Use JuiceSSH to connect  to a Linux instance](#JuiceSsh). In this example, user name and password are used for the authentication.

**Use SSH Control Lite to connect to a Linux instance**

1.  Start SSH Control Lite, and tap **Hosts**.
2.  Tap the **+** icon in the upper left corner of the Hosts page.
3.  In the action sheet, tap **Connection**.
4.  On the Connection page, set the connection information and tap ****. The following connection information is required:
    -   Name: Specify the Host name. DocTest is used in this example. .
    -   Protocol: Use the default value SSH.
    -   Host: Type the public IP address of the Linux instance to connect to.
    -   Port: Type the port number for SSH protocol. 22 is used in this example.
    -   Username: Type root for the user name.
    -   Password: Type the logon password of the instance.
5.  In the tool bar, tap **Remote Controls**.
6.  On the Remote Controls page, tap the**+** icon in the upper left corner to create a remote connection session. New remote is used in this example.

    The following figure shows Steps 1 through 6. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/5317_en-US.png)

7.  On the New remote page, tap **Host1**.
8.  In the action sheet, tap **Bind**.
9.  Select the new Linux instance. In this example, select DocTest.
10. On the New remote page, tap **Done** to switch it to the **Edit** mode, and then tap **DocTest**.
11. In the action sheet, tap **Connect**.

    The following figure shows Steps 7 through 11.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/5318_en-US.png)

12. In the action sheet, select **Yes, Once** or **Yes,  Permanently**. Once the connection is successful, the indicator in front of **DocTest** turns green.
13. On the New remote page, tap **DocTest**.
14. In the action sheet, tap **Console** to open Linux instance console.

    The following figure shows Steps 12 through 14:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/5319_en-US.png)


Now, you are connected to the Linux instance.

**Use JuiceSSH to connect to a Linux instance**

1.  Start JuiceSSH, and tap **Connections**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/5320_en-US.png)

2.  Under the Connections tab, tap the **+** icon.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/5321_en-US.png)

3.  On the New Connection page, add the connection information and tap the ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/58642/cn_zh/1503983576102/check%20icon.png) icon. The following connection information is required:
    -   Nickname: Specify the name of the connection session. DocTest is used in this example.
    -   Type: Use the default value SSH.
    -   Address: Type the public IP address of the Linux instance to connect to.
    -   To setI Identity, follow these steps:
        1.  Tap **Identity**, and tap **New**in the drop-down list.
        2.  On the New Identitypage, add the following information and tap the  ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/58642/cn_zh/1503983576102/check%20icon.png) icon. The following connection information is required:
            -   Nickname: Optional. You may set a nickname  to ease management.  DocTest is used in this example.
            -   Username: Type root for the user name.
            -   Password: Tap **SET\(OPTIONAL\)**, and type the logon password of the instance.

                ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/5322_en-US.png)

    -   Port: Type the port number for SSH protocol. In this example, 22 is used.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/5323_en-US.png)

4.  Confirm the message, and tap**ACCEPT**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/5324_en-US.png)

5.  \(Optional\) For the first connection, the app would offer you some tips about font setting and the like. Confirm the message, and tap **OK - I’VE GOT IT!**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/5325_en-US.png)


Now, you are connected to the Linux instance.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/5326_en-US.png)

## Connect to Windows instances {#windows .section}

In this section, we take Microsoft Remote Desktop as an example to describe how to use an app to connect to a Windows instance on a mobile device.

**Prerequisites**

Confirm the following before connecting to your instance:

-   The instance is **Running**.
-   The instance has a public IP address and is accessible from public network.
-   You have set the logon password for the instance. If the password is lost, you must [reset the instance password](intl.en-US/User Guide/Instances/Reset an instance password.md#).
-   The security group of the instance has [the following security group rules](intl.en-US/User Guide/Security groups/Add security group rules.md#):

    |Network type|NIC|Rule direction|Authorization policy|Protocol type|Port range|Authorization type|Authorization object|Priority|
    |:-----------|:--|:-------------|:-------------------|:------------|:---------|:-----------------|:-------------------|:-------|
    |VPC |No configuration required|Inbound|Allow|RDP\(3389\)|3389/3389|Address field access|0.0.0.0/0|1|
    |Classic |Internet|

-   You have downloaded and installed Microsoft Remote Desktop.
    -   For iOS devices, download the app from iTunes.
    -   For Android devices, download the app from Google Play.

**Procedure**

To connect to a Windows instance by using Microsoft Remote Desktop, follow these steps:

1.  Start RD Client. In the navigation bar, tap the**+** icon.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/5327_en-US.PNG)

2.  On the Add New page, select**Desktop**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/5329_en-US.PNG)

3.  On the Edit Desktop page, type the connection information and tap **Save**.  The following connection information is required:
    -   PC Name: Type the public IP address of the Windows instance to connect to.
    -   User Account: Type the account name administrator and the logon password of the Windows instance.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/5330_en-US.PNG)

4.  On the Remote Desktop page, tap the icon of a Windows instance.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/5331_en-US.PNG)

5.  On the confirmation page, confirm the message and tap **Accept**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/5332_en-US.PNG)


Now, you are connected to the Windows instance.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9623/5333_en-US.PNG)

