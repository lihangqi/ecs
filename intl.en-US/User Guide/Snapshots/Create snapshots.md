# Create snapshots {#concept_eps_gbl_xdb .concept}

You can create instance snapshots to save the system state from a certain point in time for data backup or to create images.

**Note:** 

-   Creation of the first snapshot will take relatively longer than subsequent snapshots due to the first snapshot being a full snapshot. However, depending on the amount of changed data since previous snapshots, the length of time for each snapshot creation may vary.
-   Creating snapshots of a disk may reduce disk performance.
-   We recommended that you not create snapshots during peak traffic hours.
-   Manually created snapshots, unlike automatic snapshots, are retained until they are manually deleted.

## Procedure {#section_pdn_xdl_xdb .section}

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/#/home).
2.  Select a region. In the left-side navigation pane, click Instances, and click **Manage**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9687/15353522684545_en-US.png)

3.  In the left-side navigation pane, click  **Instance Disks**, and click **Create Snapshot** for the target disk. You can select only one disk at a time, either system disk or data disk.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9687/15353522694530_en-US.png)

4.  Enter the name for the snapshot, and click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9687/15353522694550_en-US.png)

5.  To view the snapshots, click **Instance Snapshots** from the left-side navigation pane. You can see the progress and status of the snapshot.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9687/15353522694552_en-US.png)


