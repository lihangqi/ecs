# Create an automatic snapshot policy {#task_1443510 .task}

This topic describes how to create an automatic snapshot policy in the ECS console.

The snapshot feature has been enabled. For more information, see [Activate ECS Snapshot](intl.en-US/Snapshots/Use snapshots/Activate ECS Snapshot.md#).

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).
2.  In the left-side navigation pane, choose **Storage & Snapshots** \> **Snapshots**.
3.  In the top navigation bar, select a region.
4.  On the **Snapshots** page, click the **Automatic Snapshot Policies** tab.
5.  In the upper-right corner of the Automatic Snapshot Policies page, click **Create Policy**.
6.  In the Create Policy dialog box that appears, configure the following parameters as prompted. 

    -   **Name**: specifies the policy name.
    -   **Executed At**: Select one or more points in time from 00:00 to 23:00.

        **Note:** Creating a snapshot may temporarily reduce the I/O performance of a block storage device by about 10%. We recommend that you create snapshots during off-peak hours.

    -   **Execution Frequency**: Select one or more days of the week.
    -   **Keep Snapshots**: specifies the number of days to retain the snapshot. Valid values: 1 to 65,536. Default value: 30. If you select **Always Keep** and the maximum number of snapshots is reached, the system will delete the earliest automatic snapshot.
    ![Create Policy](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1148290/156591996553896_en-US.png)

7.  Click **OK**.

We recommend that you specify cloud disks to execute an automatic snapshot policy immediately after the policy is created. Click **Apply Policy** in the Actions column corresponding to the new policy to go to the Create Automatic Snapshot Policy page. For more information, see [Apply or disable an automatic snapshot policy](intl.en-US/Snapshots/Automatic snapshot policies/Apply or disable an automatic snapshot policy.md#).

**More information**  


[../DNA0011860945/EN-US\_TP\_9906.md\#](../intl.en-US/API Reference/Snapshots/CreateAutoSnapshotPolicy.md#)

