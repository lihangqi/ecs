# Import custom images {#concept_w4x_4ms_xdb .concept}

You can import on-premises image files to your ECS environment to create ECS instances or change system disks

**Note:** 

-   The time it takes to import an image depends on the size of the image file and the number of concurrent tasks.
-   When you import an image, a snapshot is automatically generated. You can view the snapshot information on the **Snapshots** page in the ECS Console. Before the import image task is completed, the status of the snapshot is displayed as **Failed**. When the task is completed, the status is automatically updated to **Successful**. The snapshot capacity is the size of the imported image file, regardless of the system disk size that was set when the image was imported.

## Prerequisites {#section_jn1_5ns_xdb .section}

Before importing an image, we recommend that you:

-   Review the [notes for importing images](reseller.en-US/User Guide/Images/Import images/Notes for importing images.md#), [customize Linux images](reseller.en-US/User Guide/Images/Import images/Customize Linux images.md#), and [convert image format](reseller.en-US/User Guide/Images/Import images/Convert image file format.md#) to understand the limitations of importing an on-premises image.
-   [Activate OSS](../../../../../reseller.en-US/Quick Start/Sign up for OSS.md#).
-   \(Optional\) If you are using a RAM user account, you need to contact the Alibab Cloud account to obtain permission for the `AliyunECSImageImportDefaultRole` role.

## Procedure {#section_nc3_yns_xdb .section}

To import custom images in the ECS console, follow these steps:

1.  Use an OSS third-party client, OSS API or OSS SDK to upload the prepared custom image. If the file you want to upload is larger than 5 GiB, see [multipart upload](../../../../../reseller.en-US/Developer Guide/Upload files/Multipart upload.md#).
2.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
3.  In the left-side navigation pane, choose **Snapshots and Images** \> **Images**.
4.  Click **Import Image**.
5.  In the Import Image dialog box, click **Confirm Address** as follows.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9706/15433094017027_en-US.png)
6.  In the Cloud Resource Access Authorization window, select `AliyunECSImageImportDefaultRole` and `AliyunECSExportDefaultRole`, then click **Confirm Authorization Policy** to allow the ECS service to access your OSS resources.
7.  On the Images page, click **Import Image** again.
8.  In the Import Image dialog box, enter the following information:
    -   **Region of Image**: Select the region where the OSS Bucket of the image file to upload is located.
    -   **OSS Object Address**: Copy the object address of the image file from the OSS console. For more information, see [download an object](../../../../../reseller.en-US/Console User Guide/Manage objects/Download an object.md#).
    -   **Image Name**: Enter a name for the custom image. The name must be 2 to 128 characters in length and can contain letters, numbers, Chinese characters, periods \(.\), underscores \(\_\), colons \(:\), and hyphens \(-\).
    -   **Operating System**: Select **Windows** or **Linux**, that is, the same as that of your image. If you want to import a non-standard platform image, select Linux.
    -   **System Disk Size**: The system disk size, which ranges from 40 GiB to 500 GiB.
    -   **System Architecture**: Choose **x86\_64** for 64 bit operating systems and choose **i386** for 32 bit operating systems.
    -   **Platform**: The options depend on the **Operating System** you chose.
        -   Windows: Windows Server 2003, Windows Server 2008, and Windows Server 2012.
        -   Linux: Centos, SUSE, Ubuntu, Debian, FreeBSD, CoreOS, Aliyun, Customized Linux, and Others Linux \(open a ticket to confirm the selected edition is supported\).
        -   If your image OS is a custom edition developed from Linux kernel, open a ticket to contact us.
    -   **Image Format**: Supports qcow2, RAW, and VHD. Qcow2 or VHD is recommended.
    -   **Image Description**: Enter a description of the custom image.
    -   **Add Images of Data Disks**: Choose this option if you want to import an image that contains data disks. Supported data disk capacity ranges from 5 GiB to 2,000 GiB.
9.  Click **OK**.
10. \(Optional\) You can view the task progress in the image list of the import region. Before the task is completed, you can find the imported custom image through [Tasks](https://partners-intl.console.aliyun.com/#/ecs/task/region/) management, and, if needed, cancel the import task.

You can also use the ECS API [ImportImage](../reseller.en-US/API Reference/Images/ImportImage.md#) to import a custom image.

## Next step {#section_mhq_zps_xdb .section}

[Create an instance from a custom image](reseller.en-US/User Guide/Instances/Create an instance/Create an instance from a custom image.md#).

## References {#section_pkr_1qs_xdb .section}

-   [Custom images FAQ](https://partners-intl.aliyun.com/help/faq-detail/40549.htm)
-   [Create and import on-premise images by using Packer](reseller.en-US/User Guide/Images/Open source tools/Create and import on-premises images by using Packer.md#)

