# Apply automatic snapshot policies to disks {#concept_nyv_k3l_xdb .concept}

You can apply an automatic snapshot policy to disks according to your business needs.

Automatic snapshots are named in the format of auto\_yyyymmdd\_1, for example, auto\_20140418\_1.

**Note:** 

-   Creating snapshots may interrupt read/write operations on your disk. We recommend that you set the creation time of automatic snapshots during off-peak business hours to avoid interruptions to your business services.
-   Automatic snapshot policies cannot be applied to unused basic cloud disks.
-   Snapshots that are manually created do not conflict with automatic snapshots. However, if an automatic snapshot is being created on a disk, you must wait for it to finish before manually creating a snapshot.

You can apply an automatic snapshot policy to a disk using either of the following menus:

-   From the Cloud Disks menu. This method is suitable for applying an automatic snapshot policy to a specific disk.
-   From the Snapshots and Images menu. This method is suitable for applying a unified automatic snapshot policy to multiple disks.

## From the Cloud Disks menu {#section_yzf_tkl_xdb .section}

To apply an automatic snapshot policy through the Cloud Disks menu, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  Select the target region.
3.  In the left-side navigation pane, click **Disks**.
4.  Select the disk for which you want to execute the policy and click **Create Automatic Snapshot Policy**.
5.  Enable the automatic snapshot function and select the desired snapshot policy.
6.  Click **OK**.

## From the Snapshots and Images menu {#section_dm4_zkl_xdb .section}

To apply or disable an automatic snapshot policy, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  Select the target region. 
3.  In the left-side navigation pane, select **Snapshots and Images** \> **Automatic Snapshot Policies**. 
4.  Select the automatic snapshot policy that you want to apply and click **Apply Policy**.
5.  To enable an automatic snapshot policy, select **Disks without Policy Applied** to view the disks. Find the disk for which you want to enable the policy, and then click **Apply Policy** after it. Alternatively, if you select multiple disks, click **Apply Policy** at the lower-left corner.

    ![](images/4563_en-US.gif)

6.  To disable the automatic snapshot policy, select the **Disks with Policy Applied** tab to view the disks, select the disk for which you want to disable the policy, and then click **Disable Policy** at the right side. Note that if you select multiple disks, you need to click **Disable Policy** at the lower-left corner to disable the automatic snapshot policy for all selected disks.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9689/15432263184568_en-US.png)


