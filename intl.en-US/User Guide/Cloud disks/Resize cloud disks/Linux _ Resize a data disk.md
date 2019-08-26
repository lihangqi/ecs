# Linux - Resize a data disk {#concept_z11_xsh_ydb .concept}

As your business grows, the current capacity of your data disks may not be able to meet your data storage needs. You can use the **Resize Disk** feature to resize your data disks as necessary.

**Note:** 

-   Resize the data disks that are attached to an instance only when the instance is in the **Running** or **Stopped** status. You must restart the instance in the ECS console to apply the changes. This action causes your instance to stop working and may cause your business to be interrupted, so please proceed with caution.
-   We recommend that you manually create a snapshot to back up your data before resizing your data disk.
-   You can resize a data disk when the data disk is either in the **Available** status or in the **In Use** status.
-   If you have renewed a Subscription ECS instance for configration downgrade \([renew for configuration downgrade](../../../../reseller.en-US/Pricing/Renew instances/Renew for configuration downgrade.md#) \), during its current billing cycle, you cannot resize the attached Subscription cloud disks, including its data or system disks.
-   If a snapshot is being created for a data disk, you cannot resize the data disk.
-   You can resize data disks, but not system disks or local disks.

This example uses a data disk of the ultra cloud disk type and an ECS instance running 64-bit CentOS 7.3 to describe how to resize data disk and extend the available capacity.

To resize a data disk, follow these steps:

[Step 1. Increase the size of a data disk in the ECS console](#)

[Step 2. Log on to the instance to resize the file system](#)

## Step 1. Increase the size of a data disk in the ECS console {#ResizeInConsole .section}

To increase the size of a data disk in the ECS console, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Block Storage** \> **Disks**.

    **Note:** If the data disk you want to resize has been attached to an instance, in the left-side navigation pane, click **Instances**, find the corresponding instance, go to the instance details page, and click **Disks**.

3.  Select a region.
4.  Find the disk to be resized, and in the **Actions** column, select **More** \> **Resize Disk.**.
5.  On the Resize Disk page, set **Capacity after resizing** \(in this example, 30 GiB\). The capacity after resizing must be larger than the current capacity.
6.  When the cost is calculated, click **Confirm to resize**.

    **Note:** After the resizing, you can view the new disk size in the console. However, if the data disk is attached to an ECS instance, you must [restart the instance](reseller.en-US/User Guide/Instances/Restart an instance.md#) in the ECS console to view the new disk size when you log on to the instance.


After the disk size is increased,

-   If the data disk is attached to an instance, [log on to the instance to resize the file system](reseller.en-US/User Guide/Cloud disks/Resize cloud disks/Linux - Resize a data disk.md#ResizeInInstance).
-   If the data disk is not attached to an instance, attach the disk to an instance in the console \([attach a cloud disk](reseller.en-US/User Guide/Cloud disks/Attach a cloud disk.md#)\) first, and then proceed depending on the data disk:
    -   If it is a new data disk, which has not been formatted, format it. For more information, see [format a data disk for Linux instances](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 4. Format a data disk/Format a data disk for Linux instance.md#).
    -   If it has been formatted and partitioned, [log on to the instance to resize the file system](reseller.en-US/User Guide/Cloud disks/Resize cloud disks/Linux - Resize a data disk.md#ResizeInInstance).

## Step 2. Log on to the instance to resize the file system {#ResizeInInstance .section}

After the disk size is increased, you must log on to the instance to resize the file system.

In this example, the data disk is attached to a Linux instance running the 64-bit CentOS 7.3. The data disk before resizing has only one primary partition \(/dev/vdb1, ext4 file system\), the mount point of the file system is /resizetest, and after resizing is completed, the data disk still has only one primary partition.

1.  [Connect to a Linux instance by using a password](reseller.en-US/User Guide/Connect to instances/Connect to a Linux instance by using a password.md#).
2.  Run the `umount [file system name]` command to unmount the primary partition.

    ```
    umount /dev/vdb1
    ```

    **Note:** Run the `df -h` command to check whether the unmounting is successful. If you do not see the /dev/vdb1 information, unmounting is successful. The following is the sample output.

    ```
    [root@iXXXXXX ~]# df -h
    Filesystem Size Used Avail Use% Mounted on
    /dev/vda1 40G 1.5G 36G 4% /
    devtmpfs 487M 0 487M 0% /dev
    tmpfs 497M 0 497M 0% /dev/shm
    tmpfs 497M 312K 496M 1% /run
    tmpfs 497M 0 497M 0% /sys/fs/cgroup
    tmpfs 100M 0 100M 0% /run/user/0
    ```

3.  Run the `fdisk` command to delete the original partition and create a new partition:

    **Note:** If you use the `parted` tool to manipulate partitions, you cannot use it in conjunction with `fdisk`. Otherwise, this results in an inconsistent first sector of the partition.  Instructions on how to use the `parted` tool can be found [here](#parted).

    1.  Run the `fdisk -l` command to list the partition details and record the final size of the partition and its first sector before resizing.
    2.  Run the `fdisk [device name of data disk]` command to go to `fdisk` . In this example, the device name is `/dev/vdb`.
    3.  Type `d` and press the Enter key to delete the original partition.

        **Note:** Deleting a partition does not cause loss of data in the data disk.

    4.  Type `d` and press the Enter key to start creating a new partition.
    5.  Type `p` and press the Enter key to create a primary partition. In this example, you are creating a single-partition data disk, so it is sufficient to create one primary partition.

        **Note:** If you want to create more than four partitions, create at least one extended partition, that is, type `e`.

    6.  Type the partition number and press the Enter key. In this example, only one partition is to be created, so type 1.
    7.  Type a number for the First sector: For data consistency, the number for the First sector must be identical with that of the original partition. In this example, press the Enter key to use the default value of 1.

        **Note:** If you find that the First sector is not identical with the recorded one, you may have used the `parted` tool for partitioning. In that case, stop the current `fdisk` operation and use [`parted`](#parted) to start over again. 

    8.  Type a number for the last sector: Because only one partition is to be created in this example, press the Enter key to use the default value.
    9.  Type `wq` and press the Enter key to start partitioning.

        ```
        [root@iXXXXXX ~]# fdisk /dev/vdb
        Welcome to fdisk (util-linux 2.23.2).
        Changes will remain in memory only, until you decide to write them.
        Be careful before using the write command.
        Command (m for help): d
        Selected partition 1
        Partition 1 is deleted
        Command (m for help): n
        Partition type:
        p primary (0 primary, 0 extended, 4 free)
        e extended
        Select (default p):
        Using default response p
        Partition number (1-4, default 1):
        First sector (2048-62914559, default 2048):
        Using default value 2048
        Last sector, +sectors or +size{K,M,G} (2048-62914559, default 62914559):
        Using default value 62914559
        Partition 1 of type Linux and of size 30 GiB is set
        Command (m for help): wq
        The partition table has been altered!
        Calling ioctl() to re-read partition table.
        Syncing disks.
        ```

        **Note:** If you are using the `parted` tool, type `p` in the `parted` window to list the current partition details. If any partition is displayed, use rm + serial number to delete the original partition table, then run the `unit s` command to specify the start unit, calculated by the number of sectors, and finally run the `mkpart` command to create it, as shown in the following figure.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9677/15453934715353_en-US.png)

4.  For some operating systems, the file system may be automatically mounted to the mount point after partitioning. We recommend that you run the `df -h` command to check the file system space and usage. Run the `umount [file system name]` to unmount the file system again.
5.  Check the file system and resize the file system.

    ```
    e2fsck -f /dev/vdb1 # check the file system
    resize2fs /dev/vdb1 # resize the file system
    
    
    ```

    **Note:** 

    -   Running the `e2fsck` command is time-consuming because the system needs to check and revise the file system metadata during that process, so be patient.
    -   Properly running the `e2fsck` command and the `resize2fs` command does not cause data loss.
    The following is the sample output.

    ```
    [root@iXXXXXX ~]# e2fsck -f /dev/vdb1
    e2fsck 1.42.9 (28-Dec-2013)
    Pass 1: Checking inodes, blocks, and sizes
    Pass 2: Checking directory structure
    Pass 3: Checking directory connectivity
    Pass 4: Checking reference counts
    Pass 5: Checking group summary information
    /dev/vdb1: 11/1835008 files (0.0% non-contiguous), 159218/7339776 blocks
    [root@iXXXXXX ~]# resize2fs /dev/vdb1
    resize2fs 1.42.9 (28-Dec-2013)
    Resizing the filesystem on /dev/vdb1 to 7864064 (4k) blocks.
    The filesystem on /dev/vdb1 is now 7864064 blocks long.
    ```

6.  Mount the resized file system to the original mount point \(in this example, /resizetest\).

    ```
    mount /dev/vdb1 /resizetest
    ```

7.  Run the `df -h` command to check file system space and usage. If the correct information about the resized file system is displayed, the mounting is successful and the resized file system is ready for use.

    **Note:** After the mounting is completed, you can use the resized file system without restarting the instance.

    The following is the sample output.

    ```
    [root@iXXXXXX ~]# df -h
    Filesystem Size Used Avail Use% Mounted on
    /dev/vda1 40G 1.5G 36G 4% /
    devtmpfs 487M 0 487M 0% /dev
    tmpfs 497M 0 497M 0% /dev/shm
    tmpfs 497M 312K 496M 1% /run
    tmpfs 497M 0 497M 0% /sys/fs/cgroup
    tmpfs 100M 0 100M 0% /run/user/0
    /dev/vdb1 30G 44M 28G 1% /resizetest
    ```


