# Manage snapshots {#concept_ch5_2pl_xdb .concept}

This topic describes how to manage your snapshots.

## Maintain an appropriate number of snapshots {#section_cd4_ssh_mgb .section}

The more snapshots you create, the more disk capacity you require. Therefore, we recommend that you maintain an appropriate number of snapshots and snapshot policies depending on your specific service needs.

|Item|Snapshot creation frequency|Retention duration or quantity|Note|
|:---|:--------------------------|:-----------------------------|:---|
|Critical application|Once every day or every two days|Several months or more|We recommend that you store critical data for a longer time.|
|Non-critical application|Once every week or every two weeks|Several days or weeks|We recommend that you maintain one or two snapshots for disk rollback.|
|System disk|Whenever needed|one or two snapshots|We recommend that you do not store critical application data in the system disk.|
|Software upgrade|We recommend that you delete the snapshot immediately after use.| We recommend that you reserve the necessary space for snapshots.

 We recommend that you delete the snapshot immediately after use.|
|Modification of critical files|
|Migration of application data|
|Test environment|

## Delete one or more snapshots {#section_dkx_mpl_xdb .section}

If you no longer need a snapshot, you can delete it. If the number of snapshots exceeds the snapshot quota, you must delete some snapshots to release storage space. The following procedure describes how to delete one or more snapshots in the ECS console. If a snapshot is used to create custom images, you must delete the associated images before you can delete the snapshot.

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Snapshots**.
3.  Select one or more snapshots to be deleted.
4.  Click **Delete**, and then click **OK** in the displayed dialog box.

Related API: [DeleteSnapshot](../reseller.en-US/API Reference/Snapshots/DeleteSnapshot.md#).

**Delete a snapshot that you have used to create images or disks**

-   You can directly delete a snapshot that you have used to create disks. After you delete the snapshot, services associated with the snapshot \(for example, [Reinitialize the disk](../reseller.en-US/Block Storage/Block storage/Reinitialize a cloud disk.md#)\) will become unavailable.
-   To delete a snapshot that you have used to create custom images, you must delete the corresponding images before you can delete the snapshot.
-   You can directly delete a snapshot that you have used to create instances. After you delete the snapshot, services associated with the snapshot \(for example, [Reinitialize the disk](../reseller.en-US/Block Storage/Block storage/Reinitialize a cloud disk.md#)\) will become unavailable.

## Disable unnecessary snapshot policies {#section_ws4_mql_xdb .section}

You can disable unnecessary snapshot policies to avoid redundancy and reduce the storage space occupied by your snapshots.

**Note:** To increase the fault tolerance of your services, we recommend that you maintain at least one snapshot policy for critical services.

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Snapshots**.
3.  On the Snapshots page, click the **Automatic Snapshot Policies** tab.
4.  Find the automatic snapshot policy to be disabled, and then click **Apply Policy** in the **Actions** column.
5.  In the **Create Automatic Snapshot Policy** dialog box, click the **Disks with Policy Applied** tab, select the disk for which you want to disable the policy, and then click **Disable Policy**.

Related API: [CancelAutoSnapshotPolicy](../reseller.en-US/API Reference/Snapshots/CancelAutoSnapshotPolicy.md#).

