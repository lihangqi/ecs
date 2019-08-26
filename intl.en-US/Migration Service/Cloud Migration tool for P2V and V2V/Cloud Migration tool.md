# Cloud Migration tool {#ServerMigrationCenter .concept}

The Cloud Migration tool provided by Alibaba Cloud allows you to migrate physical servers, Virtual Machines \(VMs\), and hosts on third-party cloud platforms \(collectively referred to in this topic and other topics of the Cloud Migration tool as source servers\) to Alibaba Cloud ECS to implement unified resource deployment and hybrid cloud computing architecture. The Cloud Migration tool applies to such migration scenarios as P2V \(migrating physical on-premises data centers to ECS\) and V2V \(migrating VMs or cloud hosts to ECS\).

## Migration workflow {#section_pq2_4s5_vfb .section}

After you download the Cloud Migration tool to your source server, the Cloud Migration tool can be used to create snapshots for the operating system, applications, and application data in the disk partitions of the source server according to your configuration file. Then, the Cloud Migration tool synchronizes data and generates a custom image at the ECS side. You can use the custom image to quickly create an ECS instance. The following figure shows the workflow of migrating your source server by using the Cloud Migration tool.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9832/156108400532321_en-US.png)

## Applicable operating systems {#section_x3j_v5z_jfb .section}

The Cloud Migration tool supports physical servers, VMs, or cloud hosts that are installed with the following 32-bit or 64-bit operating systems.

|Windows|Linux|
|:------|:----|
| -   Windows Server 2003
-   Windows Server 2008
-   Windows Server 2012
-   Windows Server 2016

 | -   Amazon Linux 2014 or later
-   CentOS 5/6/7
-   Debian 7/8/9
-   Gentoo 13.0
-   OpenSUSE 13.1
-   Oracle Linux 5/6/7
-   Red Hat 5/6/7
-   SUSE 11.4/12.1/12.2
-   Ubuntu 10/12/14/16/17

 |

