# Format a data disk for Linux instance {#concept_jl1_qzd_wdb .concept}

If data disks are selected when you create an instance, you must format them and mount a file system before use. This document describes how to create a single-partition data disk using a new data disk and mount a file system. You can also configure multiple partitions based on service requirements.

This article applies only to partitioning a data disk that is not greater than 2 TiB using the `fdisk` command. If the data disk is greater than 2 TiB, refer to [Partition and format data disk larger than 2 TiB](../../../../reseller.en-US/User Guide/Cloud disks/Note.md#). We recommend that you use the built-in system tool for partitioning.

**Warning:** 

-   Disk partitioning and formatting are high-risk operations, so please proceed carefully. This article describes how to deal with a blank data disk. If you have data on a data disk, make sure that you have [created a snapshot of the data disk](../../../../reseller.en-US/User Guide/Snapshots/Create snapshots.md#) to avoid any possible data loss.

-   ECS instances only support partitioning the **data disks**, but not the **system disk**. If you use a third-party tool to forcibly partition the system disk, some unknown risks, such as system crash and data loss, may occur.


## Prerequisites {#section_dqp_xc2_wdb .section}

For a [data disk](../../../../reseller.en-US/User Guide/Cloud disks/Create a cloud disk.md#) purchased separately from an instance, you must [attach it to an instance](../../../../reseller.en-US/User Guide/Cloud disks/Attach a cloud disk.md#) in the ECS console before partitioning and formatting.

For data disks purchased with an instance, you do not have to mount them.

You need to know the device name of the data disk that will be mounted to the instance. You can find the device name of the data disk by going to **ECS Console** \> **Block Storage** \> **Disks** \> **\(Disk ID specific\) More** \> **Modify Atrributes**. By default, the device names are assigned by the system, starting from /dev/xvdb and arranged in the order /dev/xvdb−/dev/xvdz.

## Procedure {#section_xtx_yc2_wdb .section}

In this example, a single-partition data disk is created with a new 20 GiB data disk \(device name /dev/vdb\) and an ext3 file system is mounted. An I/O-optimized instance with the CentOS 6.8 operating system is used.

1.  [Connect to an instance](reseller.en-US/Quick Start for Entry-Level Users/Step 3: Connect to an instance.md#).

2.  Run the `fdisk -l` command to view the data disk. If you do not find /dev/vdb after running the command, it indicates that your instance does not have a data disk. Therefore, formatting is not required and you can skip the rest of this article.

    -   If your data disk shows dev/xvd?, you are using a non-I/O optimized instance. 

    -   ? is any letter from a−z. 

3.  Create a single-partition data disk and execute the following commands in sequence: 

    1.  Run `fdisk /dev/vdb` to partition the data disk.

    2.  Enter `n` and press the Enter key to create a new partition.

    3.  Enter `p` and press the Enter key to select the primary partition. In this example, you are creating a single-partition data disk, so it is sufficient to create one primary partition.

        **Note:** If you want to create more than four partitions, you should create at least one extended partition by selecting `e`.

    4.  Type the partition number and press the Enter key. In this example, `1` is entered.

    5.  Enter the first available sector number. Press the Enter key to use the default value of 1.

    6.  Type a number for the last sector. Because only one partition is created in this example, press the Enter key to use the default value.

    7.  Type `wq` and press the Enter key.

        ```
        [root@iXXXXXXX ~]# fdisk /dev/vdb
        Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
        Building a new DOS disklabel with disk identifier 0x5f46a8a2.
        Changes will remain in memory only, until you decide to write them.
        After that, of course, the previous content won't be recoverable.
        Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)
        WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
        switch off the mode (command 'c') and change display units to
        sectors (command 'u').
        Command (m for help): n
        Command action
        e extended
        p primary partition (1-4)
        p
        Partition number (1-4): 1
        First cylinder (1-41610, default 1): 1
        Last cylinder, +cylinders or +size{K,M,G} (1-41610, default 41610):
        Using default value 41610
        Command (m for help): wq
        The partition table has been altered!
        Calling ioctl() to re-read partition table.
        Syncing disks.
        ```

4.  Run the `fdisk -l` command to view the new partition. If the following information appears, the new partition /dev/vdb1 is created.

    ```
    [root@iXXXXXXX ~]# fdisk -l
    Disk /dev/vda: 42.9 GB, 42949672960 bytes
    255 heads, 63 sectors/track, 5221 cylinders
    Units = cylinders of 16065 * 512 = 8225280 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk identifier: 0x00053156
    Device Boot Start End Blocks Id System
    /dev/vda1 * 1 5222 41942016 83 Linux
    Disk /dev/vdb: 21.5 GB, 21474836480 bytes
    16 heads, 63 sectors/track, 41610 cylinders
    Units = cylinders of 1008 * 512 = 516096 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk identifier: 0x5f46a8a2
    Device Boot Start End Blocks Id System
    /dev/vdb1 1 41610 20971408+ 83 Linux
    ```

5.  Run the command `mkfs.ext3 /dev/vdb1` to create a file system on the new partition.

    -   In this example, an ext3 file system will be created. You can also choose to create other file systems according to your needs. For example, if you need to share files between Linux, Windows, and Mac, you can use `mkfs.vfat` to create a VFAT file system.

    -   The time required to create a file system depends on the data disk size.

        ```
        [root@iXXXXXXX ~]# mkfs.ext3 /dev/vdb1
        mke2fs 1.41.12 (17-May-2010)
        Filesystem label=
        OS type: Linux
        Block size=4096 (log=2)
        Fragment size=4096 (log=2)
        Stride=0 blocks, Stripe width=0 blocks
        1310720 inodes, 5242852 blocks
        262142 blocks (5.00%) reserved for the super user
        First data block=0
        Maximum filesystem blocks=4294967296
        160 block groups
        32768 blocks per group, 32768 fragments per group
        8192 inodes per group
        Superblock backups stored on blocks:
        32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
        4096000
        Writing inode tables: done
        Creating journal (32768 blocks): done
        Writing superblocks and filesystem accounting information: done
        This filesystem will be automatically checked every 37 mounts or
        180 days, whichever comes first. Use tune2fs -c or -i to override.
        ```

6.  \(Recommended\) Run the command `cp /etc/fstab  /etc/fstab.bak` to back up the data disk.

7.  Run the command `echo /dev/vdb1 /mnt ext3  defaults 0 0 >> /etc/fstab` to write new partition information to /etc/fstab.

    **Note:** Ubuntu 12.04 does not support barrier, so the correct command for this system is `echo '/dev/vdb1 /mnt ext3 barrier=0 0 0' >> /etc/fstab`.

    If you need to mount the data disk to a folder separately, for example, to store web pages separately, replace `/mnt` with the desired mount point path. 

8.  View the new partition information in /etc/fstab: Run the command `cat /etc/fstab`.

    ```
    [root@iXXXXXXX ~]# cat /etc/fstab
    #
    # /etc/fstab
    # Created by anaconda on Thu Feb 23 07:28:22 2017
    #
    # Accessible filesystems, by reference, are maintained under '/dev/disk'
    # See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
    #
    UUID=3d083579-f5d9-4df5-9347-8d27925805d4 / ext4 defaults 1 1
    tmpfs /dev/shm tmpfs defaults 0 0
    devpts /dev/pts devpts gid=5,mode=620 0 0
    sysfs /sys sysfs defaults 0 0
    proc /proc proc defaults 0 0
    /dev/vdb1 /mnt ext3 defaults 0 0
    ```

9.  Mount the file system: Run the command `mount /dev/vdb1 /mnt`.

     

10. To view disk space and usage: run the command `df -h`. If the new file system information appears in the returned results, the mount operation is successful and you can use the new file system.

    After mounting, you can use the new file system directly and do not need to restart the instance.

    ```
    [root@iXXXXXXX ~]# mount /dev/vdb1 /mnt
    [root@iXXXXXXX ~]# df -h
    Filesystem Size Used Avail Use% Mounted on
    /dev/vda1 40G 6.6G 31G 18% /
    tmpfs 499M 0 499M 0% /dev/shm
    /dev/vdb1 20G 173M 19G 1% /mnt
    ```


