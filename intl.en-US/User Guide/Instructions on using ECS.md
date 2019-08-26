# Instructions on using ECS {#concept_q1h_cyw_wdb .concept}

This article describes usage restrictions and recommendations of an ECS instance.

## **General instructions** {#section_mqk_ddx_wdb .section}

**Restrictions**

-   You are prohibited from using your instances for flow-through services. Any violations will lead to punishments including shutdown and lockout of instances, and termination of services.
-   You are prohibited from using instances for click farming, advertising, or fraudulent transactions.
-   Do not enable SELinux.
-   Do not uninstall relevant hardware drivers.
-   Do not arbitrarily modify the MAC address of the network adapter.

**Recommendations**

-   For an instance with more than 4 GiB RAM, we recommend that you use a 64-bit operating system as a 32-bit operating system only supports up to 4 GiB RAM. Currently, the following 64-bit operating systems are supported \(please refer to the instance purchase page for the latest details\):
    -   Aliyun Linux 64-bit
    -   CoreOS 64-bit
    -   CentOS 64-bit
    -   Debian 64-bit
    -   FreeBSD 64-bit
    -   OpenSUSE 64-bit
    -   SUSE Linux 64-bit
    -   Ubuntu 64-bit
    -   Windows 64-bit
-   Windows 32-bit supports vCPUs with up to 4 cores.
-   A minimum of 2 GiB RAM is required for building a website or deploying a Web environment on a Windows instance.
-   An instance type with 1 vCPU core and 1 GiB RAM cannot be used for MySQL service.
-   To guarantee service continuity and avoid service downtime, we recommend that you enable auto-start upon instance boot for relevant software. In the case of databases that are connected to service applications, auto-reconnect should be enabled for them.
-   For I/O-optimized instances, do not disable the aliyun-service process.
-   For Windows users, exercise caution when using the administrator or other accounts to perform actions involving capacity expansion, spanned volume, registry, system update, and other related actions, in order to avoid data corruption due to misoperations.
-   For Linux users, exercise caution when using the root or other accounts to perform actions involving fio, mkfs, fsck, capacity expansion, and other related actions, in order to avoid data corruption due to misoperations.
-   We do not recommend that you upgrade the kernel and the operating system. If you need to upgrade the kernel, see [How to avoid Linux instance startup failure after kernel upgrade](https://partners-intl.aliyun.com/help/faq-detail/59360.htm).

## Windows instructions {#section_ajc_kdx_wdb .section}

-   Do not kill the built-in shutdownmon.exe process. Otherwise, the server may take a longer time to restart.
-   Do not rename, delete, or disable the administrator account.
-   We do not recommend that you use the virtual memory if Basic Cloud Disks are used. For Ultra Cloud Disks or SSD Cloud Disks, you can use the virtual memory as needed.

## Linux instructions {#section_opn_ldx_wdb .section}

-   Do not modify the contents of the default /etc/issue file on Linux instances . Otherwise, if you create a custom image of the instance and then use it to create a new instance, the new instance cannot start properly because the operating system edition cannot be recognized.
-   Do no arbitrarily modify permissions of the directories in the root partition, especially `/etc`, `/sbin`, `/bin`, `/boot`, `/dev`, `/usr`, and `/lib`. Improper modification of permissions may cause errors.
-   Do not rename, delete, or disable the Linux root account.
-   Do not compile or perform any arbitrary operations on the Linux kernel.
-   We recommend you do not use the swap partition if Basic Cloud Disks are used. For Ultra Cloud Disks or SSD Cloud Disks, you can use the swap partition as needed.
-   Do not enable the NetWorkManager service. This service conflicts with the internal network service of the system which can result in network errors.

For more information, see [Limitations](reseller.en-US/User Guide/Limitations.md#).