If your operating system is not listed in the preceding table, we recommend that you see [Migrate your server to Alibaba Cloud by using the Cloud Migration tool](reseller.en-US/Migration Service/Cloud Migration tool for P2V and V2V/Migrate your server to Alibaba Cloud by using the Cloud Migration tool.md#) to learn more.

## Billing details {#section_bjj_v5z_jfb .section}

The Cloud Migration tool is provided free of charge. However, you may be charged for using the following resources:

-   An ECS instance that is automatically created under your Alibaba Cloud account as an intermediate instance during a cloud migration. This instance is named INSTANCE\_FOR\_GOTOALIYUN for migration tools of v1.5.0 and lower, and No\_Delete\_GotoAliyun\_Transition\_Instance for migration tools of v1.5.0 and higher. This intermediate instance is billed by the Pay-As-You-Go billing method. Therefore, you must make sure your Alibaba Cloud account has a sufficient balance for this migration. For more information about the Pay-As-You-Go billing method, see [Pay-As-You-Go](../reseller.en-US/Pricing/Pay-As-You-Go.md#).
-   Cloud disks that are automatically created under your Alibaba Cloud account as intermediate disks during a cloud migration. These disks are attached to your intermediate instance for data transfer.

**Note:** Even if the cloud migration fails, the instance is still retained in the ECS console. If you no longer require the instance, you can log on to the ECS console and [release the instance](../reseller.en-US/Instances/Manage instances/Release an instance.md#) to avoid incurring unnecessary charges.

## References {#section_htg_nvz_jfb .section}

-   The Cloud Migration tool can also be used to shrink your cloud disk volume. For more information, see [Shrink disk volume](reseller.en-US/Best Practices/Shrink disk volume.md#).
-   You can also [import images](../reseller.en-US/Images/Custom image/Import images/Notes for importing images.md#) to ECS to implement P2V or V2V server migration.
-   If you need to migrate databases to Alibaba Cloud, see [Data migration](https://partners-intl.aliyun.com/help/doc-detail/26594.htm).

## Update history {#section_fjj_v5z_jfb .section}

The following table describes the update history of the Cloud Migration tool. You can download the [latest version](http://p2v-tools.oss-cn-hangzhou.aliyuncs.com/Alibaba_Cloud_Migration_Tool.zip).

|Date|Version|Description|
|:---|:------|:----------|
|2019-05-17|1.5.1.5| -   Added the automatic scale-out function for intermediate disks.
-   Optimized the Windows restoration check function.
-   Added the `--verbose` option for displaying detailed progress of cloud migration.
-   Fixed other known bugs.

 |
|2019-05-05|1.5.1.3| -   Added the zoom out button to the Windows GUI of the Cloud Migration tool.
-   Optimized the Windows restoration check function.
-   Fixed Windows VSS error 0x80042308.
-   Optimized the Linux GRUB retry logic.
-   Added End-User License Agreement \(EULA\).
-   Fixed other known bugs.

 |
|2019-04-02|1.5.1| -   Optimized data transfer performance.
-   Optimized the GRUB configuration logic.
-   Optimized support for the SUSE/SLES OS.

 |
|2019-03-14|1.5.0.5| -   Provided the Chinese interface for [Windows GUI](reseller.en-US/Migration Service/Cloud Migration tool for P2V and V2V/GUI of Cloud Migration tool (Windows).md#).
-   Added support for proxy during [cloud migration through VPC intranet](reseller.en-US/Migration Service/Cloud Migration tool for P2V and V2V/Cloud migration through VPC intranet.md#).

 |
|2019-03-09|1.5.0| -   Unified the names and descriptions for intermediate resources \(instances, disks, and snapshots\).
-   Added support for automatic recovery upon errors, for example recovery of an intermediate instance that is deleted accidentally.
-   Added support for the [Elastic IP Address \(EIP\)](../../../../../reseller.en-US/Product Introduction/What are Elastic IP Addresses.md#) for the intermediate instance.
-   Added support for the EFI boot mode for Linux.
-   Optimized migration logs and prompt messages.
-   Optimized operations related to initialization of the intermediate instance and the configuration of GRUB.
-   Optimized the configuration file structure, and removed the Architecture parameter.

 |
|2019-02-02|1.3.2.5| -   Optimized HTTP access timeout settings.
-   Optimized the Windows restoration check function.
-   Optimized the migration progress display.
-   Fixed the issue that causes failure in checking the name of error-format images.

 |
|2019-01-23|1.3.2.3| -   Optimized HTTP access timeout settings.
-   Optimized the Windows restoration check function.
-   Added support for migration of large Windows data disks.

 |
|2019-01-11|1.3.2| -   Fixed incompatible cloud-init configurations.
-   Added support for automatic mount of Linux data disks.
-   Added support for migration of large Linux data disks.
-   Optimized support for the SUSE/SLES OS.

 |
|2018-11-12|1.3.1| -   Added support for transferring data through SSH and for dynamic SSH security token authentication.
-   Optimized the transfer performance for Windows.
-   Optimized support for Amazon Linux, Oracle Linux, and SLES OSs.
-   Fixed several bugs.

 |
|2018-08-29|1.3.0| -   Increased the migration speed and fixed several bugs.
-   Added automatic restoration for Windows servers, eliminating the need to manually run the file permission resetting tool.

 |
|2018-07-04|1.2.9.5| -   Added support for migration of Ubuntu 17 servers.
-   Optimized the client functions of the Cloud Migration tool and fixed several bugs.

 |
|2018-07-11|1.2.9| -   Added a simplified Wizard GUI for the Cloud Migration tool in Windows.
-   Restored the default filter option for some Windows data disk files and directories that cannot be found.

 |
|2018-04-28|1.2.8| -   Added command line parameter options, which can be queried by running the --help command in the directory where the Cloud Migration tool is located.
-   Added support for migrations from a leased-line VPC to Alibaba Cloud.

 |
|2018-04-03|1.2.6| -   Fixed the bug in which the parent directory of a Linux server data disk copied data from subdirectories repeatedly.
-   Added file transfer parameters.

 |
|2018-03-07|1.2.3| -   Shortened the first startup attempt for Linux instances.
-   Rectified the repeated disk space insufficiency prompt that occurred at every instance startup. Now the prompt displays only when disk space is determined to be insufficient.
-   Added support for Ubuntu 10 server.

 |
|2018-02-08|1.2.1| -   Simplified user interactions during the migration process.
-   Added support for temporarily disabling the SELinux feature of a Linux on-premises server.

 |
|2018-01-18|1.2.0| -   Added support for migration of more resources.
-   Enhanced the efficiency and stability of image creation.

 |
|2018-01-11|1.1.8| -   Added support for the SUSE 12 SP2 server.
-   Increased the connection speed.
-   Optimized the layout of migration logs.
-   Fixed the bug related to NetworkManager.

 |
|2017-12-21|1.1.7| -   Added support for the SUSE 12 SP1 server.
-   Added support for limiting the maximum data transfer bandwidth.

 |
|2017-12-14|1.1.6| -   Added support to scan for the latest release of the Cloud Migration tool.
-   Fixed error 6144 in data transfer.
-   Added support for proofreading the request parameters specified in the user\_config.json configuration file.

 |
|2017-12-08|1.1.5| -   Fixed the bug of Linux data disk directory.
-   Highlighted error messages in the migration logs.

 |
|2017-12-01|1.1.3|Added support for the Debian server.|

