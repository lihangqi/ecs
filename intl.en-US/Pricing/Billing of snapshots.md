# Billing of snapshots {#concept_rq2_pcx_ydb .concept}

The snapshot service provided by Alibaba Cloud ECS supports the Pay-As-You-Go billing method.

## Pay-As-You-Go {#section_w2v_pgy_pfb .section}

The snapshot fee is charged based on the size of the storage space used by a snapshot and the storage duration. Alibaba Cloud charges the snapshot fee as follows:

Charge of a snapshot = Snapshot size × Storage duration × Unit price

-   Snapshot size: the billing item of the snapshot service. The unit is GiB.

    The snapshot size can be defined as the storage used by the current snapshot subtracted by the storage used by the previous snapshot. Alibaba Cloud can identify disk space in which no data has been written and mark it as an empty block to save your snapshot space. Therefore, the size of a single incremental snapshot is less than the size of the corresponding disk. For more information, see [Snapshot concepts](../reseller.en-US/Snapshots/Snapshot concepts.md#).

-   Storage duration

    The number of hours from the time at which a snapshot is created to the time that the snapshot is deleted. The unit is hour. Similar to other Pay-As-You-Go resources, Alibaba Cloud updates the billing data and charges for Pay-As-You-Go snapshots on an hourly basis. The minimum chargeable storage duration is one hour. That is, periods of time that are less than an hour are billed as an hour.

-   Unit price

    The unit price of Pay-As-You-Go snapshots is consistent with the unit price of OSS standard storage. The unit price is given in the following unit: USD/GiB/month. For a comprehensive price list of various Alibaba Cloud regions, see the **Pricing** tab page of the ECS product details page.


## Overdue payment {#section_plm_hrv_rpf .section}

If you have an overdue payment, the snapshot service is suspended 24 hours later.

Within the first 15 days, all your snapshots are retained but you cannot create snapshots. Automatic snapshots with a retention duration shorter than 15 days will be deleted after they expire.

Fifteen days after the overdue payment, only snapshots that were used to create disks or custom images are retained.

**Note:** The system sends you a reminder via a short message or an email in advance if your account balance is less than the bill for the previous billing cycle.

## References {#section_hgr_g1f_5c9 .section}

-   [Snapshot overview](../reseller.en-US/Snapshots/Snapshot overview.md#)
-   [Reduce snapshot fees](../reseller.en-US/Snapshots/Use snapshots/Reduce snapshot fees.md#)
-   [Snapshot FAQ](../reseller.en-US/Snapshots/FAQ/Snapshot FAQ.md#)

