# ECS operation instructions {#concept_q1h_cyw_wdb .concept}

To guarantee proper operation of your ECS instance, you must take the considerations outlined in this section into account before use.

**Prohibitions**

-   Alibaba Cloud prohibits you from using your instance for flow-through services.  Any violation results in punishment up to shutdown and lockout of instance, and termination of services.
-   Alibaba Cloud prohibits you from using your instance for click farming, advertising, or fictitious transactions.
-   Alibaba Cloud prohibits you from activating SELinux.
-   Alibaba Cloud prohibits you from uninstalling hardware related drivers.
-   Alibaba Cloud prohibits you from arbitrarily modifying the MAC address of the network adapter.

**Suggestions**

-   For an ECS with more than 4 GiB RAM, we recommend that you use a 64-bit OS, because a 32-bit OS supports a maximum of 4 GiB RAM. Currently available 64-bit systems include:
    -   Aliyun Linux
    -   CoreOS
    -   CentOS
    -   Debian
    -   FreeBSD
    -   OpenSUSE
    -   SUSE Linux
    -   Ubuntu
    -   Windows
-   32-bit Windows OS supports CPUs with up to 4 cores.
-   A minimum of 2 GiB RAM is needed for buiding a website on a Windows instance, and an instance type with 1 vCPU core and 1 GiB RAM cannot be used for MySQL service.
-   To guarantee service continuity and avoid service downtime, you must enable auto-start of service applications upon OS boot.
-   For I/O-optimized instances, do not stop the aliyun-service process.
-   We do not recommmend that you update the kernel and the OS. For more information, see [How to avoid Linux instance startup failure after kernel upgrade](https://www.alibabacloud.com/help/faq-detail/59360.htm).

## Windows restrictions {#section_ajc_kdx_wdb .section}

-   Do not close the built-in shutdownmon.exe process, which may delay the restart of your Windows server.
-   Do not rename, delete, or disable the Administrator account.
-   We do not recommend that you use virtual memory.

## Linux restrictions {#section_opn_ldx_wdb .section}

-   Do not modify the content of the default /etc/issue file. Otherwise, if you create a custom image of the ECS instance and create a new ECS instance based on the image, the new instance cannot start because the operating system edition cannot be recognized.
-   Proceed with caution when modifying permissions of the directories in the root partition, such as `/etc`, `/sbin`, `/bin`, `/boot`, `/dev`, `/usr` and `/lib`. Improper modification of permissions may cause errors. Such modifications may cause system errors.
-   Do not rename, delete, or disable the Linux root account.
-   Do not compile or perform any other operations on the Linux kernel.
-   We do not recommend that you use swap partition.
-   Do not enable the NetWorkManager service. This service conflicts with the internal network service of the system and causes network errors.

For more information, see [Limits](intl.en-US/User Guide/Limits.md#).

