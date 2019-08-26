# Extend the file system of the Linux system disk {#concept_ocb_htw_dhb .concept}

This topic describes how to use the growpart and resize2fs tools to resize the system disk and extend the file system of a Linux instance.

## Overview {#section_mzb_5l1_khb .section}

This topic uses the /dev/vda1 partition of the /dev/vda system disk as an example.

-   If you select **Resize Disk Online** when you [Resize a disk](intl.en-US/ECS/ECS conref warehouse/Resize a cloud disk online.md#), you can resize the disk only if a combination of the following conditions are met. For more information, see [Resize the system disk online](#).
    -   Partition format: mbr and gpt
    -   File system: ext, XFS, Btrfs, and UFS
    -   Operating system: The kernel version is V3.6.0 or later \(run the `uname -a` command to check the version\).
-   If the operating system is earlier than V3.6.0 \(for example CentOS 6, Debian 7, and SUSE Linux Enterprise Server 11 SP4\), you must restart the operating system before you can resize the system disk. For more information, see [Resize the system disk offline](#).

## Preparations {#section_h25_n5w_dhb .section}

1.  [Resize the disk](intl.en-US/ECS/ECS conref warehouse/Resize a cloud disk online.md#) by using the ECS console or calling the API.
2.  [Create a snapshot](intl.en-US/Snapshots/Use snapshots/Create a snapshot.md#) to back up data.
3.  Mount the disk to an ECS instance that is in the **Running** state. For information on how to connect to an ECS instance, see [Overview](../../../../intl.en-US/Instances/Connect to instances/Overview.md#).
4.  Install the required growpart tool according to your operating system.

    |Operating system|Growpart tool|
    |:---------------|:------------|
    |CentOS 7|     ```
yum install cloud-utils-growpart
    ```

 |
    |Aliyun Linux|
    |Ubuntu 14|     ```
apt install cloud-guest-utils
    ```

 |
    |Ubuntu 16|
    |Ubuntu 18|
    |Debian 9|
    |Debian 8|Use the upstream growpart tool.|
    |OpenSUSE 42.3|
    |OpenSUSE 13.1|
    |SUSE Linux Enterprise Server 12 SP2|


## Resize the system disk online {#section_gxq_3tw_dhb .section}

This procedure uses a CentOS 7 instance as an example to describe how to resize a partition online.

1.  Install the required growpart tool according to your operating system.

    ```
    [root@localhost ~]# yum install -y cloud-utils-growpart
    ```

2.  Run the `fdisk -l` command to view the current disk size. In this example, the disk size \(/dev/vda\) is 100 GiB.

    ```
    [root@localhost ~]# fdisk -l
    Disk /dev/vda: 107.4 GB, 107374182400 bytes, 209715200 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x0008d73a
       Device Boot      Start         End      Blocks   Id  System
    /dev/vda1   *        2048    41943039    20970496   83  Linux
    ```

3.  Run the `df -h` command to view the disk partition size. In this example, the disk partition size \(/dev/vda1\) is 20 GiB.

    ```
    [root@localhost ~]# df -h
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/vda1        20G  1.5G   18G   8% /
    devtmpfs        7.8G     0  7.8G   0% /dev
    tmpfs           7.8G     0  7.8G   0% /dev/shm
    tmpfs           7.8G  344K  7.8G   1% /run
    tmpfs           7.8G     0  7.8G   0% /sys/fs/cgroup
    tmpfs           1.6G     0  1.6G   0% /run/user/0
    ```

4.  Run the `growpart <DeviceName\><PartionNumber\>` command to call the growpart tool to resize the target system disk and partition. In this example, the first partition of the system disk is resized.

    ```
    [root@localhost ~]# growpart /dev/vda 1
    CHANGED: partition=1 start=2048 old: size=41940992 end=41943040 new: size=209710462,end=209712510
    ```

5.  Run the `resize2fs <PartitionName\>` command to call the resize2fs tool to extend the file system. In this example, the file system of the /dev/vda1 partition in the system disk is extended.

    ```
    [root@localhost ~]# resize2fs /dev/vda1
    resize2fs 1.42.9 (28-Dec-2013)
    Filesystem at /dev/vda1 is mounted on /; on-line resizing required
    old_desc_blocks = 2, new_desc_blocks = 7
    The filesystem on /dev/vda1 is now 26213807 blocks long.
    ```

6.  Run the `df -h` command to view the size of the disk partition. In this example, the returned partition size \(/dev/vda1\) is 100 GiB, which means that the partition is extended.

    ```
    [root@localhost ~]# df -h
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/vda1        99G  1.6G   93G   2% /
    devtmpfs        7.8G     0  7.8G   0% /dev
    tmpfs           7.8G     0  7.8G   0% /dev/shm
    tmpfs           7.8G  500K  7.8G   1% /run
    tmpfs           7.8G     0  7.8G   0% /sys/fs/cgroup
    tmpfs           1.6G     0  1.6G   0% /run/user/0
    ```


## Resize the system disk offline {#section_vxq_3tw_dhb .section}

This procedure uses a CentOS 6 instance as an example to describe how to resize a partition offline.

1.  Install the required growpart and dracut-modules-growroot tools according to your operating system.

    ```
    [root@AliYunOS ~]# yum install -y cloud-utils-growpart dracut-modules-growroot
    [root@AliYunOS ~]# dracut -f
    ```

2.  Run the `fdisk -l` command to view the current disk size. In this example, the disk size \(/dev/vda\) is 100 GiB.

    ```
    [root@AliYunOS ~]# fdisk -l
    Disk /dev/vda: 107.4 GB, 107374182400 bytes
    255 heads, 63 sectors/track, 13054 cylinders
    Units = cylinders of 16065 * 512 = 8225280 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk identifier: 0x0003a7b4
       Device Boot      Start         End      Blocks   Id  System
    /dev/vda1   *           1        2611    20970496   83  Linux
    ```

3.  Run the `df -h` command to view the disk partition size. In this example, the disk partition size \(/dev/vda1\) is 20 GiB.

    ```
    [root@AliYunOS ~]# df -h
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/vda1        20G  1.1G   18G   6% /
    tmpfs           7.8G     0  7.8G   0% /dev/shm
    ```

4.  Run the `growpart <DeviceName\><PartionNumber\>` command to call the growpart tool to resize the target system disk and partition. In this example, the first partition of the system disk is resized.

    ```
    [root@AliYunOS ~]# growpart /dev/vda 1
    CHANGED: partition=1 start=2048 old: size=41940992 end=41943040 new: size=209710462,end=209712510
    ```

5.  Restart the instance.

    ```
    [root@AliYunOS ~]# reboot
    ```

6.  Connect to the instance again.
7.  Run the `resize2fs <PartitionName\>` command to call the resize2fs tool to extend the file system. In this example, the file system of the /dev/vda1 partition in the system disk is extended.

    ```
    [root@AliYunOS ~]# resize2fs /dev/vda1
    resize2fs 1.41.12 (17-May-2010)
    Filesystem at /dev/vda1 is mounted on /; on-line resizing required
    old desc_blocks = 2, new_desc_blocks = 7
    Performing an on-line resize of /dev/vda1 to 26213807 (4k) blocks.
    The filesystem on /dev/vda1 is now 26213807 blocks long.
    ```

8.  Run the `df -h` command to view the size of the disk partition. In this example, the returned partition size \(/dev/vda1\) is 100 GiB, which means that the partition is extended.

    ```
    [root@AliYunOS ~]# fdisk -l
    Disk /dev/vda: 107.4 GB, 107374182400 bytes
    255 heads, 63 sectors/track, 13054 cylinders
    Units = cylinders of 16065 * 512 = 8225280 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk identifier: 0x0003a7b4
       Device Boot      Start         End      Blocks   Id  System
    /dev/vda1   *           1       13054   104855231   83  Linux
    [root@AliYunOS ~]# df -h
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/vda1        99G  1.1G   93G   2% /
    tmpfs           7.8G     0  7.8G   0% /dev/shm
    ```


