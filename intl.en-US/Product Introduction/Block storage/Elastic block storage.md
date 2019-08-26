# Elastic block storage {#concept_n1s_rzb_wdb .concept}

Elastic block storage is a low-latency, persistent, and high-reliability random block-level data storage service provided by Alibaba Cloud to ECS users. It uses a [triplicate distributed system](intl.en-US/Product Introduction/Block storage/Triplicate technology.md#) to provide 99.9999999% data reliability for ECS instances. Elastic block storage supports the automatic copying of your data within the zone. It prevents unexpected hardware faults from causing data unavailability and protects your service against the threat of component faults.  Like what you can do with a hard disk, you can partition the elastic block storage attached to an ECS instance, create a file system, and store data on it.

You can expand your elastic block storage as needed at any time.  For more information, see [Linux \_ Resize a data disk](../../../../intl.en-US/User Guide/Cloud disks/Resize cloud disks/Linux _ Resize a data disk.md#) or  [Increase system disk size](../../../../intl.en-US/User Guide/Cloud disks/Resize cloud disks/Increase system disk size.md#). You can also create snapshots to back up data for the elastic block storage. For more information about snapshots, see [Snapshots](intl.en-US/Product Introduction/Snapshots/What are ECS snapshots.md#).

Based on whether it can be attached to multiple ECS instances, the elastic block storage can be divided into:

-   Cloud disks: A cloud disk can be attached to only one ECS instance in the same zone of the same region.
-   Shared Block Storage: Shared Block Storage can be attached to up to 8 ECS instances in the same zone of the same region.

    **Note:** The service is currently in public beta, during which the Shared Block Storage can be attached to a maximum of eight ECS instances.


## Cloud disks {#section_qjn_qbw_ydb .section}

Based on performance, cloud disks can be divided into:

-   SSD Cloud Disk: It adopts SSD \(Solid-state drive\) as a storage medium to deliver stable and high-performance storage with high random I/O and high data reliability.
-   Ultra Cloud Disk: It adopts the hybrid media of SSD and HDD \(Hard disk drive\) as a storage media.
-   Basic Cloud Disk: It adopts HDD as a storage medium.

Cloud disks can be used as:

-   System disks: They have the same lifecycle as the ECS instance where it is attached to. It is created and released along with the instance. Shared access is not allowed. The available size range of a single system disk varies according to the image:
    -   Linux \(excluding CoreOS\) and FreeBSD: 20 GiB−500 GiB
    -   CoreOS: 30 GiB−500 GiB
    -   Windows: 40 GiB−500 GiB
-   Data disks: They can be [created separately](../../../../intl.en-US/User Guide/Cloud disks/Create a cloud disk.md#) or jointly with ECS instances. Shared access is not allowed. The data disk created with an ECS instance has the same lifecycle as the instance, and is created and released along with the instance. Separately created data disks can be [released independently](../../../../intl.en-US/User Guide/Cloud disks/Release a cloud disk.md#) or with ECS instances.

When used as data disks, cloud disks share the data disk quota with Shared Block Storage, that is, up to 16 data disks can be attached to one ECS instance.

## Shared Block Storage {#section_gnz_nbw_ydb .section}

The Shared Block Storage is a block-level data storage service with high level of concurrency, performance, and reliability. It supports concurrent reads/writes to multiple ECS instances. It delivers the data reliability of up to 99.9999999%. Shared Block Storage can be attached to a maximum of 8 ECS instances. This service is currently in public beta, during which the Shared Block Storage can be attached to a maximum of four ECS instances.

Shared Block Storage can only be used as data disks and can only be created separately. Shared access is allowed. You can set the Shared Block Storage to release with the ECS instances.

Based on different performance, the Shared Block Storage can be divided into:

-   SSD Shared Block Storage: It adopts SSD as the storage medium to provide stable and high-performance storage with enhanced random I/O and data reliability.
-   Ultra Shared Block Storage: It adopts the hybrid media of SSD and HDD as the storage media.

When used as data disks, Shared Block Storage shares the data disk quota with cloud disks, that is, up to 16 data disks can be attached to one ECS instance.

For more information, see [FAQ about Shared Block Storage](https://www.alibabacloud.com/help/doc-detail/53820.htm).

## Billing {#section_inz_nbw_ydb .section}

The Shared Block Storage is currently in public beta, during which it is free of charge.

The billing method of a cloud disk depends on how it is created:

-   For cloud disks created with Subscription \(monthly or yearly subscription\) instances, upfront payment is required for the service to be ready for use. For more information, see [Subscription](../../../../intl.en-US/Pricing/Subscription.md#).
-   For cloud disks created jointly with Pay-As-You-Go instances or separately created are billed on a Pay-As-You-Go basis. For more information, see [Pay-As-You-Go](../../../../intl.en-US/Pricing/Pay-As-You-Go.md#).

You can change the billing method of a cloud disk, as shown in the following table.

|Conversion of billing methods|Features|Effective date|Suitable for|
|Subscription —\> Pay-As-You-Go|[Renew and downgrade configurations](../../../../intl.en-US/Pricing/Renew instances/Renew for configuration downgrade.md#)|Effective from the next billing cycle|Subscription cloud disks attached to Subscription instances.  The billing method of the system disk cannot be changed.|
|Pay-As-You-Go —\> Subscription|[Upgrade configurations](../../../../intl.en-US/User Guide/Instances/Change configurations/Upgrade configurations of Subscription instances.md#)|Effective immediately|Pay-As-You-Go data disks attached to Subscription instances. The billing method of the system disk cannot be changed.|
|[Switch from Pay-As-You-Go to subscription](../../../../intl.en-US/Pricing/Switch from Pay-As-You-Go to subscription.md#)|The system disks and data disks attached to the Pay-As-You-Go instances.|

## Related operations {#section_mnz_nbw_ydb .section}

You can perform one of the following operations on an elastic block storage:

-   If [an elastic block storage device is created separately as a data disk](../../../../intl.en-US/User Guide/Cloud disks/Create a cloud disk.md#), you must [attach the device to an instance](../../../../intl.en-US/User Guide/Cloud disks/Attach a cloud disk.md#) in the console, and then connect to the ECS instance to [partition and format the data disk](../../../../intl.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Linux _ Format and mount a data disk.md#).
-   If you want to encrypt the data on elastic block storage, [encrypt the storage](intl.en-US/Product Introduction/Block storage/ECS disk encryption.md#).
-   If your data disk capacity is insufficient, you can [resize the data disk](../../../../intl.en-US/User Guide/Cloud disks/Resize cloud disks/Linux _ Resize a data disk.md#).
-   If you want to change the operating system, you have to change the system disk.
-   If you want to back up the data of the elastic block storage, you can [manually create snapshots for the elastic block storage](../../../../intl.en-US/User Guide/Snapshots/Create snapshots.md#) or [apply an automatic snapshot policy to it](../../../../intl.en-US/User Guide/Snapshots/Apply automatic snapshot policies to disks.md#) to automatically create snapshots on schedule.
-   If you want to use the operating system and data environment information of one instance on another instance, you can [create a custom image by using the system disk snapshots of the former](../../../../intl.en-US/User Guide/Images/Create custom image/Create a custom mirror using a snapshot.md#).
-   If you want to restore the elastic block storage to the status when the snapshot is created, you can [roll back the disk](../../../../intl.en-US/User Guide/Cloud disks/Roll back a cloud disk.md#) by using its snapshot.
-   If you want to restore the elastic block storage to the status when it is created, you can [reinitialize the disk](../../../../intl.en-US/User Guide/Cloud disks/Reinitialize a cloud disk.md#).
-   If you do not need the elastic block storage, you can [detach](../../../../intl.en-US/User Guide/Cloud disks/Detach a cloud disk.md#) and [release it](../../../../intl.en-US/User Guide/Cloud disks/Release a cloud disk.md#). 

For more information about the operations on cloud disks, see the [Cloud disks](../../../../intl.en-US/User Guide/Cloud disks/Create a cloud disk.md#) section in the User Guide.

