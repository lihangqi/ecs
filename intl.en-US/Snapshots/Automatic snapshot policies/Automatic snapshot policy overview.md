# Automatic snapshot policy overview {#concept_1443642 .concept}

Automatic snapshot policies allow snapshots to be created regularly. These policies can be applied to both system disks and data disks. Automatic snapshot policies improve data security and operation error tolerance.

## Scenarios {#section_igl_737_5q0 .section}

Automatic snapshot policies allow snapshots to be created regularly at the scheduled time. These policies can protect disk data and improve system security and operation error tolerance. When your applications such as personal website or databases deployed on an ECS instance encounter security attacks or system vulnerabilities, you may not be able to manually create snapshots. In these cases, you can then use the most recent automatic snapshot to roll back affected cloud disks and reduce losses.

You can also specify an automatic snapshot policy to create snapshots before regular system maintenance tasks. This eliminates the need to manually create snapshots and ensure that snapshots are not forgotten to be created.

## Limits {#section_0sc_aqe_i98 .section}

Note the following points when you use automatic snapshot policies:

-   An account can have up to 100 automatic snapshot policies in a single region.
-   When the maximum number of snapshots is reached, the earliest automatic snapshot will be deleted automatically. This does not apply to manual snapshots.
-   Modifying the snapshot retention period of an automatic snapshot policy will only affect new snapshots created after the modification. The retention period of existing snapshots will not be modified.
-   You cannot create manual snapshots while an automatic snapshot is being created. You must wait until after the automatic snapshot has been created.
-   You can only apply automatic snapshot policies to cloud disks that are in the **In Use** state.
-   Automatic snapshot policies cannot be applied to local disks.

## Related operations {#section_ng7_tqw_xb3 .section}

-   [Create an automatic snapshot policy](reseller.en-US/Snapshots/Automatic snapshot policies/Create an automatic snapshot policy.md#)
-   [Apply or disable an automatic snapshot policy](reseller.en-US/Snapshots/Automatic snapshot policies/Apply or disable an automatic snapshot policy.md#)
-   [Delete automatic snapshots when releasing a disk](reseller.en-US/Snapshots/Automatic snapshot policies/Delete automatic snapshots when releasing a disk.md#)
-   [Modify an automatic snapshot policy](reseller.en-US/Snapshots/Automatic snapshot policies/Modify an automatic snapshot policy.md#)
-   [Delete an automatic snapshot policy](reseller.en-US/Snapshots/Automatic snapshot policies/Delete an automatic snapshot policy.md#)

## Related APIs {#section_j19_fm9_2x2 .section}

-   [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9906.md\#](../../../../reseller.en-US/API Reference/Snapshots/CreateAutoSnapshotPolicy.md#)
-   [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9907.md\#](../../../../reseller.en-US/API Reference/Snapshots/ApplyAutoSnapshotPolicy.md#)
-   [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9909.md\#](../../../../reseller.en-US/API Reference/Snapshots/CancelAutoSnapshotPolicy.md#)
-   [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9910.md\#](../../../../reseller.en-US/API Reference/Snapshots/DeleteAutoSnapshotPolicy.md#)
-   [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9911.md\#](../../../../reseller.en-US/API Reference/Snapshots/DescribeAutoSnapshotPolicyEX.md#)
-   [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9914.md\#](../../../../reseller.en-US/API Reference/Snapshots/ModifyAutoSnapshotPolicyEx.md#)

