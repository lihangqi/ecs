# ECS Snapshot 2.0 {#concept_f3f_nbx_ydb .concept}

The ECS Snapshot 2.0 data backup service provides a higher snapshot quota and more flexible automatic task policies than previous Alibaba Cloud snapshot services, further reducing its impact on the storage I/O performance.

## Comparison of specifications {#section_wjd_hdy_pfb .section}

**Note:** Disks in this topic refer to Cloud disks and Shared Block Storage. For more information, see [Cloud disks and Shared Block Storage](reseller.en-US/Product Introduction/Block storage/Cloud disks and Shared Block Storage.md#).

|Feature|Original snapshot specification|Snapshot 2.0 specifications|Benefit|Example|
|:------|:------------------------------|:--------------------------|:------|:------|
|Snapshot quota|\(Number of disks + 1\) × 6|64 snapshots for each disk|Longer protection cycle and finer protection granularity| -   The snapshot backup of a data disk for non-core businesses occurs at 00:00 every day. This backup data is retained for over 2 months.

-   The snapshot backup of a data disk for core businesses occurs every 4 hours. This backup data is retained for over 10 days.


 |
|Automatic snapshot policy|Hardcoded, triggered once daily, and unmodifiable|Can be customized for day of week and time of day snapshot creation, and for snapshot retention period. You can also query the disk quantity and details associated with an automatic snapshot policy.|More flexible protection policy| -   You can take snapshots on the hour, several times a day.

-   You can select any day of the week as the recurring day for snapshot creation.

-   You can specify a snapshot retention period or retain snapshots indefinitely. When the maximum number of automatic snapshots has been reached, the oldest automatic snapshot will be deleted.


 |
|Implementation principle|Copy-on-write \(COW\)|Redirect-on-write \(ROW\)|Mitigates impact of the snapshot task on storage I/O performance|The implementation is invisible to users, allowing snapshots to be taken at any time without affecting user experience.|

## Technical comparison {#section_zlh_bdy_pfb .section}

Compared with the snapshot features of traditional storage products, ECS Snapshot 2.0 has the following advantages:

|Item|ECS Snapshot 2.0|Snapshot feature of traditional storage products|
|:---|:---------------|:-----------------------------------------------|
|Capacity|Unlimited capacity, meeting the data protection needs of enterprise-level businesses.|Capacity limited by the purchased storage devices, meeting only the data protection needs of core business structures.|
|Scalability|Auto scale in one click to meet on-demand business scaling requirements.|Poor scalability, restricted by such factors as the production and storage performance, available capacity, and vendor support capabilities. Scaling typically takes 1 to 2 weeks.|
|TCO|Free.|Large upfront investment required, typically for software licenses, reserved space, and upgrade and maintenance expenses.|
|Usability|24 × 7 after-sales support \(available in multiple languages\).|Complicated operations, greatly restricted by vendor support capabilities.|

