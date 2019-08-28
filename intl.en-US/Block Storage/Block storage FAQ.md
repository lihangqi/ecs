# Block storage FAQ {#concept_40551_zh .concept}

## What is an ESSD cloud disk? {#section_xbq_tfk_bgr .section}

An Enhanced SSD \(ESSD\) cloud disk is an ultra-high performance cloud disk provided by Alibaba Cloud. ESSD cloud disks are based on a 25 GE network and remote direct memory access \(RDMA\) technology. They deliver a maximum random IOPS of 1 million per disk and low one-way latency.

## When are ESSD cloud disks available for purchase? {#section_xjd_2lw_io9 .section}

ESSD cloud disks are commercially available from the end of July 2019 after a beta test started on July 14, 2018. You can log on to the ECS console or call [CreateDisk](../../../../reseller.en-US/API Reference/Disk/CreateDisk.md#) to create ESSD cloud disks.

## What is the difference of ESSD cloud disks before and after the beta test? {#section_sl2_l6u_igq .section}

The difference of ESSD cloud disks before and after the beta test lies in their specifications. After the beta test, ESSD cloud disks are commercially available in three specifications, as described in the following table.

For ESSD cloud disks, larger capacity means higher data-processing performance. The capacity, IOPS, and throughput provided by ESSD cloud disks vary depending on their performance levels \(PLs\), as described in the following table.

|PL|Capacity \(GiB\)|Maximum IOPS|Maximum throughput \(MBps\)|
|--|----------------|------------|---------------------------|
|PL1|10-32,768|50,000|350|
|PL2|461-32,768|100,000|750|
|PL3|1,261-32,768|1,000,000|4,000|

## What are the similarities and differences among ESSD, SSD, and Ultra cloud disks? {#section_f0a_bts_wrh .section}

ESSD, SSD, and Ultra cloud disks have the following similarities and differences:

-   Similarities: These three types of cloud disks are based on a distributed block storage architecture. They provide high reliability and scalability and support snapshots and data encryption.
-   Differences: Compared with SSD and Ultra cloud disk, ESSD cloud disks provide better performance. For more information, see [Block storage performance](reseller.en-US/Block Storage/Block storage performance.md#).

## How can I measure the performance level of an ESSD cloud disk? {#section_vln_3tg_q6l .section}

The performance level of an ESSD cloud disk positively correlates with its capacity. Specifically, larger capacity delivers higher performance.

## How can I test the performance of an ESSD cloud disk and obtain a 1 million IOPS result? {#section_dks_tw6_fsc .section}

We recommend that you use the FIO tool to test the performance of ESSD cloud disks. For more information, see [How can I test the performance of an ESSD disk](#).

## How is the performance of an ESSD cloud disk and storage performance of the corresponding instance related? {#section_l0c_cer_qu7 .section}

The storage performance of some instances positively correlates to the instance type level. That is, higher instance type levels directly correspond to higher IOPS and throughput numbers.

For example, after you create a g5se instance \(a storage-optimized ECS instance type family\) and mount ESSD cloud disks to it:

-   If the total storage performance of ESSD cloud disks does not exceed that of the instance, the storage performance of ESSD cloud disks takes precedence.

-   If the total storage performance of ESSD cloud disks exceeds that of the instance, the storage performance of the instance takes precedence.

    Assume that you created a 16 GiB ecs.g5se.xlarge instance that has a maximum IOPS of 60,000. If you mount an ESSD disk that has a capacity of 2 TiB \(for which the IOPS is 101,800\) to the instance, the maximum IOPS of the instance is 60,000, instead of 101,800.

    The performance specifications of instance types from g5se are described in the following table.


|Instance type|vCPU \(Core\)|Memory \(GiB\)|IOPS \(10 thousand\)|Throughput \(Mbit/s\)|
|:------------|:------------|:-------------|:-------------------|:--------------------|
|ecs.g5se.large|2|8|3|118|
|ecs.g5se.xlarge|4|16|6|235|
|ecs.g5se.2xlarge|8|32|12|470|
|ecs.g5se.4xlarge|16|64|23|900|
|ecs.g5se.6xlarge|24|96|34|1350|
|ecs.g5se.8xlarge|32|128|45|1800|
|ecs.g5se.16xlarge|64|256|90|3600|
|ecs.g5se.18xlarge|70|336|100|4000|

## In which regions and zones are ESSD cloud disks available? {#section_yq8_9fo_zgu .section}

Currently, ESSD cloud disks are available in the following regions and zones:

-   China North 2 Zone G
-   China North 3 Zone A
-   China East 2 Zone E and Zone F
-   China East 1 Zone H and Zone I
-   China South 1 Zone E

## **On what instance types can I mount ESSD cloud disks?** {#section_br8_0h3_7d6 .section}

Currently, ESSD cloud disks can be mounted to 25 GE network instance type families \(c5, ic5, g5, r5, and g5se\), ECS Bare Metal Instance type families \(ebmhfg5, ebmc4, and ebmg5\), and heterogeneous computing instance type families \(vgn5i, gn6i, gn6v, gn5, gn5i, gn4, ga1, f1, and f3\).

## What are the common operations that can be performed on a disk? {#section_tgb_55w_1pz .section}

The following topics describe common operations you can perform on a disk:

-   [../DNA0011854887/EN-US\_TP\_9605.dita\#concept\_a3f\_mg2\_wdb](../DNA0011854887/EN-US_TP_9605.dita#concept_a3f_mg2_wdb)
-   [../DNA0011854887/EN-US\_TP\_9604.dita\#concept\_jl1\_qzd\_wdb](../DNA0011854887/EN-US_TP_9604.dita#concept_jl1_qzd_wdb)
-   [Detach a cloud disk](reseller.en-US/Block Storage/Block storage/Detach a cloud disk.md#)
-   [EN-US\_TP\_9679.dita\#concept\_stg\_xd3\_ydb](EN-US_TP_9679.dita#concept_stg_xd3_ydb)
-   [EN-US\_TP\_9683.dita\#concept\_vbb\_ckj\_ydb](EN-US_TP_9683.dita#concept_vbb_ckj_ydb)

## What is the I/O performance of an SSD cloud disk? {#section_ypv_dbe_eht .section}

For detailed information, see [Block storage performance](reseller.en-US/Block Storage/Block storage performance.md#).

## What scenarios are SSD cloud disks suitable for? {#section_8b8_a3b_xl7 .section}

SSD cloud disks apply to the following scenarios:

-   I/O-intensive applications, such as MySQL, SQL Server, Oracle, PostgreSQL, and other small and medium-sized relational databases
-   Small and medium-sized development and testing environments

## What is I/O optimization? Can I make a standard ECS instance an I/O-optimized instance? {#section_h1e_cfl_hia .section}

I/O optimization is a means of providing better storage performance for instances. For example, the storage performance of an SSD cloud disk can be optimized by attaching it to an I/O-optimized instance.

ECS instances that are already purchased do not support I/O optimization, and non-I/O-optimized instances cannot be upgraded to I/O-optimized instances.

## Can I use an SSD cloud disk to replace an existing basic cloud disk? {#section_63d_xhf_h8g .section}

No, as SSD cloud disks use SSD storage media, they cannot be used to replace existing basic cloud disks.

## How can I purchase an SSD cloud disk? What are the prices of I/O-optimized instances and SSD cloud disks? {#section_cvs_qnf_00b .section}

For detailed information, see [Prices](https://www.alibabacloud.com/product/ecs).

## What can I do if one or more of my custom images do not support I/O-optimized instances? {#section_y34_m8t_u25 .section}

If you want to create an I/O-optimized instance from custom images, open a ticket and include details about the image name. If Alibaba Cloud authorizes the requested image type, you can use it to create I/O-optimized instances.

## Can I upgrade the SSD cloud disk after I purchase it? {#section_cz5_52j_6mh .section}

Yes, an SSD cloud disk can be upgraded and resized.

## Why did my Linux system report an error when I attempted to mount an SSD cloud disk to an I/O-optimized instance? {#section_4mp_qna_fax .section}

The mount point for SSD cloud disks in the Linux system is /dev/vdx, whereas the mount point for basic cloud disks is /dev/xvdx. If you use the original tool script for basic cloud disks to mount SSD cloud disks, an error will occur. To resolve this issue, we recommend that you enter the mount point /dev/vdx when you manually mount an SSD cloud disk.

## Why does my instance shut down when I use FIO to test I/O performance? {#section_plz_o41_a56 .section}

The FIO tool supports I/O performance testing on the bare disk partition or on the file system. However, if you directly test bare disk partitions, the metadata in the bare disk partition may be damaged, meaning that you may be unable to access related files. This will cause the instance to shut down. This problem does not occur when you use the FIO file system to test I/O performance.

## What test tools and methods can I use to evaluate the performance of my block storage? {#section_lch_qy5_pp3 .section}

For detailed information, see [Block storage performance](reseller.en-US/Block Storage/Block storage performance.md#).

## What is Shared Block Storage? {#section_jpg_i06_bmp .section}

ECS Shared Block Storage is a data block-level storage device that supports concurrent reads/writes by multiple ECS instances. It features a high level of concurrency, performance, and reliability. A single Shared Block Storage device can be attached to a maximum of eight ECS instances at the same time.

## What are the benefits of Shared Block Storage? {#section_d5h_ch5_1qs .section}

In a traditional cluster architecture, multiple computing nodes require access to the same copy of data so that the entire cluster can continue providing services even if one or more computing nodes fail. If data files are stored in Shared Block Storage devices and these devices are managed through the cluster file system, data consistency can be guaranteed between multiple front-end computing nodes during concurrent read/write operations.

## How is Shared Block Storage billed? {#section_1sk_kzf_5qd .section}

Currently, Shared Block Storage is available across all regions free of charge. For the latest billing information, see the official [Alibaba Cloud website](https://www.alibabacloud.com/).

## How can I apply for Shared Block Storage? {#section_3m1_cgm_tzv .section}

To use Shared Block Storage, you must first open a ticket.

## What scenarios are Shared Block Storage suitable for? {#section_8a7_a5l_632 .section}

Shared Block Storage is designed for the high availability architecture required by enterprise-level applications. It provides shared access to block storage devices in a Shared-everything architecture, such as the high availability server cluster architecture and the Oracle database with Oracle RAC architecture. The Oracle RAC architecture is common among government departments, enterprises, and financial customers.

## How can I use Shared Block Storage? {#section_ycn_dlp_fhb .section}

To use block devices, you must first install a cluster file system separately.

You can use cluster file systems such as GFS and GPFS to manage Shared Block Storage. If your architecture is a typical Oracle RAC architecture, we recommend that you use ASM to manage storage volumes and data files.

If you attach Shared Block Storage devices to multiple ECS instances but use a conventional file system to manage them, disk space allocation conflicts and data file inconsistencies may occur:

-   Disk space allocation conflict

    If a Shared Block Storage device is attached to multiple instances and one of these instances \(for example, Instance A\) writes data to a file, Instance A checks the file system and available disk space. After the write operation is completed, the space allocation record of Instance A is changed, but the records of other instances are not updated. In this case, when another instance \(for example, Instance B\) tries to write data to the file, this instance may allocate the disk space that has been already allocated by Instance A, resulting in a disk space allocation conflict.

-   Data file inconsistency

    After an instance \(for example, Instance A\) reads and caches data, another process that accesses the same data will directly read the data from the cache. However, if a copy of the same data that is stored on another instance \(for example, Instance B\) is modified during this period, and Instance A does not update according to the latest data change, Instance A still reads the data from the cache. As a result, data inconsistency occurs.


## Can I attach Shared Block Storage to instances across regions and zones? {#section_adn_dlp_fhb .section}

No, a Shared Block Storage device can only be attached to instances in the same zone of the same region.

## How many Shared Block Storage devices can be attached to one ECS instance? {#section_bdn_dlp_fhb .section}

Up to 16 data disks can be attached to one ECS instance.

## What are the specifications and performance of Shared Block Storage? {#section_cdn_dlp_fhb .section}

Currently, SSD and Ultra Shared Block Storage devices are supported. For more information about their specifications and performance, see [Block storage performance](reseller.en-US/Block Storage/Block storage performance.md#).

## How can I test the performance of Shared Block Storage? {#section_frj_h4p_fhb .section}

According to the number of instances involved and the required test item, run the corresponding command as needed.

**Note:** When you use the FIO for the performance test, the total iodepth value of multiple clients cannot exceed 384. If the test is conducted simultaneously on four instances, the iodepth value of each client cannot exceed 96.

|Number of instances involved|Test item|Command|
|:---------------------------|:--------|:------|
|2|Random write IOPS| ``` {#codeblock_3ox_r3c_o6o}
FIO -direct=1 -iodepth=128 -rw=randwrite -ioengine=libaio -bs=4k -size=1G -numjobs=1
              -runtime=1000 -group_reporting -filename=iotest -name=Rand_Write_Testing
```

 |
|Random read IOPS| ``` {#codeblock_ln5_d7f_nom}
FIO -direct=1 -iodepth=128 -rw=randread -ioengine=libaio -bs=4k -size=1G -numjobs=1
              -runtime=1000 -group_reporting -filename=iotest -name=Rand_Read_Testing
```

 |
|Random write IOPS| ``` {#codeblock_sr7_h7x_4q5}
FIO -direct=1 -iodepth=64 -rw=write -ioengine=libaio -bs=64k -size=1G -numjobs=1
              -runtime=1000 -group_reporting -filename=iotest -name=Write_PPS_Testing
```

 |
|Random read throughput| ``` {#codeblock_hmk_s8z_4cq}
FIO -direct=1 -iodepth=64 -rw=read -ioengine=libaio -bs=64k -size=1G -numjobs=1
              -runtime=1000 -group_reporting -filename=iotest -name=Read_PPS_Testing
```

 |
|4|Random write IOPS| ``` {#codeblock_dwu_qll_ss2}
FIO -direct=1 -iodepth=96 -rw=randwrite -ioengine=libaio -bs=4k -size=1G -numjobs=1
              -runtime=1000 -group_reporting -filename=iotest -name=Rand_Write_Testing
```

 |
|Random read IOPS| ``` {#codeblock_3pw_yvn_lrg}
FIO -direct=1 -iodepth=96 -rw=randread -ioengine=libaio -bs=4k -size=1G -numjobs=1
              -runtime=1000 -group_reporting -filename=iotest -name=Rand_Read_Testing
```

 |
|Write throughput| ``` {#codeblock_v3o_2zm_sgy}
FIO -direct=1 -iodepth=64 -rw=write -ioengine=libaio -bs=64k -size=1G -numjobs=1
              -runtime=1000 -group_reporting -filename=iotest -name=Write_PPS_Testing
```

 |
|Read throughput| ``` {#codeblock_a43_2eb_112}
FIO -direct=1 -iodepth=64 -rw=read -ioengine=libaio -bs=64k -size=1G -numjobs=1
              -runtime=1000 -group_reporting -filename=iotest -name=Read_PPS_Testing
```

 |

## What should I consider when selecting zones for ECS instance deployment? {#section_vmf_2jp_fhb .section}

-   If you require high application availability, we recommend that you deploy ECS instances in different zones.
-   If you require lower network latency, we recommend that you deploy ECS instances in the same zone.

Note that an independent Pay-As-You-Go cloud disk must be mounted to an ECS instance in the same zone.

## What is an independent cloud disk? {#section_lth_2jp_fhb .section}

An independent cloud disk is a cloud disk that you can purchase separately, and can be mounted to or unmounted from any ECS instance in the same zone. Before you can use an independent cloud disk, you must first mount it to an instance and set the relevant configurations. For more information, see [Create a Pay-As-You-Go cloud disk](reseller.en-US/Block Storage/Block storage/Create a cloud disk/Create a Pay-As-You-Go cloud disk.md#).

## Can I mount one cloud disk to multiple ECS instances? {#section_g5g_b2r_fhb .section}

No, a cloud disk can be mounted to only one ECS instance in the same zone.

## Do I need to partition and format a Pay-As-You-Go cloud disk after I purchase it and mount it to an ECS instance? {#section_gps_gpr_fhb .section}

After purchasing an independent Pay-As-You-Go cloud disk, you must mount the disk to an ECS instance and format it. For more information, see [Format a data disk of a Linux instance](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk of a Linux instance.md#) and [Format a data disk for a Windows instance](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for a Windows instance.md#).

## How is an independent Pay-As-You-Go data disk billed? {#section_v4m_b2r_fhb .section}

The fee for a Pay-As-You-Go data disk is calculated based on the amount of data space you have used. Note that if your account balance is insufficient, the data disk service will be suspended.

## Can I attach an independent Pay-As-You-Go data disk to a Subscription instance? {#section_xtp_b2r_fhb .section}

Yes.

## Can I detach a data disk from a Subscription instance? {#section_tsb_3gr_fhb .section}

You cannot detach a data disk from a Subscription instance. The data disk is released with instance when the instance expires. If you want to release the data disk, first convert the Subscription data disk to a Pay-As-You-Go data disk, and then detach and release the data disk. For information about how to convert the billing method of cloud disks, see [Convert the billing methods of cloud disks](reseller.en-US/Block Storage/Block storage/Convert the billing methods of cloud disks.md#).

## I changed the configuration of an instance during its renewal. Can I convert a Subscription cloud disk to a Pay-As-You-Go cloud disk within the instance renewal period? {#section_nql_jnr_fhb .section}

No, you can convert a Subscription cloud disk to a Pay-As-You-Go cloud disk only after the instance renewal period elapses.

## Why was my cloud disk that was created separately from its corresponding instance released at the same time as the instance? {#section_hl3_3gr_fhb .section}

This is related to the release setting that is selected when you mount a separately created data disk. That is, when you mount a separately created data disk to an instance, you can choose whether this data disk is released along with the instance. You can change the release setting at any time through the ECS console or by calling the related API.

## Why am I unable to find my ECS instance when I attempt to mount a cloud disk? {#section_ewk_3gr_fhb .section}

Check whether the target ECS instance has been released. If the instance is displayed \(indicating it has not been released\), make sure it is in the same zone of the same region as the cloud disk.

## When I delete a cloud disk, will the corresponding snapshots also be deleted? {#section_a41_mgr_fhb .section}

If you have selected **Delete Automatic Snapshots While Releasing Disk**, the corresponding automatic snapshots will be deleted when you delete the associated cloud disk. However, corresponding manual snapshots are retained. You can modify this setting at any time by setting the required policy. For more information, see [Apply or disable an automatic snapshot policy](../../../../reseller.en-US/Snapshots/Automatic snapshot policies/Apply or disable an automatic snapshot policy.md#).

## Why are some automatic snapshots on my cloud disk missing? {#section_jvf_shr_fhb .section}

Some automatic snapshots may be missing because the system deletes automatic snapshots \(starting with the oldest snapshots\) when the snapshot quota is reached. Manual snapshots are not affected.

## How many cloud disks can be mounted to one ECS instance? {#section_kp3_shr_fhb .section}

Up to 16 data disks can be mounted to one ECS instance.

## Will the data on my disk be deleted when I unmount a cloud disk \(data disk\)? {#section_fdl_shr_fhb .section}

There is a possibility that the data on your disk will be deleted when you unmount a cloud disk \(data disk\). Therefore, we strongly recommend that you plan accordingly.

-   In Windows, we recommend that you stop the read and write operations on all file systems of the cloud disk to ensure data integrity. Otherwise, the data being read or written will be lost.
-   In Linux, you must log on to the ECS instance and run the umount command. After the command is executed successfully, log on to the ECS console to unmount the disk.

## Can I unmount the system disk? {#section_ats_klr_fhb .section}

You cannot unmount the system disk, but you can replace it. For information about how to replace the system disk, see [Replace the system disk \(non-public image\)](reseller.en-US/Block Storage/Block storage/Change the operating system/Replace the system disk (non-public image).md#).

## What is a mount point? {#section_h4v_klr_fhb .section}

A mount point is the location of the Alibaba Cloud ECS disk on the disk controller bus. The mount point matches the disk device number in Linux, and matches the disk order in the Disk Management in Windows.

## Are my snapshots retained if I reinitialize a cloud disk? {#section_msx_klr_fhb .section}

Yes, both manual snapshots and automatic snapshots are retained when you initialize a cloud disk.

## Are my snapshots retained if I replace the system disk? {#section_ywz_klr_fhb .section}

This depends on the creation method of the snapshot. Manual snapshots will be retained, but automatic snapshots will be deleted.

**Note:** The disk ID is changed when you replace the system disk. This means that the snapshots of the original system disk cannot be used for the new system disk. However, you can use the manual snapshots preserved on the original system disk to create a custom image.

## Can I use a snapshot to create an independent cloud disk? {#section_tz3_jnr_fhb .section}

Yes, you can use an existing snapshot to create an independent Pay-As-You-Go cloud disk. The newly created data disk has the same size and use the same data as the snapshot. However, the size of the cloud disk cannot be modified.

## What can I do if I cannot access a Linux data disk because of possible data disk mounting errors? {#section_fz4_jnr_fhb .section}

If data of a Linux data disk cannot be accessed, follow these steps to fix the error:

1.  Locate the disk where the data is stored and check whether the data disk is mounted to the corresponding ECS ​​instance by using either of the following methods:
    -   Perform the check in the ECS console. For more information, see [Monitor a cloud disk](reseller.en-US/Block Storage/Block storage/Monitor a cloud disk.md#).
    -   Log on to the instance, run the `fdisk -l` command to check whether the data disk partition information is correct, and run the `df -h` and `mount | grep "<devpath>"` commands to view the mount information.
2.  Run the cat command to view the /etc/fstab file and check whether you mount two cloud disks to the same directory.
    -   If two cloud disks are mounted to the same directory, the previously mounted cloud disk will be replaced by the new one, resulting in data inaccessibility. We recommend that you mount one of the cloud disks to a different directory.
    -   If they are mounted to different directories but the mount information shows that they are in the same directory, run the ll command to check whether there are links between the two directories. If there is a link, run the mkdir command to create a new directory, mount one of the cloud disks to this directory, and check whether data can be accessed.

## How can I resize a system disk? {#section_wdn_d4r_fhb .section}

You can resize a system disk through the ECS console or by calling [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9892.md\#](../../../../reseller.en-US/API Reference/Disk/ResizeDisk.md#). You can also resize a system disk by replacing it with a disk of larger specification.

## What considerations should I be aware of before I replace a system disk? {#section_z4d_vlv_fhb .section}

Before replacing a system disk, you must:

-   Create snapshots and custom images of the current system disk.
-   Make sure that your disk has enough space for storing the snapshots and images. The recommended disk space is 1GiB or larger. If the disk space is insufficient, the system may not start properly after you replace the system disk.

## What block storage devices support system disk resizing, and is there any regional restriction for this action? {#section_cbz_pdh_fhb .section}

Ultra cloud disks, SSD cloud disks, and ESSD cloud disks support system disk resizing, and all regions of the Alibaba Cloud ecosystem support system disk resizing.

## Can I resize the system disk of Subscription and Pay-As-You-Go instances? {#section_tjd_xqr_fhb .section}

Yes, the system disk of both Subscription and Pay-As-You-Go instances can be resized.

## What is the storage capacity range of a system disk? {#section_nx3_xqr_fhb .section}

The capacity of a system disk varies depending on the operating system. For more information, see [Overview](reseller.en-US/Block Storage/Block storage/Resize cloud disks/Overview.md#).

## I downgraded the configuration of a Subscription instance during its renewal. Can I specify a new system disk capacity after the renewal is completed? {#section_k1m_xqr_fhb .section}

After you [downgrade the configuration](downgrade the configuration../DNA0011810291/EN-US_TP_9593.dita#concept_pjr_l2d_5db) of a Subscription instance through instance renewal, you can resize the system disk of the instance only at the start of the next billing cycle.

## Can I scale in a system disk after I scale it out? {#section_qj5_43v_fhb .section}

No, you cannot scale in a system disk after you scale it out.

## Can I partition a data disk for data storage? {#section_ppz_43v_fhb .section}

Yes, you can divide a data disk into multiple partitions according to your specific needs. We recommend that you use the system tool for partitioning.

## For a disk with multiple partitions, are snapshots created for the entire disk or only for a specific partition? {#section_q5b_p3v_fhb .section}

Snapshots are created for the entire disk, rather than for a specific partition.

## What considerations should I be aware of before I repartition a disk? {#section_tty_ioz_c1s .section}

To ensure data security, we recommend that you [create a snapshot](create a snapshot../DNECS19100342/EN-US_TP_9687.dita#concept_eps_gbl_xdb) of the target disk before you can repartition it. This way, you can roll back the disk if an exception occurs.

## I rolled back the snapshot of a data disk after repartitioning it. How is the number of partitions changed? {#section_nyd_3mv_fhb .section}

Snapshot rollback returns a snapshot to its previous state. This means that if the disk has not been repartitioned at the time point of the previous state, there is only one partition.

## How can I ensure no data is lost during a data disk scale-out if I need to create a cloud disk from a snapshot? {#section_v2g_3mv_fhb .section}

If the original data disk cannot be scaled out due to a disk error, you can purchase a temporary Pay-As-You-Go cloud disk to store data and then format the original data disk. To do so, follow these steps:

1.  Create a snapshot of the current data disk.
2.  Go to the disk purchase page to purchase a Pay-As-You-Go cloud disk, select the same region and zone as the ECS instance, and click **Create from snapshot**.
3.  Log on to the ECS console and then mount the data disk you purchased to an ECS instance.
4.  Log on to the ECS instance, run the mount command to mount the purchased disk to the ECS instance, and then check whether files in this disk are the same as those in the original data disk.
5.  Run the fdisk command to delete the original partition table, and then run commands such as fdisk and mkfs.ext3 to format and partition the original data disk again, so that the available space of the original data disk is the same as that after the scale-out action.
6.  Run the cp -R command to copy all the data in the purchased disk back to the original data disk. You can add the --preserve=all parameter to preserve the file's properties when copying files.
7.  Run the umount command to unmount the purchased data disk.
8.  Log on to the ECS console, unmount the purchased data disk from the ECS instance, and release it.

## In a Linux instance, what considerations should I be aware of before I add mount information to a basic cloud disk or an SSD cloud disk? {#section_tdy_jmv_fhb .section}

When you add a data disk to the Linux system and add the partition information according to [Format a data disk of a Linux instance](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk of a Linux instance.md#), note that the mount point of a basic cloud disk is /dev/xvdb1 and that of an SSD cloud disk is /dev/ Vdb1. If you add invalid information, disk mounting will fail. To avoid this issue, follow these steps:

1.  Run the `fdisk -l` command to view data disk information.
2.  Check whether the information added to `/etc/fstab` is valid. Do not add mount information repeatedly because this will cause a system startup failure.
3.  Run the vim command to modify the `/etc/fstab` file.
4.  Comment out or delete invalid information, add valid mount information, and then run the `mount -a` command to check whether the data disk is successfully mounted.

## How can I re-mount data disks after initializing a Linux instance? {#section_r11_kmv_fhb .section}

Initializing the system disk of a Linux instance does not change data on the data disk. However, all the data disks will be unmounted. Therefore, you need to mount the data disks again. To do so, follow these steps:

**Note:** In this example, assume that the mount point is /dev/vdb1 and the mount point name is /InitTest before the system disk is initialized.

1.  Run the `mount` command to view the data disk mount status.

    The command output does not contain information related to /dev/vdb1.

2.  Run the `fdisk -l` command to view partitioned data disks.
3.  Run the `mkdir /InitTest` command to re-create the mount point of the data disk partition. The mount point name must be the same as that of the mount point /dev/vdb1 before the system disk initialization. You can view the original mount point name by running the `cat /etc/fstab` command.
4.  Run the `mount /dev/vdb1 /InitTest` command to remount the data disk partition.
5.  Run the `df -h` command to view the mount results.
6.  Check whether /dev/vdb1 can be mounted automatically.
    1.  Run the `umount /dev/vdb1` command to unmount /dev/vdb1.
    2.  Run the `mount` command to check whether the partition is successfully unmounted. If this is the case, the returned result does not contain information related to /dev/vdb1.
    3.  Run the `mount -a` command to automatically mount /dev/vdb1.
    4.  Run the `mount` command to check whether the auto-mount succeeded. If this is the case, the returned result contains information related to /dev/vdb1.

## What can I do if data disks of a Linux instance cannot be found after I restart the instance or initialize the system? {#section_fs3_hjx_fhb .section}

Symptom: After restarting a Linux instance or initializing the system, I log on to the instance and run the `df -h` command to check the disk mount status. However, no data disk can be found.

Cause:

-   Restarting an instance: Mount information was not written to the /etc/fstab file when the data disk was mounted. As a result, data disks are not automatically mounted after the instance restarts.
-   Initializing the system: The /etc/fstab file is reset after the system disk is initialized. As a result, data disks are not automatically mounted upon system startup.

Solution:

1.  Run the `mount /dev/xvdb1` command to mount the data disk.
2.  Run the mount command to check the format of files in the /dev/xvdb1 partition.

    In this example, the file format is ext3.

3.  Run the following command to write the data disk mount information to /etc/fstab:

    ``` {#codeblock_djo_2nw_e5s}
    echo '/dev/xvdb1 /data ext3 defaults 0 0' >> /etc/fstab
    ```


## **What can I do if data is lost after I restart a Linux instance?** {#section_pvl_hjx_fhb .section}

Symptom: All data in the /alidata directory is lost after I restart a Linux instance.

Cause: Output of the `df -h` command shows that no data disk is mounted to the instance.

Solution:

**Note:** This solution uses an I/O-optimized instance as an example. If you use a non-I/O-optimized instance, the disk partition is /dev/xvdb1.

1.  Run the `fdisk -l` command.

    The output shows that one disk is not mounted.

2.  Run the `mount /dev/vdb1 /alidata` command to mount this disk to the instance.

We recommend that you also enable auto-mount at startup for /etc/fstab to avoid encountering this issue again.

## What can I do if the error message "Bad magic number in super-block while trying to open /dev/xvdb1" is returned when I resize the cloud disk of a Linux instance? {#section_mnf_nrv_fhb .section}

Symptom: The error message "Bad magic number in super-block while trying to open /dev/xvdb1" is returned when I run the `e2fsck -f /dev/xvdb` command to resize a cloud disk.

Cause: There is no disk partition

Solution: Run the `e2fsck -f /dev/xvdb` and `resize2fs /dev/xvdb` commands to resize the disk. Then mount the disk to the instance.

## What can I do if an error message similar to "Only disks on stopped instances and disks with no ongoing snapshot tasks and no replaced operating system can be rolled back." is returned? {#section_psz_3vy_ghb .section}

Symptom: An error message similar to "Only disks on stopped instances and disks with no ongoing snapshot tasks and no replaced operating system can be rolled back." is returned when I attempt to roll back a cloud disk.

Cause: The problem is usually caused by incorrect disk attributes or disk status.

Solution:

-   Check whether the operating system of instances associated with related snapshots has been replaced. For more information, see [EN-US\_TP\_9683.dita\#concept\_vbb\_ckj\_ydb](EN-US_TP_9683.dita#concept_vbb_ckj_ydb).

    If the operating system has been replaced, the system disk of the instance will be automatically re-created from the new image and the system disk ID will change. Therefore, original snapshots cannot be used for the rollback. However, you can [../DNECS19100339/EN-US\_TP\_9696.dita\#concept\_gpg\_t5l\_xdb](../DNECS19100339/EN-US_TP_9696.dita#concept_gpg_t5l_xdb) from related snapshots and then specify the custom image by [replacing the system disk \(non-public image\)](replacing the system disk (non-public image)EN-US_TP_9683.dita#concept_vbb_ckj_ydb) to switch the instance to the corresponding snapshot state.

-   Check whether the instance has stopped.

    You can only roll back a stopped instance. You can view the instance status on the Instances page of the ECS console.

-   Check whether the disk has an ongoing snapshot task.

    To ensure data consistency, do not roll back a disk that has an ongoing snapshot task. You can check the snapshot status on the Snapshots page. A snapshot task is ongoing if its **Progress** is not **100%** and **Status** is **Progressing**.

    If you need to forcibly terminate related snapshot tasks to accelerate the rollback, select the corresponding snapshots and click Delete.


## How can I copy data across instances? {#section_kc2_efn_3fb .section}

You can choose data copy methods based on your operating system:

-   Data copy between Linux instances
    -   Using the lrzsz tool

        Log on to the Linux instance, install the lrzsz tool, run the rz command to upload files, and run the sz command to download these files.

        You can also first run the sz command to download files to your local PC and run the rz command to upload these files to another instance.

    -   Using the FTP tool

        If you use the SFTP tool, we recommend that you use the root account for instance logon and file upload and download.

    -   Using the wget command

        After compressing a file or a folder, save it to the web directory to generate a download URL. Then run the wget command on another instance to download the file or folder.

-   Data copy between Linux and Windows

    We recommend that you use the SFTP tool to download files from a Linux instance to your local PC and use the FTP tool to upload data to a Windows instance.

-   Data copy between Windows
    -   FTP tool
    -   Alibaba TradeManager

## Can I mount a cloud disk to an ECS instance that is in a different zone from the cloud disk? {#section_7el_s1q_i5w .section}

No, you can only mount a Pay-As-You-Go cloud disk to an ECS instance that is in the same zone as the cloud disk.

## Why am I unable to find the data disk I purchased for a Linux instance? {#section_d47_uxx_zga .section}

If you purchase a Pay-As-You-Go data disk separately, you need to [format the data disk](format the data disk../DNA0011854887/EN-US_TP_9604.dita#concept_jl1_qzd_wdb) and [attach it](reseller.en-US/Block Storage/Block storage/Attach a cloud disk.md#) to a Linux instance before you can use it.

## Where can I purchase a last-generation disk \(a local SSD disk\) and how can I maintain an existing local SSD disk? {#section_us2_rh2_rl5 .section}

Local SSD disks are no longer available for purchase. If you are still using a local SSD disk, see [EN-US\_TP\_9561.dita\#concept\_g3w\_qzv\_tdb](EN-US_TP_9561.dita#concept_g3w_qzv_tdb) and [FAQ about SSD cloud disks](#).

## How can I test the performance of an ESSD cloud disk? {#ESSDperfor .section}

This FAQ describes how to configure the appropriate environments for a performance test and how to obtain a 1 million IOPS result. Note that the cloud disk type and actual environment used will impact the test result.

**Warning:** You can obtain accurate test results by testing a bare disk partition, but you may destroy the file system structure by testing it directly. Before such a test, you must [create a snapshot](create a snapshot../DNECS19100342/EN-US_TP_9687.dita#concept_eps_gbl_xdb) of the disk to back up your data. We recommend that you use newly purchased ECS instances that contain no data for the test to prevent any data loss.

We recommend that you use the latest versions of Linux images in Alibaba Cloud official images, such as CentOS 7.4/7.3/7.2 \(64-bit\) and AliyunLinux 17.1 \(64-bit\) because Linux images of earlier versions and Windows images may use defective drivers.

We also recommend that you use the [FIO](https://linux.die.net/man/1/fio) for the performance test.

Assume that the instance type is ecs.g5se.18xlarge and the device name of the ESSD disk is `/dev/vdb`. This example describes how to test the random write \(`randwrite`\) performance of an ESSD cloud disk.

1.  Connect to the Linux instance.
2.  Run the following commands to install the libaio and FIO tools.

    ``` {#codeblock_eco_4hg_8tu}
    sudo yum install libaio –y
    sudo yum install libaio-devel –y
    sudo yum install fio -y
    ```

3.  Run the `cd /tmp` command to change the directory.
4.  Run the `vim test100w.sh` command to create a script test100w.sh and paste the following code to the script to test the random write `randwrite` IOPS.

    ``` {#codeblock_1lh_q2w_3tw}
    function RunFio
    {
     numjobs=$1  # The number of the tested threads, such as 8 in this example.
     iodepth=$2  # The maximum concurrent I/O requests, such as 64 in this example.
     bs=$3       # The size of the data block for one I/O, such as 4k in this example.
     rw=$4       # The read and write policy, such as randwrite in this example.
     filename=$5 # The name of the tested file, such as /dev/vdb in this example.
     nr_cpus=`cat /proc/cpuinfo |grep "processor" |wc -l`
     if [ $nr_cpus -lt $numjobs ];then
         echo “Numjobs is more than cpu cores, exit!”
         exit -1
     fi
     let nu=$numjobs+1
     cpulist=""
     for ((i=1;i<10;i++))
     do
         list=`cat /sys/block/vdb/mq/*/cpu_list | awk '{if(i<=NF) print $i;}' i="$i" | tr -d ',' | tr '\n' ','`
         if [ -z $list ];then
             break
         fi
         cpulist=${cpulist}${list}
     done
     spincpu=`echo $cpulist | cut -d ',' -f 2-${nu}`
     echo $spincpu
     fio --ioengine=libaio --runtime=30s --numjobs=${numjobs} --iodepth=${iodepth} --bs=${bs} --rw=${rw} --filename=${filename} --time_based=1 --direct=1 --name=test --group_reporting --cpus_allowed=$spincpu --cpus_allowed_policy=split
    }
    echo 2 > /sys/block/vdb/queue/rq_affinity
    sleep 5
    RunFio 8 64 4k randwrite /dev/vdb
    ```

    **Note:** 

    -   You must modify the following commands according to your test environment.
        -   `vdb` in the command line `list=`cat /sys/block/vdb/mq/*/cpu_list | awk '{if(i<=NF) print $i;}' i="$i" | tr -d ',' | tr '\n' ','``
        -   `8`, `64`, `4k`, `randwrite`, and `/dev/vdb` in the command line `RunFio 8 64 4k randwrite /dev/vdb`
    -   The file system structure may be damaged if you test the bare disk partition directly. If you choose to proceed with this action, set `filename` as the device name, such as /dev/vdb. If you do not want to risk data loss, set `filename` as a file path, such as /mnt/test.image.
5.  Run `sh test100w.sh` to start testing the performance of the ESSD disk.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10111/156679782242181_en-US.png)


Script details

-   Block device parameter

    The command `echo 2 > /sys/block/vdb/queue/rq_affinity` in the script is used to set the value of the `rq_affinity` parameter to `2`.

    -   If the value of the `rq_affinity` parameter is `1`, the block device migrates the I/O Completions to the vCPU group that originally submitted the request. In this way, I/O Completions may run on the same vCPU in the case of concurrent processing I/O requests by multiple threads. This may cause a performance bottleneck.
    -   If the value of the `rq_affinity` parameter is `2`, the I/O Completions are forced to run on the requesting vCPU. As a result, performance of each vCPU is fully used in the case of concurrent processing I/O requests by multiple threads.
-   Binding threads to corresponding vCPU cores
    -   Generally, a device has only one Request-Queue. This unique Request-Queue is a bottleneck in the case of concurrent processing I/O requests by multiple threads.
    -   In the latest Multi-Queue mode, one device can have multiple Request-Queues that process I/O requests, which deliver full performance of the back-end storage. If you have four I/O threads, you must bind them to the vCPU core corresponding to each Request-Queue. This allows you to fully use the Multi-Queue mode to improve the storage performance.

To fully output the performance of the device, you must assign the I/O requests to different Request-Queues. The following command in the script can be used to bind `jobs` to different vCPU cores. `/dev/vd*` is the device name of your ESSD cloud disk, for example, /dev/vdb.

``` {#codeblock_l3b_ggy_nfl}
fio —ioengine=libaio —runtime=30s —numjobs=${numjobs} —iodepth=${iodepth} —bs=${bs} —rw=${rw} —filename=${filename} —time_based=1 —direct=1 —name=test —group_reporting —cpus_allowed=$spincpu —cpus_allowed_policy=split
```

FIO provides the `cpusallowed` and `cpus_allowed_policy` parameters to bind vCPUs. The preceding command runs multiple `jobs`. They are bound to different CPU cores and correspond to different `Queue_Id`.

To view the `cpu_core_id` corresponding to a `Queue_Id`, follow the instructions:

1.  Run the `ls /sys/block/vd/mq/` command to check the `Queue_Id` of the ESSD disk with the device name `/dev/vd*`, for example, `/dev/vdb`.
2.  Run the `cat /sys/block/vd/mq//cpu_list` command to check the `cpu_core_id` corresponding to the `Queue_Id`.

