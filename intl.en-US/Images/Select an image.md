# Select an image {#concept_h44_kwj_dhb .concept}

This topic describes how to select an appropriate image for your instance.

We recommend that you take the following items into consideration when selecting an image for your instance:

-   Region
-   Image type and billing method
-   Operating system
-   Built-in software \(such as MySQL and other applications\)

## Region {#section_okd_bqv_hhb .section}

Images are regional resources. An image that is used to create instances must belong to the same region as the instances. For example, if you create an instance in China \(Beijing\), you can use images only in China \(Beijing\). For more information, see [Regions and zones](../../../../reseller.en-US/General Reference/Regions and zones.md#).

To create an instance by using an image located in a different region, you must first copy the image to the current region. For more information, see [Copy images](Copy imagesEN-US_TP_9699.dita#concept_a3m_5dm_xdb).

## Image types and billing methods {#section_9op_qir_5qk .section}

ECS images are classified into public images, custom images, shared images, and Marketplace images, according to the image source. For information about image types and billing methods, see [Image overview](reseller.en-US/Images/Image overview.md#section_nyg_r5w_ydb).

## Operating system {#section_x1t_f35_hhb .section}

You must select an operating system \(OS\) during instance creation.

-   **OS architecture**

    You can select a 32-bit or 64-bit OS architecture for your instance.

    -   32-bit OS architecture supports a maximum of 4 GiB memory. Additionally, a 32-bit Windows OS supports a maximum of four CPU cores.
    -   64-bit OS architecture supports at least 4 GiB memory and larger.
-   **OS type \(Windows or Linux/Unix-like OS\)**

    |OS type|Logon mode|Feature|Scenario|
    |:------|:---------|:------|:-------|
    |Windows|Remote Desktop Connection|A Windows public image is installed with a genuine activated system.|     -   Supporting programs developed based on Windows, such as .NET
    -   Supporting SQL Server and other databases \(you need to manually install a database first.\)
 |
    |Linux/Unix-like|SSH|A common server-side open-source operating system that features high security and stability, fast deployment, and easy source code compilation.|     -   Generally used for server applications such as high-performance web servers
    -   Supporting common programming languages ​​such as PHP and Python
    -   Supporting MySQL and other databases \(you need to manually install a database first.\)
 |

    Alibaba Cloud provides a list of public images that run Windows or Linux/Unix-like OS. For more information, see [Overview of public images](reseller.en-US/Images/Public image/Public image overview.md#).

-   **Considerations for Windows**

    The following information is provided for your consideration if you select to run Windows on your instance. Generally, we recommend that you use a later version of Windows for ease of use and better security.

    -   Instance types with one vCPU core and 1 GiB memory cannot start the MySQL database.
    -   We recommend that your target instances have at least 2 GiB memory or larger if you want to host one or more websites, deploy web environments, or use Windows Server 2008, Windows Server 2012, Windows Server 2016, or Windows Server 2019. Otherwise, the selected image may not be displayed on the purchase page, instance performance may be degraded, or both.
    -   Alibaba Cloud no longer provides technical support for Windows Server 2003 system images.
-   **Considerations for Linux and Unix-like OSs**

    The following information is provided for your consideration if you run a Linux or Unix-like operating system on your instance, and includes detailed information about the supported image versions.

    -   **Aliyun Linux** 

        Aliyun Linux is an operating system developed by Alibaba Cloud that provides a safer, more stable, and high-performance running environment for applications on ECS instances. Aliyun Linux 2 supports various cloud scenarios and instance types \(except for instances in a classic network and non-I/O-optimized instances\). For more information, see [Aliyun Linux 2](reseller.en-US/Images/Public image/Aliyun Linux 2.md#).

    -   **Red Hat series** 

        -   CentOS
        -   Red Hat
        The following table compares CentOS with Red Hat.

        |OS|Software package format|Package manager|Billing method|Feature|Relationship|
        |:-|-----------------------|---------------|:-------------|:------|:-----------|
        |CentOS|.rpm|yum|Free usage|         -   Stable, but lower patch update speed than Red Hat
        -   Supporting online instant upgrades
 |         -   CentOS is an open-source version of Red Hat.
        -   They can use the same RPM package and commands.
 |
        |Red Hat|Paid usage|Stable with enterprise-level technical support|

    -   **Debian series** 

        -   Debian
        -   Ubuntu
        The following table compares Debian with Ubuntu.

        |OS|Software package format|Package manager|Feature|Relationship|
        |:-|-----------------------|---------------|:------|:-----------|
        |Debian|.deb|aptitude|Stable|Ubuntu builds on the Debian architecture and infrastructure.|
        |Ubuntu|apt-get|         -   User-friendly system configuration
        -   Timely software updates
        -   Easy to use
 |

    -   **SUSE** 

        -   SUSE Linux
        -   openSUSE
        The following table compares SUSE Linux with openSUSE.

        |OS|Feature|Relationship|
        |--|-------|------------|
        |openSUSE|         -   openSUSE is the community version of SUSE Linux. It features advanced software versions, better extensibility \(desktop and server installation are supported\), and free updates \(you can also purchase official technical support\).
        -   SUSE Linux Enterprise is the enterprise version of SUSE Linux. It is more mature and stable, but its official release contains fewer software features than openSUSE.
        -   SUSE Linux Enterprise offers better work and production environments, whereas openSUSE delivers a superior entertainment experience and professional services.
 |         -   As of version 10.2, SUSE Linux was officially renamed openSUSE.
        -   openSUSE uses the same kernel as SUSE Linux.
 |
        |SUSE Linux|

    -   **CoreOS** 

        CoreOS is an open-source lightweight operating system based on the Linux kernel and designed to provide infrastructure for clustered deployments. It focuses on automation, ease of application deployment, security, reliability, and scalability. CoreOS provides the underlying functionality required for deploying applications inside software containers, together with a set of built-in tools for service discovery and configuration sharing.

    -   **FreeBSD** 

        FreeBSD is a Unix-like operating system for a variety of platforms which focuses on features, speed, and stability. FreeBSD offers advanced networking, performance, security and compatibility features today which are still missing in other operating systems, even some of the best commercial ones. For more information, see [FreeBSD official documentation](https://www.freebsd.org/about.html).


## Built-in software {#section_0r4_eja_g94 .section}

Alibaba Cloud Marketplace images are typically provided pre-installed with a running environment and software applications that you can apply to target ECS instances as needed. For more information, see [Marketplace images](reseller.en-US/Images/Marketplace images.md#).

## What to do next {#section_jv8_z0k_out .section}

-   Use a target image to create instances. For more information, see [Create an instance by using the wizard](../../../../reseller.en-US/Instances/Create an instance/Create an instance by using the wizard.md#).
-   Use a target image to change the operating system of a current image. For more information, see [Change the operating system](reseller.en-US/Images/Change the operating system.md#).

