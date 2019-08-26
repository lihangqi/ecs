# Configure automatic snapshot policies {#concept_d35_r2w_wdb .concept}

A snapshot is a copy of the data of an ECS instance at a specified point in time. A snapshot can be used to back up data and create custom images.

## Time settings {#section_yzd_gfw_wdb .section}

Each account can create up to 100 automatic snapshot policies in a region. For more information about how to create automatic snapshot policies, see [Apply or disable an automatic snapshot policy](../../../../intl.en-US/Snapshots/Automatic snapshot policies/Apply or disable an automatic snapshot policy.md#). You can set the following time-related parameters for an automatic snapshot policy:

-   Executed At: Specify the hours of the day to create snapshots. Valid values: 00:00 to 23:00.
-   Execution Frequency: Specify the days of the week to create snapshots. Valid values: Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, and Sunday.
-   Keep Snapshots: Specify the period of time to retain snapshots. Snapshots can be retained permanently or for a specified period of time \(1 to 65,536 days\). The default retention period is 30 days.

## Time when snapshots are created {#section_vn5_nxz_jfb .section}

Automatic snapshots are created at the time specified in the automatic snapshot policy. Creating snapshots may degrade the I/O performance of a disk for a short period of time. When you set the Executed At and Execution Frequency parameters, we recommend that you avoid traffic peak periods based on characteristics of your business to ensure normal service running.

## Retention period {#section_uxx_4xz_jfb .section}

You can set the snapshot retention period based on business characteristics and the data update cycle. The snapshot retention period and the number of snapshots are mutually related. If the snapshot quota is exhausted, the earliest automatic snapshot is deleted.

## Snapshot costs {#section_c12_gfw_wdb .section}

Snapshots are charged based on the storage space they occupy. As more snapshots are stored, a larger storage space is occupied, increasing the cost. For more information about how to reduce snapshot costs, see [Reduce snapshot fees](../../../../intl.en-US/Snapshots/Use snapshots/Reduce snapshot fees.md#).

## Related topics {#section_cfa_tca_d08 .section}

This topic only applies to automatic snapshot policies. You can also manually create snapshots at any time. For more information, see [Create a snapshot](../../../../intl.en-US/Snapshots/Use snapshots/Create a snapshot.md#). Manually created snapshots are retained continuously. If you no longer require a manually created snapshot, you need to manually delete it.

