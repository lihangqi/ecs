# Cloud Migration tool for P2V and V2V {#ServerMigrationCenter .concept}

Cloud Migration tool balances the workloads between your local and cloud hosts, or cloud hosts from different cloud platforms. Being lightweight and agile, Cloud Migration tool can live convert your physical desktops and servers or migrate virtual machines and cloud hosts to ECS.

Specifically, our Cloud Migration tool is designed for P2V \(Physical to virtual\) or V2V \(Virtual to virtual\) use cases. P2V indicates building virtualization environments for your physical desktops or servers in ECS, while V2V indicates migrating VMs \(virtual machines\) or cloud hosts to ECS. Resources such as operating system, applications, and application data in physical machines, VMs, or cloud hosts will be live clone to ECS images by using the Cloud Migration tool. You can use the ECS images to start a specified numbers of ECS instances afterwards.

## Applicable operating systems {#section_x3j_v5z_jfb .section}

Cloud Migration tool supports the following 32 or 64-bit physical machines, VMs, or cloud hosts:

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

Before migrating an operating system that is not listed previously, you must see topic [Migrate to Alibaba Cloud by using Cloud Migration tool](intl.en-US/Best Practices/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#) thoroughly and exercise with caution.

## Billing details {#section_bjj_v5z_jfb .section}

Cloud Migration tool is free of charge. However, you may be charged for the following resource consumption:

-   During the migration, an ECS instance is created by default under your Alibaba Cloud account to act as an intermediate station. Billing method of the intermediate ECS instance is Pay-As-You-Go. In case you have put a limit on your credit card, you must delimit your credit card before the payment is attempted..

    **Note:** If the P2V migration fails, the instance is retained on your ECS console for next migration attempt. If the migration fails, the intermediate instance is retained in ECS for the next migration attempt. You can log on to the ECS console and manually [release the instance](../../../../intl.en-US/User Guide/Instances/Release an instance.md#) to avoid unnecessary charges.


## References {#section_htg_nvz_jfb .section}

-   Alternatively, Cloud Migration tool can be used for cloud disk size shrinkage. For more information, see [Shrink disk](intl.en-US/Best Practices/Shrink disk.md#).

-   Except for Cloud Migration tool, you can also [import custom images](../../../../intl.en-US/User Guide/Images/Import images/Notes for importing images.md#) to ECS for server migration.

-   For on-premises databases to cloud migration, see [Data migration](https://www.alibabacloud.com/help/doc-detail/26594.htm).


## Update history {#section_fjj_v5z_jfb .section}

The following table shows the updated information about Cloud Migration tool:

|Date and time|Version|Description|
|:------------|:------|:----------|
|November 12, 2018|1.3.1| -   Uses SSH cryptographic protocol during data transmission, and supports dynamic SSH security token for authentication.
-   Optimizes the transmission performance for Windows operating system server.
-   Improves the support quality of Amazon Linux, Oracle Linux, and SLES operating system server.
-   Fixes several known issues.

 |
|August 29, 2018|1.3.0| -   Boosts the migration speed and fixes several bugs.
-   Implements automatic restoration for file system permission on Windows server after migration, without manual operation.

 |
|July 4, 2018|1.2.9.5| -   Supports Ubuntu 17 server.
-   Upgrades the server configuration of the Cloud Migration tool and fixes several bugs.

 |
|June 11, 2018|1.2.9| -   Publishes easy-to-use GUI wizards for Windows tool.
-   Restores the default filter option for some Windows data disk files and directories that are cannot be found.

 |
|April 28, 2018|1.2.8| -   Provides more command line parameter options. For more information, run --help within the tool.
-   Supports dedicated line for Virtual Private Cloud \(VPC\) migration.

 |
|April 3, 2018|1.2.6| -   Verifies whether the source path of a data disk is the subdirectory of another data disk or not.
-   Provides more options to transfer files.

 |
|March 8, 2018|1.2.3| -   Shortens the time of the first startup attempt for Linux instance.
-   Rectifies the insufficient disk space prompts at the instance startup.
-   Supports Ubuntu 10 server.

 |
|February 8, 2018|1.2.1| -   Simplifies the user interaction during the migration process.
-   Capable of disabling the SELinux feature of a Linux on-premises server temporarily.

 |
|January 18, 2018|1.2.0| -   Extends the range of data resource to be migrated, and more types of resource can be migrated.
-   Enhances the efficiency and stability of image creation.

 |
|January 11, 2018|1.1.8| -   Supports SUSE 12 SP2 server.
-   Boosts the connection speed.
-   Optimizes the layout of the migration logs.
-   Fixes the possible network issue of the NetworkManager.

 |
|December 21, 2017|1.1.7| -   Supports SUSE 12 SP1 server.
-   Capable of specifying the maximum bandwidth of data transmission.

 |
|December 14, 2017|1.1.6| -   Scans the latest release of Cloud Migration tool.
-   Fixes the 6144 error of data transmission.
-   Proofreads the request parameter specified in the user\_config.json configuration file.

 |
|December 8, 2017|1.1.5| -   Fixes the issue of Linux data disk directory.
-   Highlights the error message in the migration logs.

 |
|December 1, 2017|1.1.3|Supports Debian server.|

