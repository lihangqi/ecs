# （Linux）在线扩容数据盘 {#concept_whh_zrd_pgb .concept}

当Linux实例的数据盘容量无法满足数据存储的需求时，您可以扩容数据盘。在线扩容数据盘不必重启实例即可完成扩容。

## 使用限制 {#section_ohl_xvs_qgb .section}

-   仅适用于状态为**使用中**的数据盘，且所挂载的实例状态。
-   仅支持I/O优化实例。
-   弹性裸金属服务器（神龙）不支持在线扩容。
-   仅SSD云盘和高效云盘支持在线扩容。扩容上限请参见[数据盘扩容上限](../../../../../cn.zh-CN/用户指南/云盘/扩容云盘/云盘扩容概述.md#section_hzp_wzv_42b)。

## 扩容场景 {#section_cbw_wxs_qgb .section}

以下是几类常见的扩容场景，请根据需要选择：

|场景|操作|
|:-|:-|
|数据盘已挂载到实例上|数据盘已分区并格式化|参考本文档的操作步骤完成扩容|
|空数据盘，未分区，未格式化|在控制台扩容磁盘空间后，[分区并格式化数据盘](../../../../../cn.zh-CN/个人版快速入门/步骤 4：格式化数据盘/Linux 格式化数据盘.md#)|
|数据盘已格式化，未分区|在控制台扩容磁盘空间后，[扩容文件系统](#)|
|数据盘未挂载到实例上|您可以：-   离线扩容数据盘。
-   先挂载数据盘到实例，然后在线扩容。

|

本示例中，数据盘为高效云盘，ECS实例的操作系统为CentOS 7.5 64 位。实例操作系统中的数据盘设备名为**/dev/vdb**，原有分区为**/dev/vdb1**。扩容前的数据盘容量为20 GiB，通过在线扩容变为40 GiB。您可以参考以下步骤扩容数据盘并使扩容后的容量可用：

1.  [在控制台上扩容数据盘](#)
2.  [连接实例确认数据盘的分区以及文件系统情况](#)
3.  [完成扩容](#)

## 准备工作 {#section_tcx_kn5_qgb .section}

1.  [创建快照](cn.zh-CN/用户指南/快照/创建快照.md#)以备份数据。
2.  数据盘已挂载到实例上，实例必须处于**运行中**状态。
3.  数据盘已做格式化和分区。具体操作请参见[Linux 格式化数据盘](../../../../../cn.zh-CN/个人版快速入门/步骤 4：格式化数据盘/Linux 格式化数据盘.md#)。

## 步骤1. 在控制台上扩容数据盘 {#section_s44_jlv_qgb .section}

1.  登录ECS管理控制台。
2.  勾选**在线扩容**，并设置 **扩容后容量**。

    **说明：** 扩容后的容量必须大于当前容量。

3.  确认费用，并单击 **确定扩容**。

    扩容成功后，磁盘列表中立即显示扩容后的容量。


## 步骤2. 确认数据盘的分区以及文件系统 {#section_tfj_pnv_qgb .section}

在ECS控制台上完成扩容后，数据盘容量已经增加，但是数据盘的分区和文件系统并未扩容，您需要连接实例先确认分区与文件系统，再按需完成扩容。

1.  运行`fdisk -lu /dev/vdb`确认数据盘是否分区。

    本示例中，原有的磁盘空间已做分区`/dev/vdb1`。

    ```
    # fdisk -lu /dev/vdb
    Disk /dev/vdb: 42.9 GB, 42949672960 bytes, 83886080 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x9277b47b
    
    Device Boot Start End Blocks Id System
    /dev/vdb1 2048 41943039 20970496 83 Linux
    
    ```

2.  运行`blkid /dev/vdb1`确认文件系统的类型。

    本示例中，`/dev/vdb1`的文件系统类型为ext4。

    ```
    # blkid /dev/vdb1
    /dev/vdb1: UUID="e97bf1e2-fc84-4c11-9652-73554546c324" TYPE="ext4"
    ```

    **说明：** 未分区并且未格式化的数据盘，以及已分区但未格式化的数据盘，不会返回结果。

3.  运行以下命令确认文件系统的状态。

    -   ext系列文件系统：`e2fsck -n <dst_dev_part_path>`
    -   xfs文件系统：`xfs_repair -n <dst_dev_part_path>`
    本示例中，文件系统状态为clean。如果状态不是clean，请排查并修复。

    ```
    # e2fsck -n /dev/vdb1
    e2fsck 1.42.9 (28-Dec-2013)
    Warning! /dev/vdb1 is mounted.
    Warning: skipping journal recovery because doing a read-only filesystem check.
    /dev/vdb1: clean, 11/1310720 files, 126322/5242624 blocks
    ```


## 步骤3. 完成扩容 {#section_pbr_xpv_qgb .section}

****如果新磁盘空间用于扩容已有的分区，按照以下步骤在实例中完成扩容：****

1.  修改分区表。

    **说明：** 

    -   为了防止数据丢失，不建议您对被挂载（mount）的分区和文件系统进行扩容。建议您先取消挂载（umount）数据盘，在完成扩容并正常使用后，再重新挂载（mount）。
    -   如果需要扩容的分区已经被挂载（mount），则操作如下：
        -   实例内核小于3.6：先将该分区umount，然后参考下述步骤修改分区表。
        -   实例内核版本大于等于3.6：修改分区表，然后运行`partx -u <dst_dev_path>`，以通知内核磁盘的分区表已经修改，需要同步更新。
    1.  运行`fdisk -lu /dev/vdb`，并记录旧分区的起始和结束的扇区位置。

        本示例中，/dev/vdb1的起始扇区位置是2048，结束扇区位置是41943039。

        ```
        # fdisk -lu /dev/vdb
        Disk /dev/vdb: 42.9 GB, 42949672960 bytes, 83886080 sectors
        Units = sectors of 1 * 512 = 512 bytes
        Sector size (logical/physical): 512 bytes / 512 bytes
        I/O size (minimum/optimal): 512 bytes / 512 bytes
        Disk label type: dos
        Disk identifier: 0x9277b47b
        
        Device Boot Start End Blocks Id System
        /dev/vdb1 2048 41943039 20970496 83 Linux
        ```

    2.  运行`fdisk`命令删除旧分区。

        1.  运行`fdisk -u /dev/vdb`：分区数据盘。
        2.  输入`p`：选择主分区。
        3.  输入`d`：删除分区。
        4.  输入`p`：确认分区已删除。
        5.  输入`w`：保存修改并退出。
        ```
        # fdisk -u /dev/vdb
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

    3.  运行`fdisk`命令新建分区。

        **说明：** 

        -   新分区的起始位置，必须和旧分区的起始位置相同。
        -   新分区的结束位置，必须大于旧分区的结束位置，否则会导致扩容失败。
        本示例中，将/dev/vdb1由20GiB扩容到40GiB。

        ```
        # fdisk -u /dev/vdb
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
        Syncing disks.
        ```

    4.  运行`e2fsck -n /dev/vdb1`再次检查文件系统，确认扩容分区后的文件系统状态为clean。
2.  扩容文件系统。
    -   ext系列文件系统（例如ext3和ext4）：运行`resize2fs /dev/vdb1`。

        ```
        # resize2fs /dev/vdb1
        resize2fs 1.42.9 (28-Dec-2013)
        Resizing the filesystem on /dev/vdb1 to 7864320 (4k) blocks.
        The filesystem on /dev/vdb1 is now 7864320 blocks long.
        ```

    -   xfs文件系统：先运行`mount /dev/vdb1 /mnt/`命令，再运行`xfs_growfs /dev/vdb1`。

        ```
        # mount /dev/vdb1 /mnt/
        
        # xfs_growfs /dev/vdb1
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


****如果新磁盘空间用于增加新的分区，按照以下步骤在实例中完成扩容：****

1.  运行`fdisk -u /dev/vdb`命令新建分区。

    本示例中，为新增的20GiB新建分区，作为/dev/vdb2。

    ```
    # fdisk -u /dev/vdb
    Welcome to fdisk (util-linux 2.23.2).
    
    Changes will remain in memory only, until you decide to write them.
    Be careful before using the write commad.
    
    
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

2.  运行命令`lsblk /dev/vdb`查看分区。

    ```
    # lsblk /dev/vdb
    NAME   MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
    vdb    253:16   0  40G  0 disk
    ├─vdb1 253:17   0  20G  0 part
    └─vdb2 253:18   0  20G  0 part
    ```

3.  格式化新的分区。
    -   创建ext4文件系统：`mkfs.ext4 /dev/vdb2`

        ```
        # mkfs.ext4 /dev/vdb2
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
        
        
        # blkid /dev/vdb2
        /dev/vdb2: UUID="e3f336dc-d534-4fdd-af71-b6ff1a55bdbb" TYPE="ext4"
        ```

    -   创建ext3文件系统：`mkfs.ext3 /dev/vdb2`

        ```
        # mkfs.ext3  /dev/vdb2
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
        
        
        # blkid /dev/vdb2
        /dev/vdb2: UUID="dd5be97d-a630-4593-9b0f-5056def914ea" SEC_TYPE="ext2" TYPE="ext3"
        ```

    -   创建xfs文件系统：`mkfs.xfs -f /dev/vdb2`

        ```
        # mkfs.xfs -f /dev/vdb2
        meta-data=/dev/vdb2              isize=512    agcount=4, agsize=1310720 blks
                 =                       sectsz=512   attr=2, projid32bit=1
                 =                       crc=1        finobt=0, sparse=0
        data     =                       bsize=4096   blocks=5242880, imaxpct=25
                 =                       sunit=0      swidth=0 blks
        naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
        log      =internal log           bsize=4096   blocks=2560, version=2
                 =                       sectsz=512   sunit=0 blks, lazy-count=1
        realtime =none                   extsz=4096   blocks=0, rtextents=0
        
        
        # blkid /dev/vdb2
        /dev/vdb2: UUID="66251477-3ae4-4b44-8b21-5604420dbecb" TYPE="xfs"
        ```

    -   创建trfs文件系统：`mkfs.btrfs /dev/vdb2`

        ```
        # mkfs.btrfs /dev/vdb2
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
            
        
        # blkid /dev/vdb2
        /dev/vdb2: UUID="6fb5779b-57d7-4aaf-bf09-82b46f54a429" UUID_SUB="9bdd889a-ab69-4653-a583-d1b6b8723378" TYPE="btrfs"
        ```

4.  运行`mount /dev/vdb2 /mnt`挂载文件系统。
5.  运行`df -h`查看目前磁盘空间和使用情况。

    显示新建文件系统的信息，表示挂载成功，您可以使用新的文件系统。

    ```
    # df -h
    Filesystem Size Used Avail Use% Mounted on
    /dev/vda1 40G 1.6G 36G 5% /
    devtmpfs 3.9G 0 3.9G 0% /dev
    tmpfs 3.9G 0 3.9G 0% /dev/shm
    tmpfs 3.9G 460K 3.9G 1% /run
    tmpfs 3.9G 0 3.9G 0% /sys/fs/cgroup
    /dev/vdb2 9.8G 37M 9.2G 1% /mnt
    tmpfs 783M 0 783M 0% /run/user/0
    ```


