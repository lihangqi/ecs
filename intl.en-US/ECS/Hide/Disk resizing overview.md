# Disk resizing overview {#concept_e1g_44g_ydb .concept}

In Alibaba Cloud, you can resize the disk volume of a system disk or a data disk at any time.

## Scenarios {#section_ilv_yg2_2hb .section}

You can resize the volume of a disk to meet the needs of different scenarios, including the need to:

-   [Increase the disk size](intl.en-US/ECS/ECS conref warehouse/Resize a cloud disk online.md#). You can extend the existing partitions or newly added partitions.
-   [Create a cloud disk](../../../../intl.en-US/Block storage/Block storage/Create a cloud disk/Create a cloud disk.md#) and [attach the cloud disk](../../../../intl.en-US/Block storage/Block storage/Attach a cloud disk.md#) to the instance as a data disk. After, you need to [partition and format the cloud disk](../../../../intl.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk of a Linux instance.md#).
-   [Replace the system disk](../../../../intl.en-US/Block storage/Block storage/Change the operating system/Replace the system disk (public image).md#) and specify a higher system disk capacity.

## Procedures for disk resizing {#section_yvq_wg3_fhb .section}

The following table describes the process of how to resize a cloud disk based on its current status.

|**Cloud disk status**|Cloud disk that is not attached or partitioned|Cloud disk that is attached but is not partitioned|Cloud disk that is attached and partitioned|
|**Resizing procedure**| 1.  Use the ECS console or call the API action ResizeDisk to [resize the cloud disk](intl.en-US/ECS/ECS conref warehouse/Resize a cloud disk online.md#).
2.  Use the ECS console or call the API action AttachDisk to [attach the cloud disk](../../../../intl.en-US/Block storage/Block storage/Attach a cloud disk.md#).
3.  Partition and format the cloud disk:
    -   [Partition and format a Windows data disk less than 2 TiB](../../../../intl.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Windows instances.md#).
    -   [Partition and format a Linux data disk less than 2 TiB](../../../../intl.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk of a Linux instance.md#).
    -   [Partition and format a cloud disk greater than 2 TiB](../../../../intl.en-US/Block storage/Block storage/Format a data disk/Partition and format data disk more than 2 TiB.md#).

 | 1.  Use the ECS console or call the API action ResizeDisk to [resize the cloud disk](intl.en-US/Block storage/Block storage/Resize cloud disks/Resize a cloud disk offline.md#).
2.  Use the ECS console or call the API action RebootInstance to [restart the instance](../../../../intl.en-US/Instances/Manage instances/Restart an instance.md#).
3.  Partition and format the cloud disk:
    -   [Partition and format a Windows data disk less than 2 TiB](../../../../intl.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Windows instances.md#).
    -   [Partition and format a Linux data disk less than 2 TiB](../../../../intl.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk of a Linux instance.md#).
    -   [Partition and format a cloud disk greater than 2 TiB](../../../../intl.en-US/Block storage/Block storage/Format a data disk/Partition and format data disk more than 2 TiB.md#).

 | 1.  Use the ECS console or call the API action ResizeDisk to [resize the cloud disk](intl.en-US/ECS/ECS conref warehouse/Resize a cloud disk online.md#).
2.  Use the ECS console or call the API action RebootInstance to [restart the instance](../../../../intl.en-US/Instances/Manage instances/Restart an instance.md#).
3.  Extend the partitions of the attached system disk or data disk:
    -   [Extend a Windows file system](intl.en-US/ECS/ECS conref warehouse/Extend a Windows partition and file system.md#).
    -   [Extend a Linux file system](intl.en-US/ECS/ECS conref warehouse/Extend the file system of the Linux system disk.md#).
    -   [Extend the file system of a Linux data disk](intl.en-US/ECS/ECS conref warehouse/Extend the file system of a Linux data disk.md#).

 |

## Limits of resizing a system disk {#section_xhc_q4g_ydb .section}

When you resize a system disk, the new size of the system disk must be greater than its current size, but must be less than or equal to 500 GiB. The following table describes the limits of system disk resizing for different images.

|Image|Limit of system disk resizing \(GiB\)|
|:----|:------------------------------------|
|Linux \(excluding CoreOS\) + FreeBSD|\[max\{20, current size of the system disk\}, 500\]|
|CoreOS|\[max\{30, current size of the system disk\}, 500\]|
|Windows|\[max\{40, current size of the system disk\}, 500\]|

For example, if the system disk size of a CentOS instance is 35 GiB, it must be greater than 35 GiB and must be less than or equal to 500 GiB after being resized.

## Upper limit of data disk resizing {#section_hzp_wzv_42b .section}

After being resized, the new size of the data disk must be greater than its current size. The following table describes the upper limit of data disk resizing for different cloud disk.

|Cloud disk type|Current size \(GiB\)|Upper limit of data disk resizing \(GiB\)|
|:--------------|:-------------------|:----------------------------------------|
|Basic cloud disk|No limit|2000|
|SSD cloud disk or ultra disk|≤ 2048|2048|
|SSD cloud disk or ultra disk|\> 2048|N/A|
|ESSD cloud disk|No limit|32768|

