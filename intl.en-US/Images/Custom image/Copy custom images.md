# Copy custom images {#concept_a3m_5dm_xdb .concept}

This topic describes how to copy a custom image that is under your Alibaba Cloud account. This action enables you to create identical ECS instances across regions, allowing you to implement seamless data backups of the target instances.

## Background information {#section_l4m_ltd_2hb .section}

An image is a regional resource, and a custom image belongs to the region where it is created. The following table lists the different scenarios of using custom images.

|Scenario|Procedure|Description|
|:-------|:--------|:----------|
|Copy images across regions under the same account|See [Copy images](#section_copy_image).|When an image is copied, the corresponding snapshot is generated in the target region at the same time. After the copy operation is completed, a new image is generated in the target region, and it has a unique image ID.|
|Copy images across regions under different accounts|See [Copy images](#section_copy_image) and [Share images](reseller.en-US/Images/Custom image/Share custom images.md#).|An image is copied to the target region and then shared with the target account.|
|Share images in the same region under different accounts|See [Share images](reseller.en-US/Images/Custom image/Share custom images.md#).|This operation does not create a new image. The shared image still belongs to you.|

## Limits {#section_wgf_n2m_xdb .section}

Before you copy a custom image, note the following:

-   Only custom images can be copied across regions. If you need to copy an image of another type, you need to first use that image to create an instance and then use that instance to create a custom image. Afterwards, you can copy the newly created custom image to the target region.

-   When an image is copied, a corresponding snapshot is generated in the target region at the same time, and then a custom image is generated based on the snapshot. Therefore, data traffic occurs between the source and target regions. Currently, no fees are charged for this traffic. For the latest billing details, see the official Alibaba Cloud website for announcements.
-   The created custom image in the target region has the same configuration as the original custom image. However, the related role authorization and service authorization information is not copied, nor are the settings of [instance user data](../reseller.en-US/Instances/Manage instances/User-defined data/User data.md#).
-   The task completion time depends on the image size, the network transmission speed, and the number of concurrent tasks in the queue.
-   Images with encrypted snapshots cannot be copied across regions.

## Procedure {#section_copy_image .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Instances & Images** \> **Images**.
3.  In the top navigation bar, select a region.
4.  Select the custom image to be copied. Note that **Type** must be **Custom Image**. Then, in the **Actions** column, click **Copy Image**.

    **Note:** If your custom image is larger than 500 GiB, when you click **Copy Image**, you will be directed to open a ticket to complete the operation.

5.  In the Copy Image dialog box, verify the ID of the selected image is the target image, and then complete the following configurations:
    1.  Select the **Target Region**.
    2.  Enter **Custom Image Name** and **Custom Image Description** that are shown in the target region.
    3.  Click **OK**.
6.  \(Optional\) Switch to the target region and check the progress. When 100% is displayed, the image is copied successfully.

    **Note:** If **Progress** is not 100%, **Status** is **Creating**. In this case, you can click **Cancel Copy** to cancel the operation. After the operation is canceled, the image information is removed from the target region.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9699/15665433764607_en-US.png)


You can also call the [CopyImage](../reseller.en-US/API Reference/Images/CopyImage.md#) and [CancelCopyImage](../reseller.en-US/API Reference/Images/CancelCopyImage.md#) API actions to perform the preceding operations.

## What to do next {#section_kmp_xfm_xdb .section}

When a copied image is in the **Available** state, you can use it to [create an instance](../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#) or [change the system disk](../reseller.en-US/Block Storage/Block storage/Change the operating system/Replace the system disk (non-public image).md#).

You can also view the copied snapshot in the target region.

