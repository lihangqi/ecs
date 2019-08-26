# Cloud disks and Shared Block Storage {#concept_n1s_rzb_wdb .concept}

Cloud disks and Shared Block Storage are block-level data storage products provided by Alibaba Cloud for ECS that features low latency, high performance, persistence, and high reliability. They use a [triplicate distributed system](reseller.en-US/Block Storage/Block storage/Triplicate technology.md#) to provide 99.9999999% data reliability for ECS instances. Cloud disks and Shared Block Storage can automatically copy your data within the target zone to help you prevent unexpected hardware faults from causing data unavailability or service disruption. Just like what you do with a hard disk, you can partition and format the cloud disks and Shared Block Storage attached to an ECS instance, create a file system, and store data on them.

You can expand the cloud disks and Shared Block Storage as needed at any time. For more information, see [Linux - Resize a data disk](reseller.en-US/Block Storage/Block storage/Resize cloud disks/Extend the file system of a Linux data disk.md#) and [increase system disk size](reseller.en-US/Block Storage/Block storage/Resize cloud disks/Resize a cloud disk.md#). You can also create snapshots to back up data for the cloud disks and Shared Block Storage. For more information about snapshots, see [what are ECS snapshots](reseller.en-US/Snapshots/Snapshot overview.md#).

Cloud disks and Shared Block Storage differ in whether they can be simultaneously attached to multiple ECS instances and perform read and write operations. Details are as follows:

-   Cloud disks can be attached to only one ECS instance in the same zone of the same region.
-   Shared Block Storage devices can be mounted to a maximum of eight ECS instances in the same zone of the same region.

    **Note:** Shared Block Storage is currently in public beta phase. You can open a ticket to submit your application for beta testing.


## Cloud disks {#cloudDisk .section}

-   **Performance-based category**

    -   ESSD cloud disks: ESSD is an ultra-high-performance cloud product based on the next generation distributed block storage architecture. ESSD combines 25 GE networks with RDMA technology, offering the capability of up to 1 million random read/write operations and a shorter single-link latency. ESSD is currently in public beta phase. For more information, see [FAQ about ESSD cloud disks](https://partners-intl.aliyun.com/help/faq-detail/64950.htm).
    -   SSD cloud disks: high-performance disks with stable and high random I/O performance and high data reliability
    -   Ultra cloud disks: with high cost performance, medium random I/O performance, and high data reliability
    -   Basic cloud disks: with high data reliability and general random I/O performance
-   **Function-based category**

    -   System disks: have the same life cycle as the ECS instance to which it is mounted. A system disk is created and released at the same time as the instance. Shared access is not allowed. The available size range of a single system disk varies according to the image, as follows:
        -   Linux \(excluding CoreOS\) and FreeBSD: 20−500 GiB
        -   CoreOS: 30−500 GiB
        -   Windows: 40−500 GiB
    -   Data disks: can be [created separately](reseller.en-US/Block Storage/Block storage/Create a cloud disk/Create a cloud disk.md#) or at the same time as ECS instances. If the release with instance attribute is set to a data disk, it has the same life cycle as the instance to which it is attached, and is released along with the instance. Data disks created separately can be [released independently](reseller.en-US/Block Storage/Block storage/Release a cloud disk.md#) or at the same time as the corresponding ECS instances. Shared access is not allowed. The performance of data disks depends on the cloud disk type. For more information, see [storage parameters and performance test](reseller.en-US/Block Storage/Storage parameters and performance tests.md#).
    When used as data disks, up to 16 cloud disks can be attached to one ECS instance.


## Shared Block Storage {#sharedBlock .section}

Shared Block Storage is a block-level data storage service with strong concurrency, high performance, and high reliability. It supports concurrent reads from and writes to multiple ECS instances, and provides data reliability of up to 99.9999999%. Shared Block Storage can be mounted to a maximum of 8 ECS instances.

Shared Block Storage can only be used as data disks and can only be created separately. Shared access is allowed. You can set the Shared Block Storage device to be released when the ECS instances are released.

Shared Block Storage can be divided into:

-   SSD Shared Block Storage, which uses SSD as the storage medium to provide stable and high-performance storage with enhanced random I/O and data reliability.
-   Ultra Shared Block Storage, which uses the hybrid media of SSD and HDD as the storage media.

When used as data disks, Shared Block Storage allows up to 16 data disks to be attached to each ECS instance.

For more information, see [FAQ about Shared Block Storage](https://partners-intl.aliyun.com/help/doc-detail/53820.htm).

## Billing {#section_inz_nbw_ydb .section}

Shared Block Storage is currently in public beta phase free of charge.

The billing method of a cloud disk depends on how it is created:

-   Cloud disks created with Subscription instances are billed before the service is ready for use. For more information, see [Subscription](../../../../reseller.en-US/Pricing/Subscription.md#).
-   Cloud disks created at the same time as Pay-As-You-Go instances, or created separately, are billed on a Pay-As-You-Go basis. For more information, see [Pay-As-You-Go](../../../../reseller.en-US/Pricing/Pay-As-You-Go.md#).

You can change the billing method of the cloud disk, as shown in the following table.

|Conversion of billing methods|Feature|Effective time|Suitable for|
|:----------------------------|:------|:-------------|:-----------|
|Subscription -\> Pay-As-You-Go|[Renew for configuration downgrade](../../../../reseller.en-US/Pricing/Renew instances/Renew for configuration downgrade.md#)|Effective from the next billing cycle|Subscription cloud disks mounted to Subscription instances. The billing method of the system disk cannot be changed.|
|Pay-As-You-Go -\> Subscription|[Upgrade configurations](reseller.en-US/Instances/Change configurations/Upgrade configurations/Upgrade configurations of Subscription instances.md#)|Effective immediately|Pay-As-You-Go data disks mounted to Subscription instances. The billing method of the system disk cannot be changed.|
|[Switch from Pay-As-You-Go to Subscription billing](../../../../reseller.en-US/Pricing/Switch from Pay-As-You-Go to Subscription billing.md#)|System disks and data disks mounted to Pay-As-You-Go instances.|

## Related operations {#section_mnz_nbw_ydb .section}

You can perform the following operations on cloud disks:

-   If [a cloud disk or Shared Block Storage device is created separately from a data disk](reseller.en-US/Block Storage/Block storage/Create a cloud disk/Create a cloud disk.md#), you must [attach a cloud disk](reseller.en-US/Block Storage/Block storage/Attach a cloud disk.md#) in the ECS console, and then connect to the ECS instance to [partition and format the data disk](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk of a Linux instance.md#).
-   If you want to encrypt the data on a cloud disk, [encrypt the disk](reseller.en-US/Block Storage/Block storage/ECS disk encryption.md#).
-   If your system disk capacity is insufficient, you can [increase system disk size](reseller.en-US/Block Storage/Block storage/Resize cloud disks/Resize a cloud disk.md#).
-   If you want to expand the data disk capacity, you can [resize the data disk](reseller.en-US/Block Storage/Block storage/Resize cloud disks/Extend the file system of a Linux data disk.md#).
-   If you want to change the OS, you can [change the system disk](reseller.en-US/Block Storage/Block storage/Change the operating system/Replace the system disk (public image).md#).
-   If you want to back up the data of a cloud disk or Shared Block Storage device, you can [manually create snapshots for the cloud disk or Shared Block Storage](reseller.en-US/Snapshots/Use snapshots/Create a snapshot.md#) or [apply an automatic snapshot policy to it](reseller.en-US/Snapshots/Use snapshots/Apply automatic snapshot policies to disks.md#) to automatically create snapshots on schedule.
-   If you want to use the OS and data environment information of one instance on another instance, you can [create a customized image using the system disk snapshots of the latter instance](reseller.en-US/Images/Custom image/Create custom image/Create a custom image by using a snapshot.md#).
-   If you want to restore a cloud disk or Shared Block Storage device to the status when the snapshot is created, you can [roll back a cloud disk](reseller.en-US/Block Storage/Block storage/Roll back a cloud disk.md#) using its snapshot.
-   If you want to restore a cloud disk to its status at the time of creation, you can [reinitialize a cloud disk](reseller.en-US/Block Storage/Block storage/Reinitialize a cloud disk.md#).
-   If you do not need a cloud disk or Shared Block Storage device, you can [detach a cloud disk](reseller.en-US/Block Storage/Block storage/Detach a cloud disk.md#) and [release a cloud disk](reseller.en-US/Block Storage/Block storage/Release a cloud disk.md#).
-   If you no longer need a Subscription billed cloud disk, you can [convert the billing methods of cloud disks](reseller.en-US/Block Storage/Block storage/Convert the billing methods of cloud disks.md#), and then [detach a cloud disk](reseller.en-US/Block Storage/Block storage/Detach a cloud disk.md#) and [release a cloud disk](reseller.en-US/Block Storage/Block storage/Release a cloud disk.md#).

For more information about operations on cloud disks, see [cloud disks](reseller.en-US/Block Storage/Block storage/Create a cloud disk/Create a cloud disk.md#) in *User Guide* .

