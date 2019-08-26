# Apply automatic snapshot policies to disks {#concept_nyv_k3l_xdb .concept}

This topic describes how to apply automatic snapshot policies to disks by using the ECS console. Automatic snapshots are created on a scheduled basis. They apply to system disks and data disks. Appropriate snapshot policies can increase data security and fault tolerance.

## Limits {#section_an3_vds_ngb .section}

When you apply automatic snapshot policies, note the following limits:

-   You can create a maximum of 100 automatic snapshot policies for one account in a region.
-   If the snapshot quota is reached, the system deletes automatic snapshots, starting with the oldest one. However, manual snapshots are not affected.
-   Manual snapshots do not conflict with automatic snapshots. However, if an automatic snapshot of a disk is being created, you must wait for the automatic snapshot to finish before you can create a manual snapshot.
-   Automatic snapshot policies do not apply to unused basic cloud disks.
-   Automatic snapshots are named in the format of auto\_yyyyMMdd\_X, where:

    -   `auto`: refers to an automatic snapshot.
    -   `yyyyMMdd`: refers to the date on which the automatic snapshot is created. Specifically, `yyyy` refers to the year, `MM` the month, and `dd` the day.
    -   `X`: refers to when a snapshot was created relative to the creation time of other snapshots generated on the same day.
    For example, `auto_20140418_1` refers to the first automatic snapshot created on April 18, 2014.


## Step 1: Open the automatic snapshot policy page {#section_hvg_pbs_ngb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  Select the target region.
3.  In the left-side navigation pane, choose **Snapshots and Images** \> **Automatic Snapshot Policies**.

## Step 2: Create an automatic snapshot policy {#section_vq3_rbs_ngb .section}

1.  On the Automatic Snapshot Policies page, click **Create Policy**.
2.  In the Create Policy dialog box, set the following snapshot policy parameters as needed:
    -   **Name**: It must be 2 to 128 characters in length. It cannot start with a number or contain special characters other than a decimal point \(.\), underscore \(\_\), hyphen \(-\), and colon \(:\).
    -   **Executed At**: the point in time at which an automatic snapshot is created. You can select the hour or hours at which snapshots can be created each day \(from 00:00 to 23:00\).

        **Note:** When you create a snapshot, the I/O performance of block storage automatically degrades by less than 10%, which results in an instantaneous I/O speed decrease. Therefore, we recommend that you create snapshots during off-peak hours.

    -   **Execution Frequency**: the date on which an automatic snapshot is created. You can select one or more days \(from Monday to Sunday\) in each week.
    -   **Keep Snapshots**: By default, a snapshot is kept for 30 days. You can set how long \(from 1 to 65,536 days\) you want to keep a snapshot. Alternatively, you can select **Always Keep**.
3.  Click **OK**.

Related API: [CreateAutoSnapshotPolicy](../../../../reseller.en-US/API Reference/Snapshots/CreateAutoSnapshotPolicy.md#).

## Step 3: \(Optional\) Modify an automatic snapshot policy {#section_uxl_tbs_ngb .section}

1.  On the Automatic Snapshot Policies page, find the policy to be modified, and then click **Modify Policy** in the **Actions** column.
2.  In the Modify Policy dialog box, use the method described in [Step 2: Create an automatic snapshot policy](reseller.en-US/Snapshots/Use snapshots/Apply automatic snapshot policies to disks.md#) to set the name of the snapshot policy, the point in time and frequency at which snapshots are created, and the number of days that the automatic snapshots are retained.
3.  Click **OK**.

Related APIs:

-   To query automatic snapshot policies, call [DescribeAutoSnapshotPolicyEx](../../../../reseller.en-US/API Reference/Snapshots/DescribeAutoSnapshotPolicyEx.md#).
-   To modify automatic snapshot policies, call [ModifyAutoSnapshotPolicyEx](../../../../reseller.en-US/API Reference/Snapshots/ModifyAutoSnapshotPolicyEx.md#).

## Step 4: Apply an automatic snapshot policy {#section_bp4_z2s_ngb .section}

1.  On the Automatic Snapshot Policies page, find the policy to be applied, and then click **Apply Policy** in the **Actions** column.
2.  In the Create Automatic Snapshot Policy dialog box, click the **Disks without Policy Applied** tab.

    -   Find the disk to which the policy is applied, and then click **Apply Policy** in the **Actions** column.
    -   Optional. Select multiple disks, and then click **Apply Policy** at the bottom of the dialog box.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9689/155911646940228_en-US.png)

3.  To disable a snapshot policy, click the **Disks with Policy Applied** tab.

    -   Find the disk whose policy you want to disable, and then click **Disable Policy**.
    -   Optional. Select multiple disks, and then click **Disable Policy** at the bottom of the dialog box.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9689/155911646940229_en-US.png)


Related APIs:

-   To apply automatic snapshot policies, call [ApplyAutoSnapshotPolicy](../../../../reseller.en-US/API Reference/Snapshots/ApplyAutoSnapshotPolicy.md#).
-   To disable automatic snapshot policies, call [CancelAutoSnapshotPolicy](../../../../reseller.en-US/API Reference/Snapshots/CancelAutoSnapshotPolicy.md#).

## Step 5: \(Optional\) Delete the automatic snapshot when releasing a disk {#section_jdf_rwy_ngb .section}

1.  In the left-side navigation pane, choose **Block Storage** \> **Disks**.
2.  Find the target disk, and then choose **More** \> **Modify Attributes** in the **Actions** column.
3.  In the **Modify Disk Type** dialog box, select **Delete Automatic Snapshots While Releasing Disk**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9689/155911646940230_en-US.png)

    **Note:** Even if you clear **Delete Automatic Snapshots While Releasing Disk**, automatic snapshots will be still stored for the retention days set by the policy. However, you can modify the automatic snapshot policy as needed.


Related API: [ModifyDiskAttribute](../../../../reseller.en-US/API Reference/Disk/ModifyDiskAttribute.md#).

## Step 6: \(Optional\) Disable an automatic snapshot policy {#section_ujq_pkp_wgb .section}

For more information, see [Delete snapshots or automatic snapshot policies](reseller.en-US/Snapshots/Use snapshots/Manage snapshots.md#section_ws4_mql_xdb).

## Step 7: \(Optional\) Delete an automatic snapshot policy {#section_tw1_4kp_wgb .section}

1.  In the left-side navigation pane, choose **Snapshots and Images** \> **Automatic Snapshot Policies**.
2.  Find the automatic snapshot policy to be deleted, and then click **Delete Automatic Snapshot Policy**.
3.  In the displayed dialog box, click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9689/155911646940231_en-US.png)


Related API: [DeleteAutoSnapshotPolicy](../../../../reseller.en-US/API Reference/Snapshots/DeleteAutoSnapshotPolicy.md#).

