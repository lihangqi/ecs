# Modify the performance level of an ESSD cloud disk {#task_810820 .task}

This topic describes how to modify the performance level of a running ESSD cloud disk in the ECS console.

You can follow the steps in this guide if your ESSD cloud disk meets the following requirements:

-   Your account does not have overdue payment.
-   If you attach an ESSD cloud disk to a Pay-As-You-Go ECS instance, make sure that the instance is not in the **Expired** state.
-   You can change the performance level of a new ESSD cloud disk only after it enters the **Unattached** \(Available\) state.

When you create an ECS instance, you can set the ESSD cloud disk as the system disk or data disk. You can also create a separate ESSD cloud disk. For information about how to create an ESSD cloud disk, see [Create an instance by using the wizard](../reseller.en-US/Instances/Create an instance/Create an instance by using the wizard.md#) and [Create a Pay-As-You-Go cloud disk](reseller.en-US/Block Storage/Block storage/Create a cloud disk/Create a Pay-As-You-Go cloud disk.md#). For information about ESSD cloud disks, see [ESSD cloud disk](reseller.en-US/Block Storage/Block storage/ESSD cloud disk.md#).

After the performance level is modified, the ESSD cloud disk is billed according to the new performance level.

You can also call the API action [ModifyDiskSpec](../reseller.en-US/API Reference/Disk/ModifyDiskSpec.md#) to complete this task.

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Disks**.
3.  In the top navigation bar, select a region.
4.  Find the target ESSD cloud disk. In the **Actions** column, choose **More** \> **Modify Performance Level**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/655586/156593753850139_en-US.png)

5.  In the Modify Performance Level dialog box, select a higher performance level and click **OK**. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/655586/156593753850141_en-US.png)


The performance level you can select for an ESSD cloud disk is determined by its storage capacity. If the performance level of an ESSD cloud disk cannot be upgraded, [resize the ESSD cloud disk](reseller.en-US/Block Storage/Block storage/Resize cloud disks/Overview.md#) and then modify its performance level.

