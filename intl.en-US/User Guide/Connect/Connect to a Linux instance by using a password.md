# Connect to a Linux instance by using a password {#concept_rsl_2vx_wdb .concept}

You can connect to a Linux instance by using different authentication methods:

-   If you are using an SSH key pair, see [Connect to a Linux instance by using an SSH key pair](intl.en-US/User Guide/Connect/Connect to a Linux instance by using an SSH key pair.md#).
-   If you are using a password, you can connect to an instance [Step 3. Connect to an instance](../../../../intl.en-US/Quick Start for Entry-Level Users/Step 3. Connect to an instance.md#) or by using software applications or command lines.

## Prerequisites {#section_tyv_dwx_wdb .section}

Before you begin, make sure the following:

-   The instance must be in the **Running** status. If not, [Start or stop an instance](intl.en-US/User Guide/Instances/Start or stop an instance.md#).
-   You have set a logon password for the instance. If the password is lost, [Reset an instance password](intl.en-US/User Guide/Instances/Reset an instance password.md#).
-   The instance can access Internet:
    -   In a VPC, a public IP address is assigned to the instance or [an EIP address is bound to the instance](https://www.alibabacloud.com/help/doc-detail/27714.htm).
    -   In the classic network, a public IP address is assigned to the instance by using either of the following methods:
        -   For a Subscription or a Pay-As-You-Go instance, you can select Assign public IP when creating the instance.
        -   For a Subscription instance without public IP address, you can assign one by [Overview of configuration changes](intl.en-US/User Guide/Instances/Change configurations/Overview of configuration changes.md#) .
-   The following security group rules must be added to the security group that the instance joins. For more information, see [Add security group rules](intl.en-US/User Guide/Security groups/Add security group rules.md#).

    |Network type|NIC|Rule direction|Authorization policy|Protocol type|Port range|Authorization type|Authorization object |Priority|
    |------------|---|--------------|--------------------|-------------|----------|------------------|---------------------|--------|
    |VPC|N/A|Inbound|Allow|SSH \(22\)|22/22|Address Field Access|0.0.0.0/0|1|
    |Classic|Internet|


## Procedure {#section_czv_dwx_wdb .section}

Based on the operating system of your local machine, you have various options to connect to a Linux instance by using the SSH protocol:

-   [Windows OS](#windows)
-   [Linux or Mac OS X](#linux)
-   [Android or iOS](#mobile)

**Windows OS**

If your local machine is running Windows OS, you can use a remote connection tool, such as PuTTY, to connect to a Linux instance. In this article, we use PuTTY as an example to describe how to connect to a Linux instance by using the password authentication method. Before you start, download [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/).

Follow these steps to connect to a Linux instance:

1.  Start putty.exe.
2.  In the left-side navigation pane, click Session, and configure the following parameters:
    -   Host Name: Type the public IP address or EIP address of the instance.
    -   Port: Type 22.
    -   Connection Type: Select SSH.
    -   \(Optional\) Saved Session: If you do not want to repeat the configurations during the next logon, add a name for the session, and click **Save**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9621/5249_en-US.gif)

3.  Click **Open** to connect, and in the PuTTY Security Alert dialog box, click Yes.

    **Note:** For the first connection to an ECS instance, you have the PuTTY Security Alert as follows, which means PuTTY cannot guarantee the instance is the one that you think it is, so it can only provide the public key fingerprint of the instance for you to decide to trust the instance or not. If you select **Yes**, the public key will be added to the PuTTY’s cache and you will not be alerted again during your next connection. If you select Yes but are alerted again, a [man-in-the-middle attack \(MITM\)](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) may occur. For more information, see [PuTTY User Manual](https://the.earth.li/~sgtatham/putty/0.70/htmldoc/Chapter2.html#gs-hostkey).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9621/5251_en-US.png)

4.  As prompted, type the username and password for the Linux instance, and press the Enter key.

    **Note:** The password is not displayed on screen.


When you see the following message, you have successfully connected to an instance.

```
Welcome to Alibaba Cloud Elastic Compute Service !
```

Now, you can start working on your instance.

**Linux or Mac OS X**

If your local machine is running Linux OS or Mac OS X, follow these steps:

1.  Run the command `ssh root@[Public IP address or EIP address of the instance]`.
2.  Type the password and press the Enter key.

When you see the following message, you have successfully connected to an instance.

```
Welcome to Alibaba Cloud Elastic Compute Service !
```

Now, you can start working on your instance.

**Android or iOS**

If your local machine is running Android OS or iOS, you can use various apps to connect to a Linux instance. For more information, see [Connect to an instance on a mobile device](intl.en-US/User Guide/Connect/Connect to an instance on a mobile device.md#).

## Reference {#section_pzv_dwx_wdb .section}

You can run a script to install a graphical desktop on an instance running CentOS. For more information, see [Automatic installation tool for Linux instance](https://www.alibabacloud.com/help/faq-detail/41181.htm).

