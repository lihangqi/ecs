# Why is the size of a snapshot of a disk larger than the disk space usage displayed in the file system? {#concept_apr_lsr_lgb .concept}

Each ECS instance is assigned one or more disks, which share a file system. When you delete one or more files from an ECS instance and then create a snapshot of the corresponding disk, the snapshot size is larger than the space occupied by the disk.

## Possible causes {#section_ajl_ggh_4gb .section}

The size of a snapshot of a disk may be inconsistent with the disk usage space displayed in the file system due to one of the following causes:

-   The metadata of the file system occupies disk space.
-   A large number of blocks are written to the file system when the file system is initialized. These blocks occupy disk space.
-   To reduce performance consumption, the file system only creates deprecation tags when files are deleted. However, the disk is unaware of the deletion command and still regards the blocks as assigned. As a result, the blocks are copied to the snapshot, making the snapshot size larger than the disk space usage of the file system.
-   The Virtio-block module of KVM and the Block-front module of Xen do not support the TRIM command \(an I/O command that indicates which blocks of data are no longer considered in use and can be wiped internally\). As a result, the data is retained in the disk.

## Relationships between the file system, disk, and snapshot {#section_rwz_4nq_wgb .section}

The file system you create on your disk partitions is responsible for managing disk space. The relevant management operations are finally converted to I/O requests of the disk. The disk records the status of blocks and copies the disk data to the Object Storage Service \(OSS\). This is the process in which a snapshot is created. The following figure shows the relationships between the file system and the snapshot.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10122/155905036139434_en-US.png)

**Note:** The blocks to which data is written will be recorded into the snapshot regardless of whether the relevant files have been deleted from the disk. When deleting a file, the file system tags the file head to indicate that the space occupied by the file becomes available, but this does not reduce the space that the disk occupies.

## Relationships between data writes and disk formatting {#section_f21_qyg_4gb .section}

A new disk or a new disk partition must be formatted and its data structure must be recorded before the disk or disk partition can be used. The purpose of formatting is to create a file system. Data writes are required to create a file system in a disk. The size of files written to the disk varies depending on file systems during formatting.

-   Disk formatting in Windows, which is classified into quick formatting and normal formatting.
    -   Quick formatting: In quick formatting, a file system is assigned to the disk partitions and the File Directory Table \(FDT\) is rewritten. The data writes during quick formatting occupy relatively small space.
    -   Normal formatting: In normal formatting, the operations in quick formatting are also performed. Moreover, the disk partitions are scanned sector by sector to identify and tag bad sectors and fill in free disk blocks. This is equivalent to writing the data of the entire disk. Therefore, the size of the full snapshot is almost equal to the disk capacity.
-   Disk formatting in Linux: After the disk is formatted, the size of the first snapshot depends on the disk file system format before business data is written to the instances.

