# Create a custom image by using a snapshot {#concept_gpg_t5l_xdb .concept}

This topic describes how to create a custom image by using a snapshot. A custom image typically contains the operating system and data environment of an ECS instance that you can use to create multiple, identical ECS instances. You can also change the configurations of ECS instances created by a custom image as needed.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9696/15659363444584_en-US.png)

You can also use an instance to create an image. For more information, see [Create a custom image by using an instance](reseller.en-US/Images/Custom image/Create custom image/Create a custom image by using an instance.md#).

To enhance the security of custom images created from snapshots, see [Security suggestions for Alibaba Cloud custom image](https://partners-intl.aliyun.com/help/faq-detail/54903.htm?spm=a2c63.q38357.a3.3.358654ffzwageD).

## Limits {#section_adn_35b_fhb .section}

Before you proceed, note the following:

-   Custom images must be created from system disk snapshots \(or system disk snapshots and data disk snapshots\). Data disk snapshots alone cannot be used to create custom images.
-   Both encrypted and unencrypted snapshots can be used to create custom images.
-   Custom images cannot be used across regions. However, you can copy custom images to the destination region for later use. For more information, see [Copy custom images](reseller.en-US/Images/Custom image/Copy custom images.md#).
-   Custom images are created independently from the billing methods of the instances from which they were created. For example, custom images created from Subscription instances can be used for creating Pay-As-You-Go instances. The converse method also applies.
-   You can upgrade the instance created from a custom image, including upgrading the CPU, memory, bandwidth, and disks.
-   You can change the operating system of an instance created from a custom image, and the custom image remains usable. For more information, see [Change the system disk \(custom image\)](reseller.en-US/Block Storage/Block storage/Change the operating system/Replace the system disk (non-public image).md#).
-   If the ECS instance used for creating a custom image expires or is released, the custom image and the ECS instances created from the custom image are not affected. However, automatic snapshots are cleared when an ECS instance is released.

## Procedure {#section_p1r_rwl_xdb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Instances & Images** \> **Images**.
3.  In the top navigation bar, select a region.
4.  Find the target instance and click its instance ID, or click **Manage** in the **Actions** column.
5.  In the left-side navigation pane, click **Instance Snapshots**. Find a snapshot whose **Disk Type** is system disk and then click **Create Custom Image** in the **Actions** column.
6.  In the Create Custom Image dialog box, complete the following:

    -   Confirm the snapshot ID.
    -   Enter a name and description of the custom image.
    -   \(Optional\) Check **Add Data Disk Snapshot**, select multiple snapshots of data disks for the image, and click **Add**.

        **Note:** 

        -   If no data disk snapshot is selected \(namely, no data disk snapshot ID is selected\), an empty data disk is created with a default capacity of 5 GiB.
        -   If a data disk snapshot is selected, the disk size is the same as the snapshot size.
        -   We recommend that you remove sensitive data from the data disk before creating a custom image to guarantee data security.
    -   \(Optional\) Attach tags to custom images for classification. For more information, see [Tags](../reseller.en-US/Tags & Resource Management /Tags/Limits.md#).
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9696/156593634441259_en-US.png)


You can also choose **Storage & Snapshots** \> **Snapshots**, and select a snapshot whose **Disk Type** is **System Disk** to create a custom image.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9696/15659363444593_en-US.png)

## What to do next {#section_rwd_lcm_xdb .section}

After you create a custom image, you can:

-   Use it to create instances. For more information, see [Create an instance by using a custom image](reseller.en-US/Instances/Create an instance/Create an instance by using a custom image.md#).
-   Use it to replace the system disk of an instance. For more information, see [Replace a system disk \(non-public image\)](reseller.en-US/Block Storage/Block storage/Change the operating system/Replace the system disk (non-public image).md#).

