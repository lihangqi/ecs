# Troubleshooting {#ServerMigrationTroubleshooting .reference}

After you fix the error, run go2aliyun\_client of the Cloud Migration Tool again. The migration resumes from where it was suspended.

**Note:** 

-   If you are using the 1.3.0 or later version of Cloud Migration tool, after the migration job is finished for an on-premises server running Windows Server 2008 and later version of Windows Server, please wait for the automatic recovery of file system access permission at the first instance startup attempt. For more information, see *FAQ 19* [How can I check my system after migrating a Windows server](reseller.en-US/Migration Service/Cloud Migration tool for P2V and V2V/Cloud Migration tool FAQ.md#AfterWindows).
-   If you are using the 1.3.0 or earlier version of Cloud Migration tool, to avoid abnormal components and service failure, run the [Reset File Permission](http://ecs-image-p2vs-hd1.oss-cn-hangzhou.aliyuncs.com/tools/ResetFilePermissions.zip) tool to restore the file system permission of Windows Server 2008 and later operating system.

-   [Keyword “IllegalTimestamp” appears in the migration logs.](#)
-   [Keyword “UnKnownError” appears in the migration logs.](#)
-   [Keyword “OperationDenied” appears in the migration logs.](#)
-   [Keyword “InvalidAccountStatus.NotEnoughBalance” appears in the migration logs.](#)
-   [Keyword “Forbidden.RAM” appears in the migration logs.](#)
-   [Keyword “InvalidImageName.Duplicated” appears in the migration logs.](#)
-   [Keyword “InvalidAccountStatus.SnapshotServiceUnavailable” appears in the migration logs.](#)
-   [Keyword “Connect to Server Failed” appears in the migration logs.](#)
-   [Keyword “Do Rsync Disk x Failed” appears in the migration logs.](#)
-   [Winodws server migration stops at the "Prepare For Rsync Disk 0" stage.](#)
-   [What can I do if the Windows requires me to activate Microsoft license after the Windows server migration?](#)
-   [What can I do if the drive letters of data disks are missing or wrong after the Windows server migration?](#)
-   [Keyword “check rsync failed” or "rsync not found" appears in the migration logs of a Linux server.](#)
-   [Keyword “check virtio failed” appears in the migration logs of a Linux server.](#)
-   [Keyword “check selinux failed” appears in the migration logs of a Linux server.](#)
-   [Keyword “Do Grub Failed” appears in the migration logs of a Linux server.](#)
-   [Why no data is found in the original data disk directory in the started Linux ECS instances?](#)
-   [Why cannot I start the created ECS instances after Linux server migration?](#)
-   [What can I do if network service is abnormal when I start the migrated Others Linux instances?](#)

**Keyword "IllegalTimestamp" appears in the migration logs.** 

Check whether the system time is correct or not.

**Keyword "UnKnownError" appears in the migration logs.** 

Check whether the value of the `platform` parameter is correct in file user\_config.json.

**Keyword "OperationDenied" appears in the migration logs.** 

If `rsync: send_files failed to open "…": Permission denied (13)` is displayed in the log, Alibaba Cloud Migration Tool has no access permission on the directory or folder, which leads to rsync failure. In this case, you can configure rsync\_excludes\_linux.txt or Rsync/etc/rsync\_excludes\_win.txt to filter this directory or folder and try again.

**Keyword "InvalidAccountStatus.NotEnoughBalance" appears in the migration logs.** 

The default billing method of the intermediate instance is [Pay-As-You-Go](../reseller.en-US/Pricing/Pay-As-You-Go.md#). You must make sure that no credit limit is set to your credit card and it allows the payment to go through.

**Keyword "Forbidden.RAM" appears in the migration logs.** 

The RAM user is not granted with operation permission and cannot access the APIs.

If the AccessKey that you create belongs to a RAM user, you must make sure that the specified RAM user is authorized the permission of `AliyunECSFullAccess` and `AliyunVPCFullAccess` to operate the ECS and VPC resources. For more information, see [Implement access control by using RAM](../reseller.en-US/Security/Implement access control by using RAM.md#).

**Keyword "InvalidImageName.Duplicated" appears in the migration logs.** 

The specified parameter `image_name` cannot be the same as an existing image name.

 **Keyword "InvalidAccountStatus.SnapshotServiceUnavailable" appears in the migration logs.** 

It indicates that you have not signed up for the ECS snapshot services. You can go to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs) to sign up the ECS snapshot service and try cloud migration again.

**Keyword "Connect to Server Failed" appears in the migration logs.** 

It indicates that the tool is unable to connect the intermediate instance. Follow these steps:

1.  View the migration log for any migration exception.

2.  Before you proceed, check the following:

    -   Whether the status of the intermediate instance is abnormal or not in the ECS console.

    -   Whether the network service of the on-premises server is abnormal or not. The TCP port 80, 443, 8703, and 8080 have been enabled because the Cloud Migration Tool needs the access permission of those ports.

3.  After the error is fixed, run the go2aliyun\_client again.


**Keyword "Do Rsync Disk x Failed" appears in the migration logs.** 

It indicates that the data transmission is interrupted. Follow these steps:

1.  View the migration log for any migration exception. Specifically, if the **return: 3072** or **return: 7680** is displayed in the log file, you must make sure the database or container service in the on-premises server has been disabled, such as Oracle, MySQL, MS SQL Server, MongoDB, and Docker. In that case, you can disable the service or filter out the related directory before you start the migration again.

2.  Before you proceed, check the following:

    -   Whether the status of the intermediate instance is abnormal or not in the ECS console.

    -   Whether the network service of the on-premises server is abnormal or not. The TCP port 80, 443, 8703, and 8080 have been enabled because the Cloud Migration Tool needs the access permission of those ports.

3.  After the error is fixed, run the go2aliyun\_client again.


**Winodws server migration stops at the "Prepare For Rsync Disk 0" stage.** 

Winodws server migration stops at the "Prepare For Rsync Disk 0" stage, meanwhile, the log file record that "VssSnapshotul::VssSnapshotul GetSnapshotul Failed: 0x80042308". Follow these steps:

1.  To enable the Volume Shadow Copy Service, for example, in Windows Server 2016:

    1.  Log on to your on-premises server, and click **Start**, enter **Services** and select the gadget icon.
    2.  Locate the Volume Shadow Copy Service, and click **Start** the service.
2.  To uninstall the qemu guest agent software:

    1.  Log on to your on-premises server, and click **Start**, enter **Services** and select the gadget icon.
    2.  Check that whether the QEMU Guest Agent VSS Provider service is running or not. And if this service is not available, you can run the Cloud Migration tool directly.
    3.  Find the uninstall program, possibly in the C:\\Program Files \(x86\)\\virtio\\monitor\\uninstall.bat directory, execute the program to uninstall the QEMU Guest Agent.
3.  Run the Cloud Migration tool again.


**What can I do if the Windows requires me to activate Microsoft license after the Windows server migration?** 

You can activate Windows service via KMS after reinstalling Windows KMS Client Key.

-   Log on to the Windows instance.

-   On the Microsoft [Appendix A: KMS Client Setup Keys](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj612867(v%3dws.11)) page, find your relevant KMS Client Key, here, it is assumed to be xxxx-xxxx-xxxx-xxxx-xxxx.

-   Open the command-line tool with administrative permission, and run the following command:

    ``` {#codeblock_kqv_kyc_tlh}
    slmgr /upk
    slmgr /ipk xxxx-xxxx-xxxx-xxxx-xxxx
    ```


**What can I do if the drive letters of data disks are missing or wrong after the Windows server migration?** 

If the drive letters are missing, you can add the drive letters in the Disk Management.

1.  Choose **Control Panel** \> **System and Security** \> **Administrative Tools** \> **Computer Management**.

2.  Locate and right-click the target data disk in Disk Management module, and click **Change Drive Letters and Path...**.

3.  Click **Add** and specify a drive letter.


If the drive letter is in disorder, you can open the Disk Management and change it again.

1.  Select **Control Panel** \> **System and Security** \> **Administrative Tools** \> **Computer Management**.

2.  Locate and right-click the target data disk in Disk Management module, and click **Change Drive Letters and Path...**.

3.  Click **Change** and assign a drive letter.


**Keyword "check rsync failed" or "rsync not found" appears in the migration logs of a Linux server.** 

Check whether the rsync component is installed. For more information, see *Preparations* in [Migrate your server to Alibaba Cloud by using the Cloud Migration tool](reseller.en-US/Migration Service/Cloud Migration tool for P2V and V2V/Migrate your server to Alibaba Cloud by using the Cloud Migration tool.md#).

**The keyword "check virtio failed" appears in the migration logs.** 

Check whether the [virtio driver](../reseller.en-US/Images/Custom image/Import images/Install virtio driver.md#) is installed or not.

**The keyword "check selinux failed" appears in the migration logs.** 

Check whether SElinux is deactivated or not.

You can temporarily deactivate SELinux by running `setenforce 0`.

**Keyword "Do Grub Failed" appears in the migration logs of a Linux server.** 

Check whether the on-premises server has correctly installed the GRUB \(GRand Unified Bootloader\) or not when `Do Grub Failed` is received. You can [install a GRUB with the version newer than 1.9 and try again](https://partners-intl.aliyun.com/help/doc-detail/62807.html) and try again.

**Why no data is found in the original data disk directory in the started Linux ECS instances?** 

After you migrate an on-premises Linux server, the data disks are not mounted by default. You can run the command `ls /dev/vd*` to view the data disk devices. You may mount the data disks manually as needed, and edit configuration file `/etc/fstab` to configure the mounting file systems.

**Why cannot I start the created ECS instances after Linux server migration?** 

-   Check the driver. Before creating the I/O optimized instances, make sure that the [virtio driver](../reseller.en-US/Images/Custom image/Import images/Install virtio driver.md#) is installed on the on-premises server.

-   Check whether the boot configurations of the on-premises server are normal.

-   Connect to the ECS instance by using the [Management Terminal](../reseller.en-US/Instances/Connect to instances/Connect to Linux instances/Connect to an instance by using the Management Terminal.md#) in the ECS console, if the following output appears:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22638/155955512813375_en-US.png)

    Perhaps the kernel of your on-premises Linux servers is the earlier version, and the version of GRUB \(GRand Unified Bootloader\) is earlier than 1.9. You may [update the boot loader GRUB to a version later than 1.9](https://partners-intl.aliyun.com/help/doc-detail/62807.html).


**What can I do if network service is abnormal when I start the migrated Others Linux instances?** 

When an image of Others Linux type is imported, Alibaba Cloud performs no configuration, including network configuration and SSH configuration, on ECS instances created by custom images. You can manually modify the network service configurations.

After the migration job is finished, we provide the created instance a single virtual network interface that uses DHCP to assign addresses. If network configuration still fails, open a ticket to contact Alibaba Cloud.

If the problem persists, [join the dedicated DingTalk Migration Tool group chat](https://h5.dingtalk.com/invite-page/index.html?code=ca190154ff) or open a ticket to contact Alibaba Cloud.

