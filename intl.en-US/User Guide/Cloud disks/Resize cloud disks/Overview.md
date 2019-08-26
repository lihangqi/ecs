# Overview {#concept_e1g_44g_ydb .concept}

Depending on the disk type, you can resize a disk as follows:

-   For a system disk: **Change System Disk**
-   For a data disk: **Resize Disk**

## Limitations {#section_whc_q4g_ydb .section}

Limitations of resizing disks vary between system disks and data disks.

## System disks {#section_xhc_q4g_ydb .section}

The **Change system disk** feature allows you to increase the disk size only. The size limit for disk resizing is determined by the image and the current size of the system disk, as displayed in the following table.

|Image|Size limit \(GiB\)|
|:----|:-----------------|
|Linux \(excluding CoreOS\) and FreeBSD|20-500|
|CoreOS|30-500|
|Windows|40-500|

## Data disk {#section_zhc_q4g_ydb .section}

The **Resize Disk** feature allows you to increase the disk size only. The following table lists the capacity limits of different data disk typics after resizing, which is determined by the cloud disk types.

|Cloud disk type|Current capacity|Capacity after resizing|
|:--------------|:---------------|:----------------------|
|Basic Cloud Disk |Any|2,000 GiB|
|SSD Cloud Disk or Ultra Cloud Disk|equal or less than 2,048 GiB|2,048 GiB|
|SSD Cloud Disk or Ultra Cloud Disk|\> 2,048 GiB|Cannot be resized|
|ESSD Cloud Disk|Any|32,768 GiB|

## Additional operations {#section_d3c_q4g_ydb .section}

-   To increase the size of the system disk of an ECS instance, see [increase system disk size](reseller.en-US/User Guide/Cloud disks/Resize cloud disks/Increase system disk size.md#).
-   To resize a data disk attached to a Windows instance, see [Windows \_ Resize a data disk](reseller.en-US/User Guide/Cloud disks/Resize cloud disks/Windows _ Resize a data disk.md#).
-   To resize a data disk attached to a Linux instance, see [Linux \_ Resize a data disk](reseller.en-US/User Guide/Cloud disks/Resize cloud disks/Linux _ Resize a data disk.md#).

