# Connect to a Windows instance {#concept_n31_wyx_wdb .concept}

If your Windows instance can access the Internet, you can use remote connection tools to connect to it. Otherwise, you can use the [Management Terminal](reseller.en-US/User Guide/Connect to instances/Connect to an instance by using the Management Terminal.md#).

## Prerequisites {#section_hxc_qcy_wdb .section}

-   The instance is in the **Running** status. If not, [start it](reseller.en-US/User Guide/Instances/Start or stop an instance.md#).
-   You have set a logon password for the instance. If the password is lost, you can [reset the password](reseller.en-US/User Guide/Instances/Reset an instance password.md#).
-   The instance can access the Internet:
    -   In a VPC, a public IP address is assigned to the instance or [an EIP address is bound to the instance](../../../../reseller.en-US/Quick Start/Create a VPC.md#section_ux1_cmw_rdb).
    -   In the classic network, a public IP address is assigned to the instance by using either of the following methods:
        -   For a Subscription or a Pay-As-You-Go instance, you can select Assign public IP when creating the instance.
        -   For a Subscription instance without a public IP address, you can assign one by [upgrading bandwidth](reseller.en-US/User Guide/Instances/Change configurations/Overview of configuration changes.md#).
-   The following security group rules must be added to the security group that the instance joins. For more information, see [add security group rules](reseller.en-US/User Guide/Security groups/Add security group rules.md#).

    |Network Type|NIC|Rule Direction|Authorization Policy|Protocol Type|Port Range|Authorization Type|Authorization Object|Priority|
    |------------|---|--------------|--------------------|-------------|----------|------------------|--------------------|--------|
    |VPC|N/A|Inbound|Allow|RDP\(3389\)|3389/3389|Address Field Access|0.0.0.0/0|1|
    |Classic|Internet|


## Procedure {#section_b55_ycy_wdb .section}

Based on the operating system of your local machine, use one of the following methods to connect to a Windows instance:

-   [Windows OS](#)
-   [Linux](#)
-   [Mac OS](#)
-   [Android or iOS](#)

## Windows OS {#windows .section}

If the local machine is running Windows OS, you can use the mstsc to create a remote connection to a Windows instance.

1.  Use any one of the following methods to start **mstsc**:
    -   Select **Start** \> **icon** \> **Remote Desktop Connection**.
    -   Click the **Start** icon and search for mstsc.
    -   Press the **Windows key** + **R** to open the Run window, type mstsc, and then press **Enter**.
2.  In the Remote Desktop Connection dialog box, follow these steps:
    1.  Click the **Show Options** drop-down box.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/15432172095258_en-US.png)

    2.  Type the public IP address or EIP address of the instance.
    3.  Type the user name. The default user name is Administrator

        **Note:** If you want to log on to the instance next time using the same credentials, select **Allow me to save credentials**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/15432172095259_en-US.png)

    4.  Optional. If you want to copy text or files from the local machine to the instance, click the **Local Resources** tab to see options for sharing local computer resources.
        -   If you want to copy text only, select **Clipboard**.
        -   If you also want to copy files, select **More** and select the drive letters from which you want to copy files to your instance and click **OK**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/15432172095260_en-US.png)

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/15432172095261_en-US.png)

    5.  Optional. Click the **Display** tab to resize the remote desktop window. Full Screen is recommended.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/15432172095262_en-US.png)

    6.  Click **Connect**.

## Linux {#linux .section}

If the local machine is running Linux OS, you can use a remote connection tool to create a remote connection to a Windows instance. This article takes rdesktop as an example to describe how to connect a Windows instance from a local machine running Linux.

1.  Download and start rdesktop.
2.  Run the command to connect to a Windows instance. Replace the parameter values with your own configurations.

    ```
    rdesktop -u administrator -p password -f -g 1024*720 192.168.1.1 -r clipboard:PRIMARYCLIPBOARD -r disk:sunray=/home/yz16184
    ```

    The following table describes the parameters involved.

    |Parameters|Description|
    |:---------|:----------|
    |-u|The user name. The default user name for a Windows instance is Administrator.|
    |-p|The password used to log on to the windows instance.|
    |-f|Full screen by default. Use **Ctrl**+**Alt**+**Enter** to switched the mode.|
    |-g|Resolution. Asterisks \(\*\) are used for separation. If omitted, full-screen display is used by default.|
    |192.168.1.1|The IP address of the server that requires remote connection. Replace it with the public IP or EIP address of your Windows instance.|
    |-d|Domain name. For example, if the domain name is INC, then the parameter is `-d inc`.|
    |-r|Multimedia reorientation. For example:    -   Turn on the sound:-`-r sound`.
    -   Use a local sound card:-r sound: `-r sound : local`.
    -   Open the U Disk: `-r disk:usb=/mnt/usbdevice`.
|
    |-r clipboard:PRIMARYCLIPBOARD|Realizes direct word copying and pasting between Linux and Windows instances of local devices. Supports Chinese words copying and pasteing.|
    |-r disk:sunray=/home/yz16184|Specifies that a directory on the Linux system of a local device maps to a hard disk on a Windows instance. If this is configured, Samba and FTP are not recommended for file transfers.|


For more information about parameters of the `rdesktop` command, see [rdesktop documentation](https://github.com/rdesktop/rdesktop/blob/master/doc/rdesktop.1).

## Mac OS {#macOS1 .section}

To connect to a Windows instance from a local machine running Mac OS, see [get started with Remote Desktop on Mac](https://docs.microsoft.com/zh-cn/windows-server/remote/remote-desktop-services/clients/remote-desktop-mac).

## Android or iOS {#mobile .section}

If your local machine is running Android OS or iOS, see [connect to an instance on a mobile device](reseller.en-US/User Guide/Connect to instances/Connect to an instance on a mobile device.md#).

