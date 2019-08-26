# Create and delete an automatic snapshot policy {#concept_smh_y2l_xdb .concept}

An automatic snapshot policy is a set of defined parameters for automatically creating snapshots.

**Note:** 

-   We recommend you set the automatic snapshot creation time and repeat date during off-peak business hours to avoid interruptions to your business services.
-   You can create a maximum of 100 automatic snapshot policies per region.

## Prerequisite {#section_odg_ffl_xdb .section}

You must have created an automatic snapshot policy.

## Procedure {#section_pdg_ffl_xdb .section}

To create an automatic snapshot policy, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Snapshots and Images** \> **Automatic Snapshot Policies**.
3.  On the Automatic Snapshot Policies page, perform the following action as required:
    -   If you want to create a policy, click **Create Policy** at the upper-right corner.
    -   If you want to modify a policy, find the policy that you want to modify, and click **Modify Policy** in the **Actions** column.
4.  In the Create Policy or Modify Policy dialog box, define the automatic snapshot policy as follows.
    -   Enter a policy name.
    -   Select a time after **Executed At** to specify the time of day for automatically creating snapshots.
    -   Specify the **Execution Frequency**.
    -   Set a number after **Keep Snapshots** to defines the number of days a snapshot can be retained. The value range is 1−65535 days, or permanently. By default, it is set to 30 days. You can also choose to permanently retain automatic snapshots.

        **Note:** When the number of snapshots reaches the limit, the system automatically removes the oldest automatic snapshots created. Manually created snapshots are not removed.

5.  Click **OK**.

## Additional operations {#section_udg_ffl_xdb .section}

You can [apply automatic snapshot policies to disks](reseller.en-US/User Guide/Snapshots/Apply automatic snapshot policies to disks.md#).

## Related APIs {#section_l1z_5hl_xdb .section}

-   [CreateAutoSnapshotPolicy](../../../../reseller.en-US/API Reference/Snapshots/CreateAutoSnapshotPolicy.md#): Creates automatic snapshot policies.
-   [DescribeAutoSnapshotPolicyEx](../../../../reseller.en-US/API Reference/Snapshots/DescribeAutoSnapshotPolicyEx.md#): Queries automatic snapshot policies.
-   [ModifyAutoSnapshotPolicyEx](../../../../reseller.en-US/API Reference/Snapshots/ModifyAutoSnapshotPolicyEx.md#): Modifies automatic snapshot policies.

