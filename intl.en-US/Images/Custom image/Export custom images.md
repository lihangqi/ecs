# Export custom images {#concept_wfq_vdt_xdb .task}

This topic describes how to export Alibaba Cloud custom images and the items that need your attention.

-   Submit a ticket to apply for permissions to export a custom image. Include a short description of how the image will be used.
-   Make sure that you have enabled OSS and that an OSS bucket is available in the region to which your custom image belongs. For more information, see [Create a bucket](../../../../../reseller.en-US/Quick Start/Create a bucket.md#).

    Exporting a custom image will incur OSS storage and download traffic fees. For more information, see [Billing items](../../../../../reseller.en-US/Pricing/Billing items.md#).

-   The custom image to be exported cannot contain Windows Server operating systems.
-   The custom image to be exported cannot contain system disk snapshots that are generated with Alibaba Cloud Marketplace images.
-   The custom image to be exported can only contain snapshots of up to four data disks. The size of each data disk cannot exceed 500 GiB.

Before you export a custom image, note the following items:

-   If an exported custom image contains data disk snapshots, multiple objects appear in your OSS. Objects whose name contains system are system disk snapshots. Objects whose name contains data are data disk snapshots. A data disk snapshot has an identifier corresponding to the source data disk. The identifier is the mount point of the data disk, such as xvdb and xvdc.
-   When using exported images to create instances that use the same configurations, you need to confirm that the storage location and storage space division of files recorded in /etc/fstab are consistent with the exported data disk snapshot information.
-   The time taken to export a custom image depends on the size of the image and the number of ongoing export tasks in the queue.

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Instances & Images** \> **Images**.
3.  In the top navigation bar, select a region.
4.  Find the custom image you want to export. In the **Actions** column corresponding to the image, click More and choose **Export Image** from the shortcut menu. 
    1.  In the Export Image dialog box that appears, click **Confirm Address**. 

        ![Export a custom image](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9712/15665254194655_en-US.png)

    2.  In the Cloud Resource Access Authorization dialog box, click **Confirm Authorization Policy** to allow ECS to access your OSS resources.
5.  Return to the ECS console homepage and access the Images page again. Find the custom image you want to export. In the **Actions** column corresponding to the image, click More and choose **Export Image** from the shortcut menu.
6.  In the Export Image dialog box, configure the following parameters: 
    -   OSS Bucket Address: Select an OSS bucket that belongs to the same region as the custom image.
    -   OSS Object Prefix: Set the prefix of the object name for the custom image. For example, if you set Demo as the prefix, the exported image displayed in the OSS bucket is named Demo-\[automatically generated object name\].
7.  Click **OK** to export the custom image. 

    You can cancel an export task at any time before the task is completed. Go to the [Tasks](https://partners-intl.console.aliyun.com/#/ecs/task/region/cn-qingdao) page in the ECS console, find the relevant task in the specified region, and cancel the task.


-   Log on to the [OSS console](https://partners-intl.console.aliyun.com/#/oss) to query the result of the export task.
-   Download the custom image. For more information, see [Download an object](../../../../../reseller.en-US/Console User Guide/Upload、download and manage objects/Download an object.md#).

    **Note:** The default format of exported custom images is .raw.tar.gz, and the format of the decompressed images is .raw. If your local computer runs on a Mac OS X system, we recommend that you use GNU Tar to decompress the images.


**More information**  


[ExportImage](../reseller.en-US/API Reference/Images/ExportImage.md#)

[CancelTask](../reseller.en-US/API Reference/Others/CancelTask.md#)

