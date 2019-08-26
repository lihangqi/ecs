# Detach a cloud disk {#concept_i1f_kgg_ydb .concept}

If a Pay-As-You-Go cloud disk is attached to an ECS instance as a data disk, you can detach it from the instance and release it. However, if the disk is used as a system disk, you cannot detach it.

When detaching a cloud disk, consider the following:

-   Only the Pay-As-You-Go cloud disks in the **In Use** state and used as a **Data Disk** can be detached.
-   You cannot detach a local disk.
-   For a Windows instance:
    -   To guarantee data integrity, we recommend that you stop writing or reading the files on the cloud disk. Otherwise, data may be lost.
    -   Before detaching a cloud disk in the ECS console, you must [connect to the instance](reseller.en-US/Instances/Connect to instances/Connect to Windows instances/Connect to a Windows instance.md#) and set its status to **Offline** in **Disk Management**.
-   For a Linux instance:

    -   Before detaching a cloud disk in the ECS console, you must [connect to the instance](reseller.en-US/Instances/Connect to instances/Overview.md#) and run `umount` to unmount the partitions.
    -   If you have configured the /etc/fstab file to automatically mount the partitions at the startup of the instance, before detaching it, you must delete the configurations from the /etc/fstab file. Otherwise, you cannot connect to the instance after the instance is restarted.

The following table describes the actions available for you to detach a cloud disk in the ECS console.

|Scenario|Action|
|:-------|:-----|
|You want to detach one or more cloud disks from one instance.|[Detach cloud disks on the Instance Disk page](#InstanceCloud).|
|You want to detach one specific cloud disk.|[Detach a cloud disks on the Disk List page](#CloudCloud).|

## Detach cloud disks on the Instance Disk page {#InstanceCloud .section}

On the Instance Disks page, you can delete one or more cloud disks that are attached to the instance.

**Prerequisites** 

The cloud disks are [attached to the instance](reseller.en-US/Block Storage/Block storage/Attach a cloud disk.md#) and its status is **In Use**.

If you are detaching a cloud disk from a Linux instance, and you have configured the /etc/fstab file to mount the partitions at the startup of the instance, you must first delete the configurations.

**Procedure** 

To detach a cloud disk from the Instance Disks page, follow these steps:

1.  Connect to the instance and unmount its partitions. According to the operating system, follow the recommended steps detailed in the following table.

    |Operating system|Steps|
    |:---------------|:----|
    |Linux|Run `umount [partition]`. For example, `umount /dev/vdb1`.|
    |Windows|Start Disk Management, right-click the disk name \(for example, **Disk 2**\) and then click **Offline**.|

2.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
3.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.
4.  In the top navigation bar, select a region.
5.  Find the target instance and click its ID to go to the **Instance Details** page.
6.  In the left-side navigation pane, click **Disks**.
7.  Find the target cloud disk and then, in the **Actions** column, select **More** \> **Unmount**.

    Only cloud disks that have the following attributes can be detached:

    -   **Status** must be **In Use**.
    -   **Detachable** must be **Yes**.
    -   **Type** must be **Data Disk**.
8.  In the dialog box, click **Confirm**.
9.  Optional. If you want to detach multiple cloud disks, repeat steps 7 and 8 as required.

When the status of the cloud disk becomes **Unattached**, the disk is detached.

## Detach a cloud disks on the Disks page {#CloudCloud .section}

On the Disk List page, you can detach a specific cloud disk from an ECS instance.

**Prerequisites** 

The cloud disk is [attached to the instance](reseller.en-US/Block Storage/Block storage/Attach a cloud disk.md#) and is in the **In Use**state.

If you are detaching a cloud disk from a Linux instance, and you have configured the /etc/fstab file to mount the partitions at the startup of the instance, delete the configurations.

**Procedure** 

To detach a cloud disk on the Disk List page, follow these steps:

1.  Connect to the instance and unmount the partitions. According to the operating system, follow the recommended steps detailed in the following table.

    |Operating system|Steps|
    |:---------------|:----|
    |Linux|Run `umount [partition]`. For example, `umount /dev/vdb1`.|
    |Windows|Start Disk Management, right-click the disk name \(for example, **Disk 2**\) and then click **Offline**.|

2.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
3.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Disks**.
4.  In the top navigation bar, select a region.
5.  Find the target cloud disk and then, in the **Actions** column, select **More** \> **Unmount**.

    Only cloud disks that have the following attributes can be detached:

    -   **Status** must be **In Use**.
    -   **Detachable** must be **Yes**.
    -   **Type** must be **Data Disk**.
6.  In the dialog box, click **Confirm**.

When the status of the cloud disk becomes **Unattached**, the disk is detached.

## Related API {#section_ijl_1qh_ydb .section}

[DetachDisk](../reseller.en-US/API Reference/Disk/DetachDisk.md#)

## What to do next {#section_jjl_1qh_ydb .section}

If you no longer need the disk, you can [release it](reseller.en-US/Block Storage/Block storage/Release a cloud disk.md#).

