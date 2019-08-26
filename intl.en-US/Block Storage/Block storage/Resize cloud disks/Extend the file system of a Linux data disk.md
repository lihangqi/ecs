# Extend the file system of a Linux data disk {#concept_z11_xsh_ydb .concept}

This topic describes how to extend the file system of a Linux data disk. Resizing a cloud disk does not extend the file system; it only extends the storage capacity. Therefore, you need to format the newly extended storage capacity after you resize a cloud disk.

## Limits {#LimitationCommon .section}

The information contained in this topic applies only to disks that are attached to ECS instances \(that is, the cloud disk is in a state other than **Available**\). For information on how to attach, partition, or format disks that are in the **Available** state, see [Attach a cloud disk](reseller.en-US/Block Storage/Block storage/Attach a cloud disk.md#) and [Partition and format a data disk](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk of a Linux instance.md#).

## Scenarios {#section_cbw_wxs_qgb .section}

|Scenario|Operation|
|:-------|:--------|
|The data disk is attached to the instance.|The data disk is partitioned and formatted.|You can follow the relevant procedure described in this topic to resize the data disk.|
|The data disk is empty and is not partitioned or formatted.|After you resize the data disk in the ECS console, you can follow the relevant procedure describe in this topic to [partition and format the data disk](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk of a Linux instance.md#).|
|The data disk is formatted but not partitioned.|After you resize the data disk in the ECS console, you can follow the procedure to [extend the file system](#).|
|The data disk is not attached to the instance.|You can resize the data disk offline, or you can resize the data disk after you attach it to the instance.|

In this example, the data disk is an ultra disk and the operating system of the ECS instance is CentOS 7.5 64-bit. The mount point of the data disk is /dev/vdb and the existing partition is /dev/vdb1. The data disk capacity before resizing is 20 GiB whereas the data disk capacity after resizing is 40 GiB. The data disk is attached to the instance and is partitioned and formatted.

-   If you want to extend the existing partition of the data disk, see [Procedure 1: Extend the existing partition](#).
-   If you want to create a partition for the newly added disk space, see [Procedure 2: Create and format a partition](#).

## Preparations {#section_tcx_kn5_qgb .section}

1.  Use the ECS console or call the API [ResizeDisk](../../../../reseller.en-US/API Reference/Disk/ResizeDisk.md#) to resize the cloud disk.
2.  [Create a snapshot](reseller.en-US/Snapshots/Use snapshots/Create a snapshot.md#) to back up your data.
3.  Attach the cloud disk to the instance and make sure that the instance is in the **Running** state. For information about the connection methods, see [Overview](../../../../reseller.en-US/Instances/Connect to instances/Overview.md#).

## Check the partition and file system {#section_tfj_pnv_qgb .section}

1.  Run the `fdisk -lu <DeviceName\>` command to check whether the data disk is partitioned.

    In this example, the data disk has the partition `/dev/vdb1`.

    ```
    [root@localhost ~]# fdisk -lu /dev/vdb
    Disk /dev/vdb: 42.9 GB, 42949672960 bytes, 83886080 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x9277b47b
    
    Device Boot Start End Blocks Id System
    /dev/vdb1 2048 41943039 20970496 83 Linux
    ```

2.  Run the `blkid <PartionName\>` command to check the file system type.

    In this example, the file system type of `/dev/vdb1` is ext4.

    ```
    [root@localhost ~]# blkid /dev/vdb1
    /dev/vdb1: UUID="e97bf1e2-fc84-4c11-9652-73554546c324" TYPE="ext4"
    ```

    **Note:** If the data disk is not partitioned or formatted, or if the data disk is partitioned but not formatted, no response message is returned.

3.  Run the following command to check the status of the file system:

    -   For ext file systems: `e2fsck -n <dst\_dev\_part\_path\>`
    -   For XFS file systems: `xfs_repair -n <dst\_dev\_part\_path\>`
    In this example, the file system is in the clean state.

    ```
    [root@localhost ~]# e2fsck -n /dev/vdb1
    e2fsck 1.42.9 (28-Dec-2013)
    Warning! /dev/vdb1 is mounted.
    Warning: skipping journal recovery because doing a read-only filesystem check.
    /dev/vdb1: clean, 11/1310720 files, 126322/5242624 blocks
    ```


**Note:** If the data disk is not partitioned or formatted, you need to partition and format it. For more information, see [Format a data disk of a Linux instance](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk of a Linux instance.md#).

## Procedure 1: Extend the existing partition {#section_yvn_mfy_dhb .section}

To avoid data loss, we recommend that you do not resize a mounted \(mount\) partition or file system. Instead, we recommend that you unmount \(umount\) the partition first, and then re-mount \(mount\) the partition after you extend it. If you do need to extend a mounted partition, follow these instructions according to the kernel version of the target instance:

-   If the kernel version of the instance is earlier than v3.6, unmount the partition, and then modify the partition table by following *Step 1: Modify the partition table* as detailed in the next section.
-   If the kernel version of the instance is later than v3.6, you need to update the kernel information after you modify the partition table.

To use the new disk space to extend the existing partition, follow these steps:

**Step 1: Modify the partition table**

1.  Run the `fdisk -lu /dev/vdb` command and note down the start sector and end sector of the old partition.

    In this example, the start sector of /dev/vdb1 is 2048 and the end sector is 41943039.

    ```
    [root@localhost ~]# fdisk -lu /dev/vdb
    Disk /dev/vdb: 42.9 GB, 42949672960 bytes, 83886080 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x9277b47b
    
    Device Boot Start End Blocks Id System
    /dev/vdb1 2048 41943039 20970496 83 Linux
    ```

2.  Run the `fdisk` command to delete the old partition.

    1.  Run the `fdisk -u /dev/vdb` command to partition the data disk.
    2.  Enter p to print the partition table.
    3.  Enter d to delete the partition.
    4.  Enter p to confirm that the partition is deleted.
    5.  Enter w to save your modifications and exit.
    ```
    [root@localhost ~]# fdisk -u /dev/vdb
    Welcome to fdisk (util-linux 2.23.2).
    Changes will remain in memory only, until you decide to write them.
    Be careful before using the write command.
    Command (m for help): p
    Disk /dev/vdb: 42.9 GB, 42949672960 bytes, 83886080 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x9277b47b
    Device Boot Start End Blocks Id System
    /dev/vdb1 2048 41943039 20970496 83 Linux
    Command (m for help): d
    Selected partition 1
    Partition 1 is deleted
    Command (m for help): p
    Disk /dev/vdb: 42.9 GB, 42949672960 bytes, 83886080 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x9277b47b
    Device Boot Start End Blocks Id System
    Command (m for help): w
    The partition table has been altered!
    Calling ioctl() to re-read partition table.
    WARNING: Re-reading the partition table failed with error 16: Device or resource busy.
    The kernel still uses the old table. The new table will be used at
    the next reboot or after you run partprobe(8) or kpartx(8)
    Syncing disks.
    ```

3.  Run the fdisk command to create a partition.

    1.  Run the `fdisk -u /dev/vdb` command to partition the data disk.
    2.  Enter p to print the partition table.
    3.  Enter n to create a partition.
    4.  Enter p to set the partition type to primary partition.
    5.  Enter <partition number\> to select a partition number. In this example, select 1.

        **Warning:** 

        -   The start sector of the new partition must be the same as that of the old partition.
        -   The end sector of the new partition must be greater than that of the old partition. Otherwise, the disk resizing operation fails.
    6.  Enter w to save your modifications and exit.
    In this example, the /dev/vdb1 partition is extended from 20 GiB to 40 GiB.

    ```
    logical[root@localhost ~]# fdisk -u /dev/vdb
    Welcome to fdisk (util-linux 2.23.2).
    Changes will remain in memory only, until you decide to write them.
    Be careful before using the write command.
    Command (m for help): p
    Disk /dev/vdb: 42.9 GB, 42949672960 bytes, 83886080 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x9277b47b
    Device Boot Start End Blocks Id System
    Command (m for help): n
    Partition type:
    p primary (0 primary, 0 extended, 4 free)
    e extended
    Select (default p): p
    Partition number (1-4, default 1): 1
    First sector (2048-83886079, default 2048):
    Using default value 2048
    Last sector, +sectors or +size{K,M,G} (2048-83886079, default 83886079):
    Partition 1 of type Linux and of size 30 GiB is set
    Command (m for help): p
    Disk /dev/vdb: 42.9 GB, 42949672960 bytes, 83886080 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x9277b47b
    Device Boot Start End Blocks Id System
    /dev/vdb1 2048 62916607 31457280 83 Linux
    Command (m for help): w
    The partition table has been altered!
    Calling ioctl() to re-read partition table.
    
    WARNING: Re-reading the partition table failed with error 16: Device or resource busy.
    The kernel still uses the old table. The new table will be used at
    the next reboot or after you run partprobe(8) or kpartx(8)
    Syncing disks.
    ```

4.  Run the `e2fsck -n /dev/vdb1` command to check the file system to confirm the file system is in the clean state.

**Step 2: Update the kernel information**

If the kernel version of the instance is later than v3.6, after you modify the partition table, run the `partprobe <dst_dev_path>` or `partx -u <dst\_dev\_path\>` command to update the kernel information.

**Step 3: Extend the file system**

-   To extend an ext file system \(for example, ext3 or ext4\), run the `resize2fs /dev/vdb1` command.

    ```
    [root@localhost ~]# resize2fs /dev/vdb1
    resize2fs 1.42.9 (28-Dec-2013)
    Resizing the filesystem on /dev/vdb1 to 7864320 (4k) blocks.
    The filesystem on /dev/vdb1 is now 7864320 blocks long.
    ```

-   To extend an XFS file system, run the `mount /dev/vdb1 /mnt/` command, and then run the `xfs_growfs /dev/vdb1` command.

    ```
    [root@localhost ~]# mount /dev/vdb1 /mnt/
    [root@localhost ~]# xfs_growfs /dev/vdb1
    
    meta-data=/dev/vdb1              isize=512    agcount=4, agsize=1310720 blks
             =                       sectsz=512   attr=2, projid32bit=1
             =                       crc=1        finobt=0 spinodes=0
    data     =                       bsize=4096   blocks=5242880, imaxpct=25
             =                       sunit=0      swidth=0 blks
    naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
    log      =internal               bsize=4096   blocks=2560, version=2
             =                       sectsz=512   sunit=0 blks, lazy-count=1
    realtime =none                   extsz=4096   blocks=0, rtextents=0
    data blocks changed from 5242880 to 7864320
    ```


## Procedure 2: Create and format a partition {#section_j4y_1gy_dhb .section}

To use the new disk space to create a partition, follow these steps:

1.  Run the `fdisk -u /dev/vdb` command to create a partition.

    In this example, the new 20 GiB disk space is used to create a partition named /dev/vdb2.

    ```
    [root@localhost ~]# fdisk -u /dev/vdb
    Welcome to fdisk (util-linux 2.23.2).
    
    Changes will remain in memory only, until you decide to write them.
    Be careful before using the write command.
    Command (m for help): p
    
    Disk /dev/vdb: 42.9 GB, 42949672960 bytes, 83886080 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x2b31a2a3
    
       Device Boot      Start         End      Blocks   Id  System
    /dev/vdb1            2048    41943039    20970496   83  Linux
    
    Command (m for help): n
    Partition type:
       p   primary (1 primary, 0 extended, 3 free)
       e   extended
    Select (default p): p
    Partition number (2-4, default 2): 2
    First sector (41943040-83886079, default 41943040):
    Using default value 41943040
    Last sector, +sectors or +size{K,M,G} (41943040-83886079, default 83886079):
    Using default value 83886079
    Partition 2 of type Linux and of size 20 GiB is set
    
    Command (m for help): w
    The partition table has been altered!
    
    Calling ioctl() to re-read partition table.
    Syncing disks.
    ```

2.  Run the `lsblk /dev/vdb` command to view the partition.

    ```
    [root@localhost ~]# lsblk /dev/vdb
    NAME   MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
    vdb    253:16   0  40G  0 disk
    ├─vdb1 253:17   0  20G  0 part
    └─vdb2 253:18   0  20G  0 part
    ```

3.  Format the new partition.
    -   To create an ext4 file system, run the `mkfs.ext4 /dev/vdb2` command.

        ```
        [root@localhost ~]# mkfs.ext4 /dev/vdb2
        mke2fs 1.42.9 (28-Dec-2013)
        Filesystem label=
        OS type: Linux
        Block size=4096 (log=2)
        Fragment size=4096 (log=2)
        Stride=0 blocks, Stripe width=0 blocks
        1310720 inodes, 5242880 blocks
        262144 blocks (5.00%) reserved for the super user
        First data block=0
        Maximum filesystem blocks=2153775104
        160 block groups
        32768 blocks per group, 32768 fragments per group
        8192 inodes per group
        Superblock backups stored on blocks:
                32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
                4096000
        
        Allocating group tables: done
        Writing inode tables: done
        Creating journal (32768 blocks): done
        Writing superblocks and filesystem accounting information: done
        
        
        [root@localhost ~]# blkid /dev/vdb2
        /dev/vdb2: UUID="e3f336dc-d534-4fdd-af71-b6ff1a55bdbb" TYPE="ext4"
        ```

    -   To create an ext3 file system, run the `mkfs.ext3 /dev/vdb2` command.

        ```
        [root@localhost ~]# mkfs.ext3  /dev/vdb2
        mke2fs 1.42.9 (28-Dec-2013)
        Filesystem label=
        OS type: Linux
        Block size=4096 (log=2)
        Fragment size=4096 (log=2)
        Stride=0 blocks, Stripe width=0 blocks
        1310720 inodes, 5242880 blocks
        262144 blocks (5.00%) reserved for the super user
        First data block=0
        Maximum filesystem blocks=4294967296
        160 block groups
        32768 blocks per group, 32768 fragments per group
        8192 inodes per group
        Superblock backups stored on blocks:
                32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
                4096000
        
        Allocating group tables: done
        Writing inode tables: done
        Creating journal (32768 blocks): done
        Writing superblocks and filesystem accounting information: done
        
        [root@localhost ~]# blkid /dev/vdb2
        /dev/vdb2: UUID="dd5be97d-a630-4593-9b0f-5056def914ea" SEC_TYPE="ext2" TYPE="ext3"
        ```

    -   To create an XFS file system, run the `mkfs.xfs -f /dev/vdb2` command.

        ```
        [root@localhost ~]# mkfs.xfs -f /dev/vdb2
        meta-data=/dev/vdb2              isize=512    agcount=4, agsize=1310720 blks
                 =                       sectsz=512   attr=2, projid32bit=1
                 =                       crc=1        finobt=0, sparse=0
        data     =                       bsize=4096   blocks=5242880, imaxpct=25
                 =                       sunit=0      swidth=0 blks
        naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
        log      =internal log           bsize=4096   blocks=2560, version=2
                 =                       sectsz=512   sunit=0 blks, lazy-count=1
        realtime =none                   extsz=4096   blocks=0, rtextents=0
        
        [root@localhost ~]# blkid /dev/vdb2
        /dev/vdb2: UUID="66251477-3ae4-4b44-8b21-5604420dbecb" TYPE="xfs"
        ```

    -   To create a TRFS file system, run the `mkfs.btrfs /dev/vdb2` command.

        ```
        [root@localhost ~]# mkfs.btrfs /dev/vdb2
        btrfs-progs v4.9.1
        See http://btrfs.wiki.kernel.org for more information.
        
        Label:              (null)
        UUID:               6fb5779b-57d7-4aaf-bf09-82b46f54a429
        Node size:          16384
        Sector size:        4096
        Filesystem size:    20.00GiB
        Block group profiles:
          Data:             single            8.00MiB
          Metadata:         DUP               1.00GiB
          System:           DUP               8.00MiB
        SSD detected:       no
        Incompat features:  extref, skinny-metadata
        Number of devices:  1
        Devices:
           ID        SIZE  PATH
            1    20.00GiB  /dev/vdb2
            
        [root@localhost ~]# blkid /dev/vdb2
        /dev/vdb2: UUID="6fb5779b-57d7-4aaf-bf09-82b46f54a429" UUID_SUB="9bdd889a-ab69-4653-a583-d1b6b8723378" TYPE="btrfs"
        ```

4.  Run the `mount /dev/vdb2 /mnt` command to mount the file system.
5.  Run the `df -h` command to view the current disk space and usage.

    The information of the new file system is displayed, indicating that the file system is mounted and you can use it.

    ```
    [root@localhost ~]# df -h
    Filesystem Size Used Avail Use% Mounted on
    /dev/vda1 40G 1.6G 36G 5% /
    devtmpfs 3.9G 0 3.9G 0% /dev
    tmpfs 3.9G 0 3.9G 0% /dev/shm
    tmpfs 3.9G 460K 3.9G 1% /run
    tmpfs 3.9G 0 3.9G 0% /sys/fs/cgroup
    /dev/vdb2 9.8G 37M 9.2G 1% /mnt
    tmpfs 783M 0 783M 0% /run/user/0
    ```


