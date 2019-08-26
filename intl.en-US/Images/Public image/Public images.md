# Public images {#concept_x4k_22r_wgb .concept}

This topic describes the public images provided by Alibaba Cloud. Alibaba Cloud provides Aliyun Linux, a customized public image type that is natively supported by ECS, in addition to public images that are authorized by corresponding third-party vendors and have been tested by Alibaba Cloud to provide a secure and stable operating environment for applications in ECS instances. All users can create ECS instances using public images \(except for the Windows Server and Red Hat Enterprise Linux images\) for free.

## Types of public images {#section_rqn_bwj_dhb .section}

Alibaba Cloud provides two types of public images.

|Type|Description|Technical support|
|:---|:----------|:----------------|
|Aliyun Linux images|The Aliyun Linux images are custom, native operating systems provided by Alibaba Cloud for ECS. Each Aliyun Linux image has undergone stringent testing to guarantee its security, stability, and normal startup and operation.| Alibaba Cloud provides technical support. To access support, open a ticket.

 |
|Third-party and open source images|These images have undergone stringent testing conducted by Alibaba Cloud to guarantee their security, stability, and normal startup and operation. Such images include: -   Windows: Windows Server
-   Linux: Ubuntu, CentOS, Redhat Enterprise Linux, Debian, SUSE Linux, FreeBSD, and CoreOS

 |We recommend that you contact the corresponding OS vendors or open source communities for technical support. In addition, Alibaba Cloud provides technical support to assist with investigation into various image-related and system-related problems.|

## Aliyun Linux images {#section_vgz_pjb_fhb .section}

Aliyun Linux is a Linux public image independently developed by Alibaba Cloud. The following table describes the available versions of Aliyun Linux.

|Operating system|Version|Description|
|:---------------|:------|:----------|
|Aliyun Linux 2|Aliyun Linux 2.1903 64-bit| A next-generation OS that supports more Alibaba Cloud instance types \(including ECS Bare Metal Instances\) than the previous Aliyun Linux image. Aliyun Linux 2 is also equipped with Alibaba Cloud command line tools and other software packages by default.

 If you are replacing other Linux distributions with Aliyun Linux, we recommend that you switch to Aliyun Linux 2. If you are currently using the Aliyun Linux image, we recommend that you replace the current distribution with Aliyun Linux 2 by creating a new instance or replacing the system disk.

 For more information, see [Aliyun Linux 2](reseller.en-US/Images/Public image/Aliyun Linux 2.md#).

 |
|Aliyun Linux|Aliyun Linux 17.1 64-bit|A secure, stable, and high-performance Linux image that interoperates natively with Alibaba Cloud ECS. For more information, see [Aliyun Linux 17.1](reseller.en-US/.md#).|

## Third-party and open source images {#section_vcx_txj_dhb .section}

Alibaba Cloud regularly releases or updates the public images of third-party and open source vendors. For more information, see [Image release records](https://help.aliyun.com/document_detail/100410.html#concept-orn-h2x-dgb). You can also view all available public images on the [public images](https://ecs.console.aliyun.com/#image/region/cn-hangzhou/systemImageList) page in the corresponding region in the ECS console.

The following tables provide references regarding the current third-party and open source image versions provided by Alibaba Cloud \(Windows and Linux\).

-   Windows images

    |Operating system|Version|
    |:---------------|:------|
    |Windows Server 2019|     -   Windows Server 2019 data center 64-bit \(Chinese edition\)
    -   Windows Server 2019 data center 64-bit \(English edition\)
 |
    |Windows Server 2016|     -   Windows Server 2016 data center 64-bit \(Chinese edition\)
    -   Windows Server 2016 data center 64-bit \(English edition\)
 |
    |Windows Server 2012|     -   Windows Server 2012 R2 data center 64-bit \(Chinese edition\)
    -   Windows Server 2012 R2 data center 64-bit \(English edition\)
 |
    |Windows Server 2008|     -   Windows Server 2008 standard SP2 32-bit \(Chinese edition\)
    -   Windows Server 2008 R2 enterprise 64-bit \(Chinese edition\)
    -   Windows Server 2008 R2 enterprise 64-bit \(English edition\)
 **Note:** If you are using a 32-bit operating system, select an instance type with a memory capacity that does not exceed 4 GiB. For more information, see [Select an image](reseller.en-US/Images/Select an image.md#).

 |
    |Windows Server Version 1809|     -   Windows Server Version 1809 data center 64-bit \(Chinese edition\)
    -   Windows Server Version 1809 data center 64-bit \(English edition\)
 |

-   Linux images

    |Operating system|Version|
    |:---------------|:------|
    |CentOS|     -   CentOS 7.6 64-bit
    -   CentOS 7.5 64-bit
    -   CentOS 7.4 64-bit
    -   CentOS 7.3 64-bit
    -   CentOS 7.2 64-bit
    -   CentOS 6.10 64-bit
    -   CentOS 6.9 64-bit
    -   CentOS 6.8 32-bit
 **Note:** If you are using a 32-bit operating system, select an instance type with a memory capacity that does not exceed 4 GiB. For more information, see [Select an image](reseller.en-US/Images/Select an image.md#).

 |
    |CoreOS|     -   CoreOS 2023.4.0 64-bit
    -   CoreOS 1745.7.0 64-bit
 |
    |Debian|     -   Debian 9.8 64-bit
    -   Debian 9.6 64-bit
    -   Debian 8.11 64-bit
    -   Debian 8.9 64-bit
 |
    |FreeBSD|FreeBSD 11.1 64-bit|
    |OpenSUSE|OpenSUSE 42.3 64-bit|
    |Red Hat|     -   Red Hat Enterprise Linux 7.5 64-bit
    -   Red Hat Enterprise Linux 7.4 64-bit
    -   Red Hat Enterprise Linux 6.9 64-bit
 |
    |SUSE Linux|     -   SUSE Linux Enterprise Server 12 SP2 64-bit
    -   SUSE Linux Enterprise Server 11 SP4 64-bit
 |
    |Ubuntu|     -   Ubuntu 18.04 64-bit
    -   Ubuntu 16.04 64-bit
    -   Ubuntu 16.04 32-bit
    -   Ubuntu 14.04 64-bit
    -   Ubuntu 14.04 32-bit
 **Note:** If you are using a 32-bit operating system, select an instance type with a memory capacity that does not exceed 4 GiB. For more information, see [Select an image](reseller.en-US/Images/Select an image.md#).

 |


