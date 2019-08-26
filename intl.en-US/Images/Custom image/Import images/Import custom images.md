# Import custom images {#concept_w4x_4ms_xdb .concept}

This topic describes how to import on-premises image files to your ECS environment to create ECS instances or change system disks.

**Note:** When you import an image, a snapshot is automatically generated. You can view the snapshot information on the **Snapshots** page of the ECS Console. Before the import image task is completed, the status of the snapshot is displayed as **Failed**. When the task is completed, the status is automatically updated to **Successful**. The snapshot capacity is the size of the imported image file, regardless of the system disk size that was set when the image was imported.

## Prerequisites {#section_jn1_5ns_xdb .section}

-   You have understood the limitations of importing an on-premises image after reviewing the [notes for importing images](reseller.en-US/Images/Custom image/Import images/Notes for importing images.md#), [customize Linux images](customize Linux imagesEN-US_TP_9703.dita#concept_nt5_4km_xdb), and [convert image format](reseller.en-US/Images/Custom image/Import images/Convert image file format.md#).
-   You have [activated OSS](../../../../../reseller.en-US/Quick Start/Activate OSS.md#).
-   \(Optional\) If you are using a RAM user account, you have obtained the permission for the `AliyunECSImageImportDefaultRole` role from the master account.

## Procedure {#section_nc3_yns_xdb .section}

To import custom images in the ECS console, follow these steps:

1.  Use an OSS third-party client or OSS API to upload the prepared custom image. If the file you want to upload is larger than 5 GiB, see [Multipart upload and resumable upload](../../../../../reseller.en-US/Developer Guide/Upload files/Multipart upload and resumable upload.md#).
2.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
3.  In the left-side navigation pane, choose **Instances & Images** \> **Images**.
4.  In the top navigation bar, select a region.
5.  Click **Import Image**.
6.  In the Import Image dialog box, click **Confirm Address**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9706/15661819657027_en-US.png)

7.  In the Cloud Resource Access Authorization window, select `AliyunECSImageImportDefaultRole` and `AliyunECSExportDefaultRole`, then click **Confirm Authorization Policy** to allow the ECS service to access your OSS resources.
8.  Go back to the **Images** page and click **Import Image** again.
9.  In the Import Image dialog box, enter the following information:
    -   **Region of Image**: Select the region where the OSS Bucket of the image file to upload is located.
    -   **OSS Object Address**: Copy the object address of the image file from the OSS console. For more information, see [Download an object](../../../../../reseller.en-US/Console User Guide/Upload、download and manage objects/Download an object.md#).
    -   **Image Name**: Enter a name for the custom image. The name must be 2 to 128 characters in length and start with a letter. It can contain letters, numbers, periods \(.\), underscores \(\_\), colons \(:\), and hyphens \(-\).
    -   **Operating System**: Select **Windows** or **Linux** according to the operating system of your image. If you want to import a non-standard platform image, select **Linux**.
    -   **System Disk Size**: The system disk size, which ranges from 40 GiB to 500 GiB.
    -   **System Architecture**: Choose **x86\_64** for 64-bit operating systems and choose **i386** for 32-bit operating systems.
    -   **Platform**: The options depend on the **Operating System** you chose.
        -   Windows: Windows Server 2003, Windows Server 2008, and Windows Server 2012.
        -   Linux: CentOS, SUSE, Ubuntu, Debian, FreeBSD, CoreOS, Aliyun, Customized Linux, and Others Linux \(open a ticket to confirm the selected edition is supported\).
        -   If your image operating system is a custom edition developed from Linux kernel, open a ticket to contact us.
    -   **Image Format**: Supports QCOW2, RAW, and VHD. QCOW2 or VHD is recommended.

        **Note:** The ISO format is not supported. You can use offline tools such as VirtualBox to create an ISO image file and then convert it to the QCOW2, RAW, or VHD format. You can also [use Packer to create and import a local image](reseller.en-US/Images/Custom image/Create custom image/Create and import on-premises images by using Packer.md#). For more information, see [Create an image by using a local ISO file](../reseller.en-US/Best Practices/Packer: machine images as code/Configure DevOps parameters by using Packer.md#).

    -   **Image Description**: Enter a description of the custom image.
    -   **Add Images of Data Disks**: Choose this option if you want to import an image that contains data disks. Supported data disk capacity ranges from 5 GiB to 2,000 GiB.
10. Click **OK**.
11. \(Optional\) You can view the task progress in the image list of the import region. Before the task is completed, you can find the imported custom image through [Tasks](https://partners-intl.console.aliyun.com/#/ecs/task/region/) management, and, if needed, cancel the import task.

The time it takes to import a custom image depends on the size of the image file and the number of image import tasks in the queue.

You can also call the [ImportImage](../reseller.en-US/API Reference/Images/ImportImage.md#) action to import a custom image or [use Packer to create and import a local image](reseller.en-US/Images/Custom image/Create custom image/Create and import on-premises images by using Packer.md#).

## What to do next {#section_mhq_zps_xdb .section}

[Create an instance from a custom image](reseller.en-US/Instances/Create an instance/Create an instance by using a custom image.md#).

## References {#section_pkr_1qs_xdb .section}

-   [Custom images FAQ](https://partners-intl.aliyun.com/help/faq-detail/40549.htm)
-   [Create and import on-premise images by using Packer](reseller.en-US/Images/Custom image/Create custom image/Create and import on-premises images by using Packer.md#)
-   [Change the operating system of an image](reseller.en-US/Images/Change the operating system.md#)

