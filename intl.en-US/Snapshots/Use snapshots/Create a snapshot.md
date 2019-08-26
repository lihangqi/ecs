# Create a snapshot {#concept_eps_gbl_xdb .concept}

This topic describes how to create a snapshot. A snapshot is a copy of data on a disk at a specific point in time. Snapshots are commonly used to back up data and create custom images.

## Scenarios {#section_ewp_wyx_52b .section}

You can create a snapshot in data backup scenarios to eliminate the risk of data loss. Specifically, you can create a snapshot if you need to:

-   Modify critical system files.
-   Back up service data.
-   Recover mistakenly released instances.
-   Mitigate network attacks.
-   Change the operating system.
-   Provide data support for a production environment.

Additionally, you can use a snapshot to [create a custom image](../intl.en-US/Images/Custom image/Create custom image/Create a custom image by using a snapshot.md#) to quickly deploy an application environment for a large number of ECS instances.

## Limits {#section_azs_vyx_52b .section}

-   Snapshots are charged based on the storage resources you actually use. For more information, see [Billing of snapshots](../intl.en-US/Pricing/Billing of snapshots.md#).
-   Creating a snapshot may have a slight impact on disk performance and I/O speeds. We recommend that you create snapshots during off-peak hours.
-   A snapshot only records data at a specific point in time. Therefore, incremental data generated when the snapshot is created will not be synchronized to the snapshot.
-   To ensure that a snapshot is successfully created, we recommend that you do not modify the ECS instance status \(that is, stop or restart the instance\) when the snapshot is being created.
-   If you want to create a snapshot of an instance, the instance must be in the **Running** or **Stopped** state.
-   If you want to create a snapshot of a cloud disk, the disk must be in the **In Use** or **Expired** state.

    **Note:** A snapshot being created for a cloud disk in an **Expired** state will be released at the same time the cloud disk is released.

-   Manually created snapshots can only be manually deleted. Therefore, you need to delete unnecessary snapshots regularly to prevent these snapshots from incurring fees. For more information, see [Reduce snapshot fees](intl.en-US/Snapshots/Use snapshots/Reduce snapshot fees.md#).
-   If you create an extended volume by using a multi-partition single disk, the snapshot that you created can be used to [roll back the disk](intl.en-US/Block Storage/Block storage/Roll back a cloud disk.md#).
-   If you create a dynamic extended volume by using multiple disks and no I/O operation is performed on data in the volume, the snapshot that you created can be used to roll back the disk. If I/O operations are continuously performed in the extended volume, data consistency of the rolled-back disk is uncertain.

## Create a snapshot in the ECS console {#section_pdn_xdl_xdb .section}

To create a snapshot in the ECS console, follow these steps:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).
2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.
3.  Find the instance for which you want to create a snapshot, and then click **Manage** in the **Actions** column.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9687/156343753740369_en-US.png)

4.  In the left-side navigation pane, click **Disks**, find the target disk, and then click **Create Snapshot**.

    **Note:** You can select only one disk at a time. The **Type** can be a system disk or a data disk.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9687/156343753740370_en-US.png)

5.  Enter a name for the snapshot and click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9687/156343753840371_en-US.png)

6.  In the left-side navigation pane, click **Instance Snapshots**. The snapshot creation progress, estimated time remaining, and snapshot status are displayed.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9687/156343753840372_en-US.png)


You can also create a snapshot as indicated on the **Storage & Snapshots** \> **Disks** page.

## Create a snapshot by using an API {#section_rn1_hys_lgb .section}

The following procedure describes how to use Alibaba Cloud CLI to call API actions to create a snapshot. For more information, see [Quick start for ECS APIs](../intl.en-US/API Reference/Quick start for ECS APIs.md#).

1.  Obtain the instance ID.
    -   If you have remotely connected to an ECS instance, you can obtain the instance ID by using [metadata](../intl.en-US/Instances/Manage instances/User-defined data and metadata/Metadata.md#). For example, to query the ID of a Linux instance, run the following command:

        ``` {#codeblock_xl0_j50_x3d}
        curl http://100.100.100.200/2016-01-01/meta-data/instance-id
        ```

    -   In your local computer, you can obtain the instance ID by calling [DescribeInstances](../intl.en-US/API Reference/Instances/DescribeInstances.md#):

        ``` {#codeblock_wrr_zja_58e}
        aliyun ecs DescribeInstances --output cols=InstanceId,InstanceName
        ```

2.  Obtain the disk ID by calling the API [DescribeDisks](../intl.en-US/API Reference/Disk/DescribeDisks.md#):

    ``` {#codeblock_9da_1i3_dkb}
    aliyun ecs DescribeDisks --RegionId cn-hangzhou --InstanceId 'i-0xi1ioe********166cq' --output cols=DiskId
    ```

3.  Call [CreateSnapshot](../intl.en-US/API Reference/Snapshots/CreateSnapshot.md#) to create a snapshot based on the disk ID:

    ``` {#codeblock_je4_car_dmu}
    aliyun ecs CreateSnapshot --DiskId d-bp19pjyf12hebpXXXXXX
    ```

    The snapshot-creating task is initiated if the following information is returned:

    ``` {#codeblock_v13_uaa_v4e}
    {"RequestId":"16B856F6-EFFB-4397-8A8A-CB73FAXXXXXX","SnapshotId":"s-bp1afnc98r8kjhXXXXXX"}
    ```

4.  Call [DescribeSnapshots](../intl.en-US/API Reference/Snapshots/DescribeSnapshots.md#) to query the progress. When `"SnapshotId"="s-bp1afnc98r8kjhXXXXXX"` and `"Status":"accomplished"` are displayed, it means that the snapshot has been created.

    ``` {#codeblock_3cv_5y6_z49}
    aliyun ecs DescribeSnapshots --RegionId cn-hangzhou --InstanceId i-bp1afnc98r8k69XXXXXX --output cols=SnapshotId,Status
    ```


## Time required {#section_gvs_ydl_xdb .section}

The time required for creating a snapshot is dependent on the capacity of the disk.

Following the content covered in [Snapshot concepts](intl.en-US/Snapshots/Snapshot concepts.md#), the first disk snapshot is a full snapshot, and therefore its creation requires a relatively long period of time. In contrast, subsequent snapshots require shorter periods of time. The amount of time needed to create subsequent snapshots is dependent on the amount of data generated since the last snapshot. Generally, the greater the amount of data, the longer time it will take to create the snapshot.

## What to do next {#section_mx4_cyy_52b .section}

After you create a snapshot, you can:

-   [Roll back a cloud disk](intl.en-US/Block Storage/Block storage/Roll back a cloud disk.md#).
-   [Create a cloud disk by using the snapshot](intl.en-US/Block Storage/Block storage/Create a cloud disk/Create a cloud disk by using a snapshot.md#).
-   [Create a custom image by using the snapshot](intl.en-US/Images/Custom image/Create custom image/Create a custom image by using a snapshot.md#).

