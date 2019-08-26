# Connect to a Linux instance by using a password {#concept_rsl_2vx_wdb .concept}

You can connect to a Linux instance by using different authentication methods:

-   If you are using an SSH key pair, see [connect to a Linux instance by using an SSH key pair](reseller.en-US/User Guide/Connect to instances/Connect to a Linux instance by using an SSH key pair.md).
-   If you are using a password, you can [connect to an instance by using the Management Terminal](reseller.en-US/User Guide/Connect to instances/Connect to an instance by using the Management Terminal.md) or by using software applications or command lines.

## Prerequisites {#section_tyv_dwx_wdb .section}

-   The instance must be in the **Running** status. If not, [start it](reseller.en-US/User Guide/Instances/Start or stop an instance.md#).
-   You have set a logon password for the instance. If the password is lost, you can [reset the password](reseller.en-US/User Guide/Instances/Reset an instance password.md#).
-   The instance can access the Internet:
    -   In a VPC, a public IP address is assigned to the instance or [an EIP address is bound to the instance](../../../../reseller.en-US/Quick Start/Create a VPC.md#section_ux1_cmw_rdb).
    -   In the classic network, a public IP address is assigned to the instance by using either of the following methods:
        -   For a Subscription or a Pay-As-You-Go instance, you can select **Assign public IP** when creating the instance.
        -   For a Subscription instance without a public IP address, you can assign one by [upgrading the bandwidth](reseller.en-US/User Guide/Instances/Change configurations/Overview of configuration changes.md#).
-   The following security group rules must be added to the security group that the instance joins. For more information, see [add security group rules](reseller.en-US/User Guide/Security groups/Add security group rules.md#).

    |Network type|NIC|Rule direction|Authorization policy|Protocol type|Port range|Authorization type|Authorization object |Priority|
    |------------|---|--------------|--------------------|-------------|----------|------------------|---------------------|--------|
    |VPC|N/A|Inbound|Allow|SSH \(22\)|22/22|Address Field Access|0.0.0.0/0|1|
    |Classic|Internet|


## Procedure {#section_czv_dwx_wdb .section}

Based on the operating system of your local machine, use one of the following methods to connect to a Linux instance by using the SSH protocol:

-   [Windows OS](#)
-   [Linux or Mac OS X](#)
-   [Android or iOS](#)

## Windows OS {#section_izn_vbg_qfb .section}

If your local machine is running Windows OS, you can use a remote connection tool, such as PuTTY, to connect to a Linux instance. In this article, we use PuTTY as an example to describe how to connect to a Linux instance by using the password authentication method. Before you start, download [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/).

Follow these steps to connect to a Linux instance:

1.  Start putty.exe.
2.  In the left-side navigation pane, click Session, and configure the following parameters:
    -   Host Name: Type the public IP address or EIP address of the instance.
    -   Port: Type 22.
    -   Connection Type: Select SSH.
    -   \(Optional\) Saved Session: If you do not want to repeat the configurations during the next logon, add a name for the session, and click **Save**.

        ![](images/5249_en-US.gif)

3.  Click **Open** to connect, and in the PuTTY Security Alert dialog box, click **Yes**.

    **Note:** For the first connection to an ECS instance, you have the PuTTY Security Alert as follows, which means PuTTY cannot guarantee the instance is the one that you think it is, so it can only provide the public key fingerprint of the instance for you to decide to trust the instance or not. If you select **Yes**, the public key will be added to the PuTTY’s cache and you will not be alerted again during your next connection. If you select Yes but are alerted again, a [man-in-the-middle attack \(MITM\)](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) may occur. For more information, see [PuTTY User Manual](https://the.earth.li/~sgtatham/putty/0.70/htmldoc/Chapter2.html#gs-hostkey).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9621/15432164125251_en-US.png)

4.  Enter the user name and password for the Linux instance, and then press **Enter**.

    **Note:** The password is not displayed on screen.


If you are successfully connected to the instance, the following message is displayed.

```
Welcome to Alibaba Cloud Elastic Compute Service !
```

## Linux or Mac OS X {#section_rpv_vbg_qfb .section}

If your local machine is running Linux OS or Mac OS X, follow these steps:

1.  Run the command `ssh root@[Public IP address or EIP address of the instance]`.
2.  Type the password and then press **Enter**.

If you are successfully connected to the instance, the following message is displayed.

```
Welcome to Alibaba Cloud Elastic Compute Service !
```

## Android or iOS {#section_tqb_wbg_qfb .section}

If your local machine is running Android OS or iOS, see [connect to an instance on a mobile device](reseller.en-US/User Guide/Connect to instances/Connect to an instance on a mobile device.md#).

## Reference {#section_pzv_dwx_wdb .section}

You can run a script to install a graphical desktop on an instance running CentOS. For more information, see [automatic installation tool for Linux instance](https://partners-intl.aliyun.com/help/faq-detail/41181.htm).

