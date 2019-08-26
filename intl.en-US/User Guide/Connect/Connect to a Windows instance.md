# Connect to a Windows instance {#concept_n31_wyx_wdb .concept}

If your Windows instance can access Internet, you can use remote connection tools to connect to it. Otherwise, you can [Terminal](intl.en-US/User Guide/Connect/Connect to an instance by using the Management Terminal.md#).

## Prerequisites {#section_hxc_qcy_wdb .section}

Before you start, complete the following:

-   The instance is in the **Running** status. If not, [Start or stop an instance](intl.en-US/User Guide/Instances/Start or stop an instance.md#).
-   You have set a logon password for the instance. If the password is lost, [Reset an instance password](intl.en-US/User Guide/Instances/Reset an instance password.md#).
-   The instance can access Internet:
    -   In a VPC, a public IP address is assigned to the instance or [an EIP address is bound to the instance](https://www.alibabacloud.com/help/doc-detail/27714.htm).
    -   In the classic network, a public IP address is assigned to the instance by using either of the following methods:
        -   For a Subscription or a Pay-As-You-Go instance, you can select Assign public IP when creating the instance.
        -   For a Subscription instance without public IP address, you can assign one by [upgrading bandwidth](intl.en-US/User Guide/Instances/Change configurations/Overview of configuration changes.md#).
-   The following security group rules must be added to the security group that the instance joins \(for more information, see [Add security group rules](intl.en-US/User Guide/Security groups/Add security group rules.md#)\).

    |Network Type|NIC|Rule Direction|Authorization Policy|Protocol Type|Port Range|Authorization Type|Authorization Object|Priority|
    |------------|---|--------------|--------------------|-------------|----------|------------------|--------------------|--------|
    |VPC|N/A|Inbound|Allow|RDP\(3389\)|3389/3389|Address Field Access|0.0.0.0/0|1|
    |Classic|Internet|


## Procedure {#section_b55_ycy_wdb .section}

Based on the operating system of your local machine, you have various options to connect to a Windows instance:

-   [Windows OS](#windows)
-   [Linux](#linux)
-   [Mac OS](#macOS1)
-   [Android or iOS](#mobile)

## Windows OS {#windows .section}

If the local machine is running Windows OS, you can use the mstsc to create a remote connection to a Windows instance.

1.  Use any one of the following methods to start **mstsc**:
    -   Select **Start** \> **icon \>** \> **Remote Desktop Connection**.
    -   Click the **Start** icon and search for mstsc.
    -   Press the shortcut key **Windows Logo** + **R** to open the Run windows, type mstsc, and then press the Enter key.
2.  In the Remote Desktop Connection dialog box, follow these steps:
    1.  Click the **Show Options** drop-down box.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/5258_en-US.png)

    2.  Type the public IP address or EIP address of the instance.
    3.  Type the user name. The default user name is Administrator

        **Note:** If you want to log on to the instance next time without repeating these steps, select **Allow me to save credentials**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/5259_en-US.png)

    4.  Optional. If you want to copy text or files from the local machine to the instance, click the **Local Resources** tab to see options for sharing local computer resources.
        -   If you want to copy text only, select **Clipboard**.
        -   If you also want to copy files, select **More** and select drive letters from which you want to copy files to your instance and click OK.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/5260_en-US.png)

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/5261_en-US.png)

    5.  Optional. Click the **Display** tab and resize the remote desktop window. Full Screen is recommended.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/5262_en-US.png)

    6.  Click **Connect**.

Now, you can operate on the instance.

## Linux {#linux .section}

If the local machine is running Linux OS, you can use a remote connection tool to create a remote connection to a Windows instance. This article takes rdesktop as an example to describe how to connect a Windows instance from a local machine running Linux.

1.  Download and start rdesktop.
2.  Run the command to connect to a Windows instance. Replace the parameter values with your own configurations.

    ```
    rdesktop -u administrator -p password -f -g 1024*720 192.168.1.1 -r clipboard:PRIMARYCLIPBOARD -r disk:sunray=/home/yz16184
    ```

    The parameter descriptions are as follows.

    |Parameters|Description|
    |:---------|:----------|
    |-u|The user name. The default user name for Windows instance is Administrator.|
    |-p|The password used to log on to the windows instance.|
    |-f|Full screen by default. Use **Ctrl**+**Alt**+**Enter** to switched the mode.|
    |-g|Resolution. Asterisks \(\*\) are used for separation. If omitted, full-screen display by default.|
    |192.168.1.1|The IP address of the server that requires remote connection. Replace it with the public IP or EIP address of your windows instance.|
    |-d|Domain name. For example, if the domain name is INC, then the parameter is `-d inc`.|
    |-r|Multimedia reorientation. For example:    -   Turn on the sound:-`-r sound`.
    -   Use a local sound card:-r sound: `-r sound : local`.
    -   Open the U Disk: `-r disk:usb=/mnt/usbdevice`.
|
    |-r clipboard:PRIMARYCLIPBOARD|Realizes direct word copying and pasting between Linux and Windows instances of local devices. Supports Chinese words copying and pasteing.|
    |-r disk:sunray=/home/yz16184|Specifies that a directory on Linux system of a local device maps to a hard disk on a Windows instance. In this way, you can no longer rely on Samba or FTP to transfer files.|


## Mac OS {#macOS1 .section}

To connect to a Windows instance from a local machine running Mac OS, see [Get started with Remote Desktop on Mac](https://docs.microsoft.com/zh-cn/windows-server/remote/remote-desktop-services/clients/remote-desktop-mac) in the Microsoft website.

## Android or iOS {#mobile .section}

If your local machine is running Android OS or iOS, you can use various apps to connect to a Linux instance. For more information, see [Connect to an instance on a mobile device](intl.en-US/User Guide/Connect/Connect to an instance on a mobile device.md#).

