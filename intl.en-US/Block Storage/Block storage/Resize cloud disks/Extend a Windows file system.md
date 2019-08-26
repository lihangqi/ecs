# Extend a Windows file system {#concept_rjc_l5h_ydb .concept}

This topic describes how to extend a Windows file system. Resizing a cloud disk does not extend the file system; it only extends the storage capacity. Therefore, you need to format the new storage capacity after you resize a cloud disk.

## Limits {#section_hst_vj1_qgb .section}

The information contained in this topic applies only to disks that are in use and are attached to **Running** instances. For information on how to attach, partition, or format disks that are in the **Available** state, see [Attach a cloud disk](reseller.en-US/Block Storage/Block storage/Attach a cloud disk.md#) and [Partition and format a data disk](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk of a Linux instance.md#).

## Preparations {#section_fds_2m1_qgb .section}

1.  Use the ECS console or call the API to resize the cloud disk.
2.  [Create a snapshot](reseller.en-US/Snapshots/Use snapshots/Create a snapshot.md#) to back up your data.
3.  Attach the cloud disk to the instance and make sure that the instance is in the **Running** state. For information about the connection methods, see [Overview](../../../../reseller.en-US/Instances/Connect to instances/Overview.md#).
4.  Format and partition the data disk. For more information, see [Partition and format a data disk](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk of a Linux instance.md#).

## Extend the system disk partition {#section_h4v_txm_qgb .section}

After you resize a system disk in the ECS console, you need to connect to the instance to extend the file system of the corresponding system disk partition. In this example, the operating system is Windows Server 2008 R2 Enterprise Edition 64-bit and the system disk is resized from 50 GiB to 72 GiB.

1.  [Connect to the Windows instance](reseller.en-US/Instances/Connect to instances/Connect to Windows instances/Connect to a Windows instance.md#).
2.  Open Server Manager.
3.  In the left-side navigation pane, choose **Storage** \> **Disk Management**.
4.  Choose **Action** \> **Refresh** or **Action** \> **Rescan Disks**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9678/155643430141660_en-US.png)

5.  In the Disk Management area, view the unallocated capacity. In this example, **Disk 0** is the resized system disk.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9678/155643430241658_en-US.png)

6.  Right-click the blank space in the **Disk 0** area, and then select **Extend Volume**.
7.  Follow the instructions provided by the Extend Volume Wizard to extend the volume.

    The new disk space is automatically added to the original volume.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9678/155643430341657_en-US.png)


## Extend a data disk partition {#section_hbw_5lw_dhb .section}

After you resize a data disk in the ECS console, you need to connect to the instance to extend the file system of the corresponding data disk partitions. In this example, the operating system is Windows Server 2008 R2 Enterprise Edition 64-bit and the data disk is resized from 20 GiB to 30 GiB.

1.  [Connect to the Windows instance](reseller.en-US/Instances/Connect to instances/Connect to Windows instances/Connect to a Windows instance.md#).
2.  Open Server Manager.
3.  In the left-side navigation pane, choose **Storage** \> **Disk Management**.
4.  Choose **Action** \> **Refresh** or **Action** \> **Rescan Disks**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9678/155643430141660_en-US.png)

5.  In the Disk Management area, view the unallocated capacity. In this example, **Disk 1** is the resized data disk.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9678/155643430341665_en-US.png)

6.  Extend **Disk 1**.
    -   To use the new disk space to extend the existing partition, follow these steps:
        1.  Right-click the blank space in the **Disk 1** area, and then select **Extend Volume**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9678/155643430341661_en-US.png)

        2.  Follow the instructions provided by the Extend Volume Wizard to extend the volume.

            The new disk space is automatically added to the original volume.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9678/155643430441662_en-US.png)

    -   To use the new disk space to add a new partition, follow these steps:
        1.  Right-click the bank space in the **Disk 1** area, and then select **New Simple Volume**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9678/155643430441663_en-US.png)

        2.  Follow the instructions provided by the New Simple Volume Wizard to extend the volume.

            The new disk space is added to a new partition.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9678/155643430441664_en-US.png)


