# Images {#concept_qql_3zb_wdb .concept}

An image is a running environment template for ECS instances. It generally includes an operating system and pre-installed software. An image works as a file copy that includes data from one or more disks. These disks can be a single system disk, or a combination of the system disk and data disks.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9572/15504717265238_en-US.png)

## Image overview {#section_nyg_r5w_ydb .section}

ECS provides a range of image types that you can use to easily access image resources.

|Image type|Type description|Technical support|
|:---------|:---------------|:----------------|
|Public image|Alibaba Cloud provides the following types of public images:-   **Aliyun Linux image**: The Aliyun Linux image is a custom, native operating system provided by Alibaba Cloud for ECS. The Aliyun Linux image has undergone stringent testing to guarantee its security, stability, and normal startup and operation.
-   **Third-party commercial image and open-source licensed image**: Such images include Windows Server, Ubuntu, CentOS, Red Hat Enterprise Linux, Debian, SUSE Linux, FreeBSD and CoreOS. These images have undergone stringent testing conducted by Alibaba Cloud to guarantee their security, stability, and normal startup and operation.

| -   **Aliyun Linux image**: Alibaba Cloud provides [technical support](https://workorder-intl.console.aliyun.com/#/ticket/createIndex).
-   **Third-party commercial image and open-source licensed image**: You can contact the OS vendors or open source communities for technical support. Additionally, Alibaba Cloud provides technical support to assist investigation into various image-related and system-related problems.

 |
|Custom image| Custom images include imported images, and custom images created from public images and Alibaba Cloud Marketplace images.

 | You can contact the OS vendors for technical support. Additionally, Alibaba Cloud provides technical support in problem investigation.

 |
|Marketplace image| [Marketplace](https://marketplace.alibabacloud.com/) images are licensed and provided by Independent Software Vendors \(ISVs\) and sold in Alibaba Cloud Marketplace. Such images have undergone stringent testing conducted by the respective ISVs and Alibaba Cloud to guarantee security.

 Marketplace images provide not only the OSs required for applications, but also the configuration environments. This eliminates complicated installation and configuration process and helps you deploy ECS in one click.

 | You can contact the image vendors for technical support.

 |

## Public images {#PublicImage .section}

Public images are fully licensed to provide a highly stable operating environment. You can customize your application environment based on a public image. Different instance types correspond to different available public images. For information about the built-in services of public images releases, go to the official website of the OS vendors.

Alibaba Cloud regularly releases and updates public images. For more information, see [Image release notes](../intl.en-US/User Guide/Images/Image release notes/Image release notes.md#). You can view available public images in the [Public image list in the ECS console](https://ecs.console.aliyun.com/#/image/region/cn-hangzhou/systemImageList). The following table lists the ECS public images.

|OS type|OS version|OS type|OS version|
|:------|:---------|:------|:---------|
|Windows Server| -   Windows Server 2008 Standard Edition SP2 32-bit
-   Windows Server 2008 R2 Enterprise Edition 64-bit
-   Windows Server 2008 R2 Enterprise Edition 64-bit
-   Windows Server 2012 R2 Datacenter 64-bit
-   Windows Server 2012 R2 Datacenter 64-bit
-   Windows Server 2016 R2 Datacenter 64-bit
-   Windows Server 2016 R2 Datacenter 64-bit
-   Windows Server Version 1809 Datacenter 64-bit
-   Windows Server Version 1809 Datacenter 64-bit

 |CentOS| -   CentOS 6.8 64-bit
-   CentOS 6.8 32-bit
-   CentOS 6.9 64-bit
-   CentOS 7.2 64-bit
-   CentOS 7.3 64-bit
-   CentOS 7.4 64-bit
-   CentOS 7.5 64-bit
-   CentOS 7.6 64-bit

 |
|SUSE Linux| -   SUSE Linux Enterprise Server 11 SP4 64-bit
-   SUSE Linux Enterprise Server 12 SP4 64-bit

 |Debian| -   Debian 8.9 64-bit
-   Debian 9.6 64-bit

 |
|Red Hat| -   Red Hat Enterprise Linux 7.5 64-bit
-   Red Hat Enterprise Linux 7.4 64-bit
-   Red Hat Enterprise Linux 6.9 64-bit

 |Ubuntu| -   Ubuntu 14.04 64-bit
-   Ubuntu 16.04 64-bit
-   Ubuntu 18.04 64-bit

 |
|FreeBSD|FreeBSD 11.1 64-bit|OpenSUSE|OpenSUSE 42.3 64-bit|
|Aliyun Linux|Aliyun Linux 17.1 64-bit|CoreOS|CoreOS 1745.7.0 64bit|

## Custom images {#section_ivt_wkq_dgb .section}

After you successfully create or import a custom image, the status of the image becomes Available. You can then use this image to create an instance, share the image with other Alibaba Cloud accounts, or copy the image to other Alibaba Cloud regions under your account. The following figure shows the typical usage of a custom image.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9572/155047172636980_en-US.png)

You can create a custom image by using the following methods:

-   [Create a custom image by using a snapshot](../intl.en-US/User Guide/Images/Create custom image/Create a custom image by using a snapshot.md#)
-   [Create a custom image by using an instance](../intl.en-US/User Guide/Images/Create custom image/Create a custom image by using an instance.md#)
-   [Import an on-premises custom image](../intl.en-US/User Guide/Images/Import images/Notes for importing images.md#)

    **Note:** A custom image must be imported in one of the following formats: VHD, qcow2, or RAW. If the custom image is in another format, it must be converted before it can run in ECS. For more information, see [Convert image file format](../intl.en-US/User Guide/Images/Import images/Convert image file format.md#).


After creating custom images, you can perform the following operations:

-   [Replace the OS of an instance](../intl.en-US/User Guide/Cloud disks/Replace the system disk (non-public image).md#)
-   [Copy your custom images from one region to another](../intl.en-US/User Guide/Images/Copy images.md#)
-   [Share your custom images with other Alibaba Cloud accounts](../intl.en-US/User Guide/Images/Share images.md#)
-   [Export your custom images to on-premises testing environments or private cloud environments](../intl.en-US/User Guide/Images/Export custom images.md#)
-   [Manage your custom images](../intl.en-US/User Guide/Images/Manage custom images.md#)

## Billing details {#section_uyg_r5w_ydb .section}

We recommend that you maintain a sufficient balance in the linked credit card or PayPal account to complete the payment or preauthorization. For more information, see [Pricing overview](../intl.en-US/Pricing/Pricing overview.md#).The ECS image billing details are as follows:

|Image type|Billing description|
|:---------|:------------------|
|Public image| Only Windows Server and Red Hat Enterprise Linux public images incur fees, which are included in the bill when an instance is created. Windows Sever public images or Red Hat Enterprise Linux public images are provided with certified licenses and authorized support from Microsoft or Red Hat, respectively.

-   Red Hat Enterprise Linux: Billing is related to the instance type.
-   Windows Server: Free of charge in Alibaba Cloud regions in Mainland China. For other countries and regions, the use of Windows Server public images incur fees.

 Other public images are available free of charge.

 |
|Custom image| -   If you [Create a custom image by using a snapshot](../intl.en-US/User Guide/Images/Create custom image/Create a custom image by using a snapshot.md#):
    -   If the image used by the system disk snapshot is from the Alibaba Cloud Marketplace, the bill may include fees for the image and fees for the snapshot capacity.
    -   If the image used by the system disk snapshot is not from the Alibaba Cloud Marketplace, the bill may include fees for the snapshot capacity.
-   If you [Create a custom image by using an instance](../intl.en-US/User Guide/Images/Create custom image/Create a custom image by using an instance.md#), and the image used by the instance is from the Alibaba Cloud Marketplace, the billing policies of the Alibaba Cloud Marketplace and the ISV apply.

 |
|Marketplace image|The billing policies of the ISVs apply.|
|Shared image|If a shared image comes from the Alibaba Cloud Marketplace, the billing policies of the ISV apply.|

## Related operations {#section_u2t_hvw_ydb .section}

**Console operations**

-   You can [Create an instance from a custom image](../intl.en-US/User Guide/Instances/Create an instance/Create an instance from a custom image.md#).
-   You can change the system disk of an ECS instance by using either of the following methods:
    -   [Replace the image of the system disk with a public image](../intl.en-US/User Guide/Cloud disks/Replace the system disk (public image).md#).
    -   [Replace the image of the system disk with a non-public image](../intl.en-US/User Guide/Cloud disks/Replace the system disk (non-public image).md#).
-   You can obtain a custom image by using the following methods:
    -   [Create a custom image by using a snapshot](../intl.en-US/User Guide/Images/Create custom image/Create a custom image by using a snapshot.md#).
    -   [Create a custom image by using an instance](../intl.en-US/User Guide/Images/Create custom image/Create a custom image by using an instance.md#).
    -   [Import an on-premises custom image](../intl.en-US/User Guide/Images/Import images/Notes for importing images.md#).
-   After creating custom images, you can perform the following operations:
    -   [Copy your custom images from one region to another](../intl.en-US/User Guide/Images/Copy images.md#).
    -   [Share your custom images with other Alibaba Cloud accounts](../intl.en-US/User Guide/Images/Share images.md#).
    -   [Export your custom images to on-premises testing environments or private cloud environments](../intl.en-US/User Guide/Images/Export custom images.md#).

**API operations**

For more information, see the [APIs for images](../intl.en-US/API Reference/API overview.md#section_image_t2h_vdb).

