# Create a Subscription cloud disk {#concept_apf_b4z_bgb .concept}

To increase the storage space for a Subscription instance, you can create a Subscription cloud disk for that instance in the ECS console. This topic describes how to create a Subscription cloud disk for a Subscription instance in the ECS console.

## Precautions {#section_twr_tx1_ydb .section}

Before you create a cloud disk, note the following:

-   If you create a Subscription cloud disk for a Subscription instance on the **Instances** page in the ECS console, that cloud disk is billed in the [Subscription](../../../../../intl.en-US/Pricing/Subscription.md#) method and can only work as a data disk.

    **Note:** You can create a cloud disk as a data disk when creating a Subscription instance. Cloud disks created in this way have the same billing method as the corresponding instance.

-   You can create a new empty cloud disk or [Create a cloud disk from a snapshot](intl.en-US/Block storage/Cloud disks/Create a cloud disk/Create a cloud disk from a snapshot.md#).
-   Currently, ECS does not allow you to merge multiple cloud disks. Each cloud disk is an independent entity. You cannot merge the disks by formatting them. We recommend that you determine the number and size of cloud disks before you create them.
-   For multiple cloud disks that were previously created, we do not recommend that you create logical volumes such as Logical Volume Manager \(LVM\) volumes. This is because a snapshot is created only for an independent cloud disk. If LVM is used, data loss will occur when you use a snapshot to restore a cloud disk.
-   For cloud disks created in this way, you cannot [Detach a cloud disk](intl.en-US/Block storage/Cloud disks/Detach a cloud disk.md#). Such cloud disks expire at the same time as the corresponding instances.

    **Note:** To release a Subscription cloud disk, convert its billing method to Pay-As-You-Go, detach it, and then release it.


## Procedure {#section_axr_tx1_ydb .section}

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/?spm=a2c4g.11186623.2.9.FNEORG#/home).
2.  In the left-side navigation pane, click **Instances**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/79763/155106066338501_en-US.png)

3.  On the Instances page, find the target Subscription instance, and then click **More** in the **Actions** column.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/79763/155106066338504_en-US.png)
4.  Click **Configuration Change** \> **Add Subscription Cloud Disk**.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/79763/155106066338505_en-US.png)
5.  In the **Disk** area of the displayed page, complete the following configurations:
    -   Cloud disk type: Select a [cloud disk type](../../../../../intl.en-US/Block storage/Block storage/Cloud disks and Shared Block Storage.md#) in the drop-down box.
    -   Cloud disk capacity: Enter a cloud disk capacity in the text box. The disk capacity ranges from 20 GiB to 32,768 GiB.
    -   Cloud disk encryption: If [ECS disk encryption](../../../../../intl.en-US/Block storage/Block storage/ECS disk encryption.md#) is needed, select the **Encrypted** check box.
    -   Quantity: Enter the number of cloud disks to add in the text box.

        **Note:** You can create up to 16 data disks \(including cloud disks and shared block storage devices\) for a single instance.

    -   Disk Name: Optional. You can enter a disk name in the text box. A disk name can contain 2 to 128 English letters or Chinese characters in length. It can also contain numbers, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\).
    -   Description: Optional. You can enter a disk description in the text box. The description information can contain 2 to 256 English letters or Chinese characters. It cannot start with http:// or https://.
    -   If you need to [Create a cloud disk from a snapshot](intl.en-US/Block storage/Cloud disks/Create a cloud disk/Create a cloud disk from a snapshot.md#), click **Create from snapshot**.
    -   ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/79763/155106066338506_en-US.png)
6.  Select the *ECS Service Level Agreement* check box.
7.  Click **Preview**.
8.  Click **Create Order**.
9.  Select a payment method and click **Confirm to Pay** to complete the creation.
10. Click **ECS console** to return to the **Instances** page. In the instance list, click the instance for which the Subscription cloud disk has just been added.
11. Click **Disks** to view the newly added Subscription cloud disk.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/79763/155106066438507_en-US.png)

