# Linux \_ Format and mount a data disk {#concept_jl1_qzd_wdb .concept}

If you select a data disk when creating an instance, you must format the data disk before using it. This article describes how to create a single-partition data disk using a new data disk and mount a file system.

This article only applies to partitioning a data disk less than 2 TiB using the `fdisk` command. If you want to partition a data disk more than 2 TiB, see [Partition and format data disk more than 2 TiB](../../../../intl.en-US/User Guide/Cloud disks/Partition and format data disk more than 2 TB.md#).

You can also configure multiple data disk partitions based on service requirements. We recommend that you use the built-in system tool for partitioning.

**Warning:** For ECS, either running Windows or Linux, only the partitions on the data disk, but not on the system disk, can be subdivided into multiple partitions. If you use a third-party tool to forcibly subdivide the partition on the system disk, some unknown risks, such as system crash and data loss, may occur.

In this article, the example instance has the following configurations:

-   Non-I/O-optimized:

    **Note:** The only difference between I/O-Optimized and non-I/O-Optimized instances is that the latter has an additional x in its device name, for example, xvdb for a non-I/O-optimized instance and vdb for an I/O-optimized instance.

-   Linux OS: Red Hat, CentOS, Debian, or Ubuntu, at your choice
-   SSD Cloud Disk

## Prerequisites {#section_dqp_xc2_wdb .section}

-   At least one data disk has been attached to the Linux ECS instance. For more information, see [Attach a cloud disk](../../../../intl.en-US/User Guide/Cloud disks/Attach a cloud disk.md#).
-   You have connected to your instance. For more information, see [Connect to an instance](intl.en-US/Quick Start for Entry-Level Users/Step 3. Connect to an instance.md#).

## Procedure {#section_xtx_yc2_wdb .section}

To format and mount a data disk:

1.  Run the `fdisk -l` command to view the data disk.

    **Note:** Before the data disk is partitioned and formatted, you cannot view the data disk by running the `df –h` command.

    In the following example, a 5 GiB data disk needs to be mounted. If you do not find /dev/xvdb after running the `fdisk -l` command, it indicates that your instance does not have a data disk. Therefore, mounting is not required. In this case, you can skip this chapter.

    ```
    [root@xxxx ~]# fdisk -l
    Disk /dev/xvda: 42.9 GB, 42949672960 bytes
    255 heads, 63 sectors/track, 5221 cylinders
    Units = cylinders of 16065 * 512 = 8225280 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk identifier: 0x00078f9c
    Device Boot Start End Blocks Id System
    /dev/xvda1 * 1 5222 41940992 83 Linux
    Disk /dev/xvdb: 5368 MB, 5368709120 bytes
    255 heads, 63 sectors/track, 652 cylinders
    Units = cylinders of 16065 * 512 = 8225280 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk identifier: 0x00000000
    ```

2.  Run the following command to partition the data disk.

    ```
    fdisk /dev/xvdb
    ```

3.  Enter the commands `n`, `p`, `1` in sequence as prompted, press the Enter key twice, and then enter the `wq` command. The partitioning will begin.

    ```
    [root@xxx ~]# fdisk /dev/xvdb
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0x33eb5059.
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
    First cylinder (1-652, default 1): 
    Using default value 1
    Last cylinder, +cylinders or +size{K,M,G} (1-652, default 652):
    Using default value 652
    Command (m for help): wq
    The partition table has been altered!
    Calling ioctl() to re-read partition table.
    Syncing disks.
    ```

4.  Run the `fdisk -l` command to view the new partition. A new partition is created, for example, /dev/xvdb1 shown in the following example.

    ```
    [root@xxx ~]# fdisk -l
    Disk /dev/xvda: 42.9 GB, 42949672960 bytes
    255 heads, 63 sectors/track, 5221 cylinders
    Units = cylinders of 16065 * 512 = 8225280 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk identifier: 0x00078f9c
    Device Boot Start End Blocks Id System
    /dev/xvda1 * 1 5222 41940992 83 Linux
    Disk /dev/xvdb: 5368 MB, 5368709120 bytes
    255 heads, 63 sectors/track, 652 cylinders
    Units = cylinders of 16065 * 512 = 8225280 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk identifier: 0x33eb5059
    Device Boot Start End Blocks Id System
    /dev/xvdb1 1 652 5237158+ 83 Linux
    ```

5.  Run the following command to format the new partition. The formatting time depends on the size of the data disk. You can also choose other file formats, for example, ext4.

    ```
    mkfs.ext3 /dev/xvdb1
    ```

6.  Run the following command to write the new partition information.

    ```
    echo '/dev/xvdb1 /mnt ext3 defaults 0 0'>> /etc/fstab
    ```

    Upon completion, run the cat /etc/fstab command to view the information.

    **Note:** Ubuntu 12.04 does not support barrier. Therefore, the correct command for the system is as follows:

    ```
    echo '/dev/xvdb1 /mnt ext3 barrier=0 0 0'>>/etc/fstab
    ```

    To mount the data disk to a folder separately, for example, to store webpages separately, modify the /mnt part in the preceding command.

7.  Run the `mount /dev/xvdb1 /mnt` command to mount the new partition. Then, run the `df -h` command to view the partition. If data disk information is displayed, the new partition has been mounted successfully and can be used.

    ```
    [root@xxx ~]# mount /dev/xvdb1 /mnt
    [root@xxx ~]# df -h
    Filesystem Size Used Avail Use% Mounted on
    /dev/xvda1 40G 1.5G 36G 4% /
    tmpfs 498M 0 498M 0% /dev/shm
    /dev/xvdb1 5.0G 139M 4.6G 3% /mnt
    ```

    **Note:** ECS does not support installation and deployment of virtualization software, for example, KVM, Xen, and VMware.


