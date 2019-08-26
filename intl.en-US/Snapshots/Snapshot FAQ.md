# Snapshot FAQ {#concept_j5z_vrr_lgb .concept}

This topic lists FAQ related to ECS snapshots.

-   OSS-related questions
    -   [If I have activated OSS, will snapshots automatically be saved to my OSS buckets?](reseller.en-US/Snapshots/Snapshot FAQ.md#section_wnf_qh1_4gb)
    -   [Can a custom image that was created from a snapshot be saved to an OSS bucket?](#section_agb_789_ug8)
-   Billing-related questions
    -   [Where can I view a list of snapshot prices by Alibaba Cloud region?](#section_nom_iuk_an9)
    -   [What impact will unpaid bills have on snapshots?](#section_qs5_lyg_4gb)
    -   [I use snapshots frequently. How can I reduce the amount of fees incurred?](#section_75v_zgn_06k)
-   Snapshot and block storage type-related questions
    -   [Are automatic snapshots different from or in conflict with manual snapshots?](#section_vj5_5ws_ngb)
    -   [Can I create snapshots for local disks?](#section_8bp_ymj_xsh)
    -   [I have created a snapshot for an encrypted data disk and generated an image but cannot share the image. Why?](#section_m0o_tpa_pb2)
-   Snapshot capacity-related questions
    -   [Will deleting files in an ECS instance free up storage space?](#section_akt_4yg_4gb)
    -   [Why is the snapshot size larger than the disk size displayed in the file system?](#section_rr2_pyg_4gb)
    -   [What is the relationship between a file system and a cloud disk or a snapshot?](#section_tsa_qqu_wdx)
-   Snapshot deletion-related questions
    -   [How can I prevent snapshots from being deleted by Alibaba Cloud?](#section_wj5_5ws_ngb)
    -   [Can snapshots be deleted to reduce backup costs?](#section_pjl_hqz_ngb)
    -   [Will automatic snapshots be deleted after the system disk is changed, the instance expires, or the cloud disk is released?](#section_ck5_5ws_ngb)
    -   [How can I delete snapshots that have been used to create images and cloud disks?](#section_hji_juh_uhk)
-   Automatic snapshot policy-related questions
    -   [If I have used an automatic snapshot to create a custom image or a cloud disk, will the automatic snapshot policy fail to be executed?](#section_xj5_5ws_ngb)
    -   [Can I create multiple snapshot policies for a cloud disk?](#section_dx2_bzg_4gb)
-   Disk rollback with snapshot-related questions
    -   [How can I avoid losing data due to misoperations?](#section_oou_9ap_jvp)
    -   [After you change the system disk, can a snapshot of a previous system disk be used to roll the new system disk back?](#section_hpz_qkh_mgb)

## If I have activated OSS, will snapshots automatically be saved to my OSS buckets? {#section_wnf_qh1_4gb .section}

No. Snapshots will not automatically be saved to existing OSS buckets. The storage location of snapshots is independent of existing OSS buckets. You do not need to create new buckets for snapshots.

## Can a custom image that was created from a snapshot be saved to an OSS bucket? {#section_agb_789_ug8 .section}

Yes. You can export the image to your OSS bucket to download in the future. For more information, see [../../../../dita-oss-bucket/SP\_2/DNECS19100339/EN-US\_TP\_9712.md\#](../../../../reseller.en-US/Images/Custom image/Export custom images.md#). However, custom images cannot be directly stored to the OSS bucket.

## Where can I view a list of snapshot prices by Alibaba Cloud region? {#section_nom_iuk_an9 .section}

The price per GiB to store snapshots is the same as that of OSS standard storage and charged on a monthly basis. For a list of snapshot prices by Alibaba Cloud region, see the Pricing tab of the Elastic Compute Service page.

## What impact will unpaid bills have on snapshots? {#section_qs5_lyg_4gb .section}

Snapshots will be suspended 24 hours after an unpaid bill becomes overdue. After the unpaid bill becomes overdue:

-   In the first 15 days, all existing snapshots will be retained, but no new snapshots will be created. Snapshots that have their retention period expire within these 15 days will be cleared normally.
-   After 15 days, all snapshots will be deleted except for those which have been used to create cloud disks or custom images.

You can recharge your account to resume the snapshot service. For more information, see [Recharging](https://help.aliyun.com/knowledge_list/37106.htm).

## I use snapshots frequently. How can I reduce the amount of fees incurred? {#section_75v_zgn_06k .section}

We recommend that you maintain an appropriate number of snapshots, and delete unnecessary snapshots. For more information, see [Reduce snapshot fees](reseller.en-US/Snapshots/Use snapshots/Reduce snapshot fees.md#).

## Are automatic snapshots different from or in conflict with manual snapshots? {#section_vj5_5ws_ngb .section}

No. Both manual snapshots and automatic snapshots are data files of a cloud disk and shared block storage device at a certain point in time. However, you cannot create manual snapshots while an automatic snapshot is being created. You must wait until after the automatic snapshot has been created.

## Can I create snapshots for local disks? {#section_8bp_ymj_xsh .section}

No. If you want to improve the high availability performance of applications, we recommend that you create data redundancy at the application layer or create deployment sets for clusters.

## I have created a snapshot for an encrypted data disk and generated an image but cannot share the image. Why? {#section_m0o_tpa_pb2 .section}

To ensure data privacy, custom images created from encrypted snapshots cannot be shared. We recommend that you use unencrypted snapshots to create custom images that can be shared with other users.

## Will deleting files in an ECS instance free up storage space? {#section_akt_4yg_4gb .section}

No. When you delete files in an ECS instance, tags are added to the file headers but space is not cleared in the cloud disks.

## Why is the snapshot size larger than the disk size displayed in the file system? {#section_rr2_pyg_4gb .section}

-   Issue: You have created a snapshot after deleting files in the ECS instance. However, the size of the snapshot has not been reduced, or the size of the snapshot is larger than that of the disk size displayed in the file system.
-   Cause: When snapshots are created, a mechanism identifies empty blocks to reduce the size of the snapshot. However, empty blocks will be occupied when you format the file system, delete files, and write data to blocks. Because of this, the snapshot size may be larger than the disk size currently displayed in the file system. Specific causes:
    -   File system metadata is occupying disk space.
    -   The file system has written data to a large number of blocks divided equally from the logical block address during initialization. This operation also will occupy disk space.
    -   To improve performance, the file system only adds tags to the headers of files when they are deleted. Because the disk cannot detect delete instructions, data blocks will still be allocated and copied to the snapshots.
    -   The KVM virtio block and Xen block front drivers do not support the TRIM instruction, an I/O instruction used to prompt that data in the logical block address is no longer in use and can be deleted.

## What is the relationship between a file system and a cloud disk or a snapshot? {#section_tsa_qqu_wdx .section}

You can create a file system in a disk partition. The file system manages disk space. These management tasks take the form of I/O requests in the disk. The disk records the states of data blocks and copies the data to OSS as needed. This process is how snapshots are created. The following figure shows the relationship between a file system and a snapshot.

![Relationship between a file system and a cloud disk or a snapshot](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10122/156637844839434_en-US.png)

**Note:** In the preceding figure, any data blocks with data written to them will be recorded in the snapshot, even if the related files have been deleted from the disk. In the file system, only tags are added in the headers of files to deleted but space is not cleared in the cloud disks.

## How can I prevent snapshots from being deleted by Alibaba Cloud? {#section_wj5_5ws_ngb .section}

-   Manual snapshots will never be deleted by Alibaba Cloud, regardless of whether the cloud disk or instance has been released.
-   Automatic snapshots: When you [Modify an automatic snapshot policy](reseller.en-US/Snapshots/Automatic snapshot policies/Modify an automatic snapshot policy.md#), you can set the **Keep Snapshots** parameter to **Always Keep**. Snapshots will then only be deleted when the maximum number of snapshots \(64\) has been reached.

## Can snapshots be deleted to reduce backup costs? {#section_pjl_hqz_ngb .section}

-   Manual snapshots: You can delete manual snapshots.
-   Automatic snapshots: You can delete automatic snapshots. When the maximum number of snapshots is reached, the system will delete the earliest automatic snapshot.

## Will automatic snapshots be deleted after the system disk is changed, the instance expires, or the cloud disk is released? {#section_ck5_5ws_ngb .section}

-   If **Delete Automatic Snapshots While Releasing Disk** is selected for the automatic snapshot policy, the automatic snapshots will be deleted when the corresponding instance or cloud disk is released.
-   If **Delete Automatic Snapshots While Releasing Disk** is not selected for the automatic snapshot policy, the retention period of the automatic snapshot policy applies. If necessary, you can [Modify an automatic snapshot policy](reseller.en-US/Snapshots/Automatic snapshot policies/Modify an automatic snapshot policy.md#).

## How can I delete snapshots that have been used to create images and cloud disks? {#section_hji_juh_uhk .section}

-   You can delete snapshots that have been used to create cloud disks. After deleting snapshots, you cannot perform operations that depend on the status of the original snapshot data, such as the operation to [reinitialize a cloud disk](../../../../reseller.en-US/Block Storage/Block storage/Reinitialize a cloud disk/Reinitialize a cloud disk.md#).
-   If a snapshot has been used to create custom images, you must delete those custom images before the snapshot can be deleted.
-   You can delete images that have been used to create instances. After a snapshot is deleted, you cannot perform operations that depend on the status of the original snapshot data, such as the operation to [reinitialize a cloud disk](../../../../reseller.en-US/Block Storage/Block storage/Reinitialize a cloud disk/Reinitialize a cloud disk.md#).

## If I have used an automatic snapshot to create a custom image or a cloud disk, will the automatic snapshot policy fail to be executed? {#section_xj5_5ws_ngb .section}

No.

## Can I create multiple snapshot policies for a cloud disk? {#section_dx2_bzg_4gb .section}

No.

## How can I avoid losing data due to misoperations? {#section_oou_9ap_jvp .section}

You can create snapshots to back up data in advance before you perform operations that carry risks to your data. For example, you can create a snapshot if you need to modify critical system files, migrate instances from a classic network to a VPC, back up data, restore an instance that was released by accident, prevent network attacks, change operating systems, or provide data support for a production environment. If an error occurs, you can roll back the cloud disk in time to reduce risks. For more information, see [Create a snapshot](reseller.en-US/Snapshots/Use snapshots/Create a snapshot.md#) and [Roll back a disk by using a snapshot](reseller.en-US/Snapshots/Use snapshots/Roll back a disk by using a snapshot.md#).

## After you change the system disk, can a snapshot of a previous system disk be used to roll the new system disk back? {#section_hpz_qkh_mgb .section}

No.

