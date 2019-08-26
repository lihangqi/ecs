# Format a data disk of a Linux instance {#concept_jl1_qzd_wdb .concept}

This topic describes how to format a data disk of a Linux instance. A newly created or purchased data disk cannot be used unless you format it, create one or more partitions in it, and mount a file system on it.

**Warning:** 

-   Disk partitioning and formatting are high-risk operations. Exercise caution when performing these operations. The following procedure uses a newly purchased data disk as an example. If you partition or format an existing data disk, make sure that you have [created a snapshot of the data disk](../../../../reseller.en-US/Snapshots/Use snapshots/Create a snapshot.md#) to avoid data loss.

-   Do not partition the system disk of an ECS instance. Failure to comply can result in unknown risks, such as system failure and data loss. You can only extend a partition of, or add a partition to a system disk after you resize the system disk. For more information, see [Extend the file system of the Linux system disk](../../../../reseller.en-US/Block Storage/Block storage/Resize cloud disks/Extend the file system of the Linux system disk.md#).


**Note:** The following procedure applies only to data disks less than 2 TiB. If your data disk is greater than 2 TiB, see [Partition and format data disk greater than 2 TiB](../../../../reseller.en-US/Block Storage/Block storage/Resize cloud disks/Extend the file system of the Linux system disk.md#).

## Prerequisites {#section_uyv_5wy_wyy .section}

-   The ECS instance is [attached with a data disk](../../../../reseller.en-US/Block Storage/Block storage/Attach a cloud disk.md#) that was [created separately](../DNA0011894323/EN-US_TP_9669.dita#concept_jx1_tx1_ydb). You do not need to perform this operation for data disks created along with ECS instances.
-   The device name of the data disk is obtained.

    You can obtain the device name of the data disk by choosing **ECS Console** \> **Block Storage** \> **Disks** \> **\(Disk ID specific\) More** \> **Modify Attributes**.

    **Note:** By default, device names are assigned by the system. The device name for I/O-optimized instances starts from /dev/vdb to /dev/vdz. If the device name is `dev/xvd*` \(where, `*` is a lowercase letter\), then a non-I/O-optimized instance is being used.


## Procedure {#section_xtx_yc2_wdb .section}

In this example, a new 20 GiB data disk with the device name of /dev/vdb is used to create a single-partition data disk and format the disk to an ext4 file system. An I/O-optimized instance with CentOS 7.6 is used.

1.  [Connect to the instance](reseller.en-US/Quick Start for Entry-Level Users/Step 3: Connect to an instance.md#) to which the data disk is attached.

2.  Run the `fdisk -l` command to view the data disks of the instance.

**Note:** If /dev/vdb is not displayed in the output, no data disk is attached to the instance. In this case, check whether a data disk is mounted to the instance.

3.  Create a single-partition data disk by running the following commands in sequence:

    1.  Run the `fdisk -u /dev/vdb` command to partition the data disk.

    2.  Enter `p` and press **Enter** to view the partitions of the data disk. In this example, the data disk is not partitioned.

    3.  Enter `n` and press **Enter** to create a new partition.

    4.  Enter `p` and press **Enter** to select the primary partition.

        **Note:** In this example, you are creating a single-partition data disk, so you only need to create one primary partition. If you want to create four or more partitions, you must create at least one extended partition by selecting `e`.

    5.  Enter the partition number and press **Enter**. In this example, enter `1`.

    6.  Enter a number for the first available sector, or press **Enter** to use the default value of 2048.

    7.  Press **Enter** to use the default number for the last sector.

    8.  Enter `p` and press **Enter** to view the planned partitions of the data disk.
    9.  Enter `w` and press **Enter** to start partitioning and exit after partitioning.

        ``` {#codeblock_yey_mlu_783}
        [root@ecshost~ ]# fdisk -u /dev/vdb
        Welcome to fdisk (util-linux 2.23.2).
        Changes will remain in memory only, until you decide to write them.
        Be careful before using the write command.
        Device does not contain a recognized partition table
        Building a new DOS disklabel with disk identifier 0x3e60020e.
        
        Command (m for help): p
        Disk /dev/vdb: 21.5 GB, 21474836480 bytes, 41943040 sectors
        Units = sectors of 1 * 512 = 512 bytes
        Sector size (logical/physical): 512 bytes / 512 bytes
        I/O size (minimum/optimal): 512 bytes / 512 bytes
        Disk label type: dos
        Disk identifier: 0x3e60020e
        Device Boot Start End Blocks Id System
        
        Command (m for help): n
        Partition type:
        p primary (0 primary, 0 extended, 4 free)
        e extended
        Select (default p): p
        Partition number (1-4, default 1): 1
        First sector (2048-41943039, default 2048):
        Using default value 2048
        Last sector, +sectors or +size{K,M,G} (2048-41943039, default 41943039):
        Using default value 41943039
        Partition 1 of type Linux and of size 20 GiB is set
        
        Command (m for help): p
        
        Disk /dev/vdb: 21.5 GB, 21474836480 bytes, 41943040 sectors
        Units = sectors of 1 * 512 = 512 bytes
        Sector size (logical/physical): 512 bytes / 512 bytes
        I/O size (minimum/optimal): 512 bytes / 512 bytes
        Disk label type: dos
        Disk identifier: 0x3e60020e
        Device Boot Start End Blocks Id System
        /dev/vdb1 2048 41943039 20970496 83 Linux
        
        Command (m for help): w
        The partition table has been altered!
        
        Calling ioctl() to re-read partition table.
        Syncing disks.
        ```

4.  Run the `fdisk -lu /dev/vdb` command to view the new partition.

    If the following information is displayed, the new partition `/dev/vdb1` is created successfully.

    ``` {#codeblock_ra4_kha_cb0}
    [root@ecshost~ ]# fdisk -lu /dev/vdb
    
    Disk /dev/vdb: 21.5 GB, 21474836480 bytes, 41943040 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x3e60020e
    
    Device Boot Start End Blocks Id System
    /dev/vdb1 2048 41943039 20970496 83 Linux
    ```

5.  Run the `mkfs.ext4 /dev/vdb1` command to create an ext4 file system on the new partition.

    **Note:** You can also create other file systems as needed. For example, if you need to share files among different operating systems, such as Linux, Windows, and macOS, you can run the `mkfs.vfat` command to create a VFAT file system. The time required to create a file system depends on the data disk size.

    ``` {#codeblock_ims_1va_6g9}
    [root@ecshost~ ]# mkfs.ext4 /dev/vdb1
    mke2fs 1.42.9 (28-Dec-2013)
    Filesystem label=
    OS type: Linux
    Block size=4096 (log=2)
    Fragment size=4096 (log=2)
    Stride=0 blocks, Stripe width=0 blocks
    1310720 inodes, 5242624 blocks
    262131 blocks (5.00%) reserved for the super user
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
    ```

6.  \(Recommended\) Run the command `cp /etc/fstab /etc/fstab.bak` to back up etc/fstab.

7.  Run the command `echo /dev/vdb1 /mnt ext4 defaults 0 0 >> /etc/fstab` to write the new partition information to /etc/fstab.

    **Note:** 

    -   Ubuntu 12.04 does not support barrier. Therefore, the correct command for this system is `echo '/dev/vdb1 /mnt ext4 barrier=0 0 0' >> /etc/fstab`.
    -   If you need to mount the data disk to a folder to store web pages separately, replace `/mnt` with the desired mount point path.
8.  Run the `cat /etc/fstab` command to view the new partition information in /etc/fstab.

    ``` {#codeblock_cpk_9bz_pd6}
    [root@ecshost~ ]# cat /etc/fstab
    #
    # /etc/fstab
    # Created by anaconda on Wed Dec 12 07:53:08 2018
    #
    # Accessible filesystems, by reference, are maintained under '/dev/disk'
    # See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
    #
    UUID=d67c3b17-255b-4687-be04-f29190d37396 / ext4 defaults 1 1
    /dev/vdb1 /mnt ext4 defaults 0 0
    ```

9.  Run the `mount /dev/vdb1 /mnt` command to mount the file system.

10. Run the `df -h` command to view the disk space and usage.

    **Note:** If the new file system information is displayed in the response message, the file system is successfully mounted, and you can use the new file system without restarting the instance.

    ``` {#codeblock_lo8_nfi_1s6}
    [root@ecshost~ ]# df -h
    Filesystem Size Used Avail Use% Mounted on
    /dev/vda1 40G 1.6G 36G 5% /
    devtmpfs 234M 0 234M 0% /dev
    tmpfs 244M 0 244M 0% /dev/shm
    tmpfs 244M 484K 244M 1% /run
    tmpfs 244M 0 244M 0% /sys/fs/cgroup
    tmpfs 49M 0 49M 0% /run/user/0
    /dev/vdb1 20G 45M 19G 1% /mnt
    ```


