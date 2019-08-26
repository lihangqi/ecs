# 扩展分区和文件系统\_Linux数据盘 {#concept_z11_xsh_ydb .concept}

扩容云盘只是扩大存储容量，不会扩容文件系统，您需要按照本文步骤扩容文件系统，实现ECS实例存储空间的扩展。

## 准备工作 {#section_vjz_tg3_vlw .section}

在扩展数据盘扩展分区和文件系统前，请提前完成以下工作。

1.  [创建快照](intl.zh-CN/快照/使用快照/创建快照.md#)以备份数据，防止操作失误导致数据丢失。
2.  通过ECS控制台或者API[扩容云盘容量](intl.zh-CN/块存储/云盘/扩容云盘/离线扩容云盘.md#)。
3.  远程连接ECS实例。连接方式请参见[连接方式导航](../../../../intl.zh-CN/实例/连接实例/连接方式导航.md#)。

## 确认分区格式和文件系统 {#section_jdz_a9a_my1 .section}

本示例中，数据盘采用高效云盘，ECS实例的操作系统为CentOS 7.5 64 位，数据盘设备名为/dev/vdb。

1.  运行`fdisk -lu <DeviceName\>`确认数据盘是否分区。

    本示例中，原有的数据盘空间已做分区/dev/vdb1。`"System"="Linux"`说明数据盘使用的是MBR分区格式，如果`"System"="GPT"`则说明数据盘使用的是GPT格式。

    ``` {#codeblock_rt0_ob6_ww6 .lanuage-shell}
    [root@ecshost ~]# fdisk -lu /dev/vdb
    Disk /dev/vdb: 42.9 GB, 42949672960 bytes, 83886080 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x9277b47b
    
    Device Boot Start End Blocks Id System
    /dev/vdb1 2048 41943039 20970496 83 Linux
    ```

2.  运行`blkid <PartionName\>`确认文件系统的类型。

    本示例中，/dev/vdb1的文件系统类型为ext4。 

    ``` {#codeblock_mxg_qw8_ocw .lanuage-shell}
    [root@ecshost ~]# blkid /dev/vdb1
    /dev/vdb1: UUID="e97bf1e2-fc84-4c11-9652-73********24" TYPE="ext4"
    ```

    **说明：** 未分区并且未创建文件系统的数据盘，以及已分区但未创建文件系统的数据盘，不会返回结果。

3.  运行以下命令确认文件系统的状态。

    -   ext\*文件系统：`e2fsck -n <dst\_dev\_part\_path\>`
    -   xfs文件系统：`xfs_repair -n <dst\_dev\_part\_path\>`
    本示例中，文件系统状态为clean。如果状态不是clean，请排查并修复。

    ``` {#codeblock_i6g_2gi_2bs .lanuage-shell}
    [root@ecshost ~]# e2fsck -n /dev/vdb1
    e2fsck 1.42.9 (28-Dec-2013)
    Warning! /dev/vdb1 is mounted.
    Warning: skipping journal recovery because doing a read-only filesystem check.
    /dev/vdb1: clean, 11/1310720 files, 126322/5242624 blocks
    ```


## 选择分区或文件系统扩容方式 {#section_2ua_pt6_4qe .section}

根据您查询到的分区格式和文件系统情况确定操作选项。

|扩容场景|相关操作|
|----|----|
|数据盘已分区并创建文件系统| -   如果您需要扩展数据盘已有的MBR分区，请参见[选项一：扩展已有MBR分区](#)。
-   如果新增空间用于增加新的MBR分区，请参见[选项二：新增并格式化MBR分区](#)。
-   如果您需要扩展数据盘已有的GPT分区，请参见[选项三：扩展已有GPT分区](#)。
-   如果新增空间用于增加新的GPT分区，请参见[选项四：新增并格式化GPT分区](#)。

 |
|全新数据盘，未分区，未创建文件系统|在控制台扩容磁盘空间后，参见[分区并格式化数据盘](../../../../intl.zh-CN/个人版快速入门/格式化数据盘/Linux格式化数据盘.md#)或者[分区格式化大于2 TiB云盘](intl.zh-CN/块存储/云盘/分区格式化数据盘/分区格式化大于2 TiB数据盘.md#)。|
|数据盘已创建文件系统，未分区|在控制台扩容数据盘空间后，直接[扩容文件系统](#)。|
|数据盘未挂载到实例上|挂载数据盘到实例后，参见本文档的操作步骤完成扩容。|

**说明：** 如果一个已有分区采用了MBR分区格式，则不支持扩容到2 TiB及以上。为避免造成数据丢失，建议您创建一块大于2 TiB的云盘，参见[分区格式化大于2 TiB云盘](intl.zh-CN/块存储/云盘/分区格式化数据盘/分区格式化大于2 TiB数据盘.md#)格式化一个GPT分区，再将MBR分区中的数据拷贝到GPT分区中。

## 选项一：扩展已有MBR分区 {#section_vvb_gcs_bhm .section}

**说明：** 为了防止数据丢失，不建议扩容已挂载的分区和文件系统。请先取消挂载（umount）分区，完成扩容并正常使用后，重新挂载（mount）。针对不同的Linux内核版本，推荐以下操作方式：

-   实例内核版本 < 3.6：先取消挂载该分区，再修改分区表，最后扩容文件系统。
-   实例内核版本 ≥ 3.6：先修改对应分区表，再通知内核更新分区表，最后扩容文件系统。

如果新增空间用于扩容已有的MBR分区，按照以下步骤在实例中完成扩容：

步骤一：修改分区表

1.  运行`fdisk -lu /dev/vdb`，并记录旧分区的起始和结束的扇区位置。

    本示例中，/dev/vdb1的起始扇区是2048，结束扇区是41943039。

    ``` {#codeblock_y7s_lg2_9mv .lanuage-shell}
    [root@ecshost ~]# fdisk -lu /dev/vdb
    Disk /dev/vdb: 42.9 GB, 42949672960 bytes, 83886080 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x9277b47b
    
    Device Boot Start End Blocks Id System
    /dev/vdb1 2048 41943039 20970496 83 Linux
    ```

2.  查看数据盘的挂载路径，根据返回的文件路径卸载分区，直至完全卸载已挂载的分区。

    ``` {#codeblock_jag_max_se7 .lanuage-shell}
    [root@ecshost ~]# mount | grep "/dev/vdb"
    /dev/vdb1 on /mnt type ext4 (rw,relatime,data=ordered)
    [root@ecshost ~]# umount /dev/vdb1
    [root@ecshost ~]# mount | grep "/dev/vdb"
    ```

3.  使用fdisk工具删除旧分区。

    1.  运行`fdisk -u /dev/vdb`：分区数据盘。
    2.  输入p：打印分区表。
    3.  输入d：删除分区。
    4.  输入p：确认分区已删除。
    5.  输入w：保存修改并退出。
    ``` {#codeblock_28y_5ck_z16 .lanuage-shell}
    [root@ecshost ~]# fdisk -u /dev/vdb
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

4.  使用fdisk命令新建分区。

    1.  运行`fdisk -u /dev/vdb`：分区数据盘。
    2.  输入p：打印分区表。
    3.  输入n：新建分区。
    4.  输入p：选择分区类型为主分区。
    5.  输入<分区号\>：选择分区号。本示例选取了1。

        **警告：** 新分区的起始位置必须和旧分区的起始位置相同，结束位置必须大于旧分区的结束位置，否则会导致扩容失败。

    6.  输入w：保存修改并退出。
    本示例中，将/dev/vdb1由20 GiB扩容到40 GiB。

    ``` {#codeblock_a4w_96v_3of .lanuage-shell}
    [root@ecshost ~]# fdisk -u /dev/vdb
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

5.  运行`lsblk /dev/vdb`确保分区表已经增加。
6.  运行`e2fsck -n /dev/vdb1`再次检查文件系统，确认扩容分区后的文件系统状态为clean。

步骤二：通知内核更新分区表

运行`partprobe <dst_dev_path>`或者`partx -u <dst_dev_path>`，以通知内核数据盘的分区表已经修改，需要同步更新。

步骤三：扩容文件系统

-   ext\*文件系统（例如ext3和ext4）：运行`resize2fs /dev/vdb1`并重新挂载分区。

    ``` {#codeblock_e7j_9x0_xf4 .lanuage-shell}
    [root@ecshost ~]# resize2fs /dev/vdb1
    resize2fs 1.42.9 (28-Dec-2013)
    Resizing the filesystem on /dev/vdb1 to 7864320 (4k) blocks.
    The filesystem on /dev/vdb1 is now 7864320 blocks long.
    [root@ecshost ~]# mount /dev/vdb1 /mnt
    ```

-   xfs文件系统：先运行`mount /dev/vdb1 /mnt/`命令，再运行`xfs_growfs /dev/vdb1`。

    ``` {#codeblock_5e0_g7h_otl .lanuage-shell}
    [root@ecshost ~]# mount /dev/vdb1 /mnt/
    [root@ecshost ~]# xfs\_growfs /dev/vdb1
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


## 选项二：新增并格式化MBR分区 {#section_gg7_ilv_h3j .section}

如果新增空间用于增加新的MBR分区，按照以下步骤在实例中完成扩容：

1.  运行`fdisk -u /dev/vdb`命令新建分区。

    本示例中，为新增的20 GiB新建分区，作为/dev/vdb2使用。

    ``` {#codeblock_or8_07t_e4r .lanuage-shell}
    [root@ecshost ~]# fdisk -u /dev/vdb
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

    ``` {#codeblock_3u7_ycf_95m .lanuage-shell}
    [root@ecshost ~]# lsblk /dev/vdb
    NAME   MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
    vdb    253:16   0  40G  0 disk
    ├─vdb1 253:17   0  20G  0 part
    └─vdb2 253:18   0  20G  0 part
    ```

3.  格式化新的分区。
    -   创建ext4文件系统：`mkfs.ext4 /dev/vdb2` 

        ``` {#codeblock_bzg_w8d_3pe .lanuage-shell}
        [root@ecshost ~]# mkfs.ext4 /dev/vdb2
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
        [root@ecshost ~]# blkid /dev/vdb2
        /dev/vdb2: UUID="e3f336dc-d534-4fdd-****-b6ff1a55bdbb" TYPE="ext4"
        ```

    -   创建ext3文件系统：`mkfs.ext3 /dev/vdb2` 

        ``` {#codeblock_r80_vxx_d62 .lanuage-shell}
        [root@ecshost ~]# mkfs.ext3 /dev/vdb2
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
        [root@ecshost ~]# blkid /dev/vdb2
        /dev/vdb2: UUID="dd5be97d-a630-4593-****-5056def914ea" SEC_TYPE="ext2" TYPE="ext3"
        ```

    -   创建xfs文件系统：`mkfs.xfs -f /dev/vdb2` 

        ``` {#codeblock_tzg_2uj_usi .lanuage-shell}
        [root@ecshost ~]# mkfs.xfs -f /dev/vdb2
        meta-data=/dev/vdb2              isize=512    agcount=4, agsize=1310720 blks
                 =                       sectsz=512   attr=2, projid32bit=1
                 =                       crc=1        finobt=0, sparse=0
        data     =                       bsize=4096   blocks=5242880, imaxpct=25
                 =                       sunit=0      swidth=0 blks
        naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
        log      =internal log           bsize=4096   blocks=2560, version=2
                 =                       sectsz=512   sunit=0 blks, lazy-count=1
        realtime =none                   extsz=4096   blocks=0, rtextents=0
        [root@ecshost ~]# blkid /dev/vdb2
        /dev/vdb2: UUID="66251477-3ae4-4b44-****-5604420dbecb" TYPE="xfs"
        ```

    -   创建btrfs文件系统：`mkfs.btrfs /dev/vdb2` 

        ``` {#codeblock_zje_bhf_paj .lanuage-shell}
        [root@ecshost ~]# mkfs.btrfs /dev/vdb2
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
        [root@ecshost ~]# blkid /dev/vdb2
        /dev/vdb2: UUID="6fb5779b-57d7-4aaf-****-82b46f54a429" UUID_SUB="9bdd889a-ab69-4653-****-d1b6b8723378" TYPE="btrfs"
        ```

4.  运行`mount /dev/vdb2 /mnt`挂载文件系统。
5.  运行`df -h`查看目前数据盘空间和使用情况。

    显示新建文件系统的信息，表示挂载成功。

    ``` {#codeblock_zb6_5zt_gtk .lanuage-shell}
    [root@ecshost ~]# df -h
    Filesystem Size Used Avail Use% Mounted on
    /dev/vda1 40G 1.6G 36G 5% /
    devtmpfs 3.9G 0 3.9G 0% /dev
    tmpfs 3.9G 0 3.9G 0% /dev/shm
    tmpfs 3.9G 460K 3.9G 1% /run
    tmpfs 3.9G 0 3.9G 0% /sys/fs/cgroup
    /dev/vdb2 9.8G 37M 9.2G 1% /mnt
    tmpfs 783M 0 783M 0% /run/user/0
    ```


## 选项三：扩展已有GPT分区 {#section_oi9_qp8_f04 .section}

如果新增空间用于扩容已有的GPT分区，按照以下步骤在实例中完成扩容。示例采用一块1 TiB的数据盘，扩容后为32 TiB，已有分区为/dev/vdb1。

1.  使用fdisk工具查看待扩展的数据盘分区。

    ``` {#codeblock_7se_li5_o6n .lanuage-shell}
    [root@ecshost ~]# fdisk -l
    Disk /dev/vda: 42.9 GB, 42949672960 bytes, 83886080 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x000b1b45
    
       Device Boot      Start         End      Blocks   Id  System
    /dev/vda1   *        2048    83875364    41936658+  83  Linux
    WARNING: fdisk GPT support is currently new, and therefore in an experimental phase. Use at your own discretion.
    
    Disk /dev/vdb: 35184.4 GB, 35184372088832 bytes, 68719476736 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: gpt
    Disk identifier: BCE92401-F427-45CC-8B0D-B30EDF279C2F
    
    #         Start          End    Size  Type            Name
     1         2048   2147483647   1024G  Microsoft basic mnt                    
    ```

2.  查看数据盘的挂载路径，根据返回的文件路径卸载分区，直至完全卸载已挂载的分区。

    ``` {#codeblock_tl5_yci_a49 .lanuage-shell}
    [root@ecshost ~]# mount | grep "/dev/vdb"
    /dev/vdb1 on /mnt type ext4 (rw,relatime,data=ordered)
    [root@ecshost ~]# umount /dev/vdb1
    [root@ecshost ~]# mount | grep "/dev/vdb"
    ```

3.  使用parted工具为分区分配容量。
    1.  运行`parted /dev/vdb`进入parted分区工具。
    2.  （可选）运行`help`查看工具使用说明。
    3.  运行`print`查看待扩容的分区号（Number）和容量（Size）。

        示例中，待扩容的分区为1号分区，已有容量为1100 GiB，以下步骤会将所有新增容量分配到该分区。

    4.  运行`resizepart <分区号> <容量分配百分比>`扩展分区。

        示例操作为`resizepart 1 100%`。

    5.  运行`print`查看分区号（Number）和容量（Size）是否发生变化。

        ``` {#codeblock_hw4_cmz_08o .lanuage-shell}
        [root@ecshost ~]# parted /dev/vdb
        GNU Parted 3.1
        Using /dev/vdb
        Welcome to GNU Parted! Type 'help' to view a list of commands.
        
        (parted) print
        Model: Virtio Block Device (virtblk)
        Disk /dev/vdb: 35.2TB
        Sector size (logical/physical): 512B/512B
        Partition Table: gpt
        Disk Flags:
        
        Number  Start   End     Size    File system  Name  Flags
         1      1049kB  1100GB  1100GB  ext4         mnt
        (parted) resizepart 1 100%
        (parted) print
        Model: Virtio Block Device (virtblk)
        Disk /dev/vdb: 35.2TB
        Sector size (logical/physical): 512B/512B
        Partition Table: gpt
        Disk Flags:
        
        Number  Start   End     Size    File system  Name  Flags
         1      1049kB  35.2TB  35.2TB  ext4         mnt                    
        ```

    6.  运行`quit`退出parted分区工具。
4.  运行`fsck -f /dev/vdb1`确认文件系统一致性。

    ``` {#codeblock_r7a_3jb_gkh .lanuage-shell}
    [root@ecshost ~]# fsck -f /dev/vdb1
    fsck from util-linux 2.23.2
    e2fsck 1.42.9 (28-Dec-2013)
    Pass 1: Checking inodes, blocks, and sizes
    Pass 2: Checking directory structure
    Pass 3: Checking directory connectivity
    Pass 4: Checking reference counts
    Pass 5: Checking group summary information
    /dev/vdb1: 11/67108864 files (0.0% non-contiguous), 4265369/268435200 blocks
    ```

5.  扩展分区对应的文件系统并重新挂载分区。
    -   ext\*文件系统（例如ext3和ext4）：运行`resize2fs /dev/vdb1`并重新挂载分区。

        ``` {#codeblock_vgo_hmt_rmq .lanuage-shell}
        [root@ecshost ~]# resize2fs /dev/vdb1
        resize2fs 1.42.9 (28-Dec-2013)
        Resizing the filesystem on /dev/vdb1 to 8589934331 (4k) blocks.
        The filesystem on /dev/vdb1 is now 8589934331 blocks long.
        [root@ecshost ~]# mount /dev/vdb1 /mnt
        ```

    -   xfs文件系统：先运行`mount /dev/vdb1 /mnt/`命令，再运行`xfs_growfs /dev/vdb1`。

        ``` {#codeblock_muy_rnl_1g7 .lanuage-shell}
        [root@ecshost ~]# mount /dev/vdb1 /mnt/
        [root@ecshost ~]# xfs\_growfs /dev/vdb1
        ```


## 选项四：新增并格式化GPT分区 {#section_4hl_5l7_87s .section}

如果新增空间用于增加新的分区并希望使用GPT分区格式，按照以下步骤在实例中完成扩容。示例采用一块32 TiB的数据盘，已有一个4.8 TiB的分区/dev/vdb1，此次新建了一个/dev/vdb2分区。

1.  使用fdisk工具查看数据盘中已有分区的信息。

    ``` {#codeblock_nrd_kr0_4x1 .lanuage-shell}
    [root@ecshost ~]# fdisk -l
    Disk /dev/vda: 42.9 GB, 42949672960 bytes, 83886080 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x000b1b45
    
       Device Boot      Start         End      Blocks   Id  System
    /dev/vda1   *        2048    83875364    41936658+  83  Linux
    WARNING: fdisk GPT support is currently new, and therefore in an experimental phase. Use at your own discretion.
    
    Disk /dev/vdb: 35184.4 GB, 35184372088832 bytes, 68719476736 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: gpt
    Disk identifier: BCE92401-F427-45CC-8B0D-B30EDF279C2F
    
    #         Start          End    Size  Type            Name
     1         2048  10307921919    4.8T  Microsoft basic mnt                    
    ```

2.  使用parted工具创建新分区并分配容量。
    1.  运行`parted /dev/vdb`进入分区工具。
    2.  运行`print free`查看数据盘待分配的容量，记录已有分区的扇区位置和容量。

        示例中/dev/vdb1的起始位置为1049 KB，结束扇区为5278 GB，容量为5278 GiB。

        ``` {#codeblock_k7q_ebl_6pw .lanuage-shell}
        (parted) print free
        Model: Virtio Block Device (virtblk)
        Disk /dev/vdb: 35.2TB
        Sector size (logical/physical): 512B/512B
        Partition Table: gpt
        Disk Flags:
        
        Number  Start   End     Size    File system  Name  Flags
                17.4kB  1049kB  1031kB  Free Space
         1      1049kB  5278GB  5278GB  ext4         mnt
                5278GB  35.2TB  29.9TB  Free Space                    
        ```

    3.  运行`mkpart <分区名称> <起始扇区> <容量分配百分比>`。

        示例新建了一个名为test的/dev/vdb2分区，起始扇区为上一个分区的结束扇区，并将所有新增空间分配给该分区。

    4.  运行`print`查看容量（Size）是否发生变化。

        ``` {#codeblock_g8z_sg6_22e .lanuage-shell}
        (parted) mkpart test 5278GB 100%
        (parted) print
        Model: Virtio Block Device (virtblk)
        Disk /dev/vdb: 35.2TB
        Sector size (logical/physical): 512B/512B
        Partition Table: gpt
        Disk Flags:
        
        Number  Start   End     Size    File system  Name  Flags
         1      1049kB  5278GB  5278GB  ext4         mnt
         2      5278GB  35.2TB  29.9TB               test                    
        ```

    5.  运行`quit`退出parted分区工具。
3.  为新分区创建文件系统。

    -   创建ext4文件系统：`mkfs.ext4 /dev/vdb2`
    -   创建ext3文件系统：`mkfs.ext3 /dev/vdb2`
    -   创建xfs文件系统：`mkfs.xfs -f /dev/vdb2`
    -   创建btrfs文件系统：`mkfs.btrfs /dev/vdb2`
    示例中创建了一个xfs文件系统，如下所示。

    ``` {#codeblock_sb7_qm1_env .lanuage-shell}
    [root@ecshost ~]# mkfs -t xfs /dev/vdb2
    meta-data=/dev/vdb2              isize=512    agcount=28, agsize=268435455 blks
             =                       sectsz=512   attr=2, projid32bit=1
             =                       crc=1        finobt=0, sparse=0
    data     =                       bsize=4096   blocks=7301444096, imaxpct=5
             =                       sunit=0      swidth=0 blks
    naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
    log      =internal log           bsize=4096   blocks=521728, version=2
             =                       sectsz=512   sunit=0 blks, lazy-count=1
    realtime =none                   extsz=4096   blocks=0, rtextents=0               
    ```

4.  运行`fdisk -l`查看分区容量变化。

    ``` {#codeblock_bve_5oy_ggu .lanuage-shell}
    [root@ecshost ~]# fdisk -l
    Disk /dev/vda: 42.9 GB, 42949672960 bytes, 83886080 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x000b1b45
    
       Device Boot      Start         End      Blocks   Id  System
    /dev/vda1   *        2048    83875364    41936658+  83  Linux
    WARNING: fdisk GPT support is currently new, and therefore in an experimental phase. Use at your own discretion.
    
    Disk /dev/vdb: 35184.4 GB, 35184372088832 bytes, 68719476736 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: gpt
    Disk identifier: BCE92401-F427-45CC-8B0D-B30EDF279C2F
    
    #         Start          End    Size  Type            Name
     1         2048  10307921919    4.8T  Microsoft basic mnt
     2  10307921920  68719474687   27.2T  Microsoft basic test  
    ```

5.  运行blkid查看存储设备的文件系统类型。

    ``` {#codeblock_yc6_imy_avh .lanuage-shell}
    [root@ecshost ~]# blkid
    /dev/vda1: UUID="ed95c595-4813-480e-****-85b1347842e8" TYPE="ext4"
    /dev/vdb1: UUID="21e91bbc-7bca-4c08-****-88d5b3a2303d" TYPE="ext4" PARTLABEL="mnt" PARTUUID="576235e0-5e04-4b76-****-741cbc7e98cb"
    /dev/vdb2: UUID="a7dcde59-8f0f-4193-****-362a27192fb1" TYPE="xfs" PARTLABEL="test" PARTUUID="464a9fa9-3933-4365-****-c42de62d2864"  
    ```

6.  挂载新分区。

    ``` {#codeblock_8if_42j_r60 .lanuage-shell}
    [root@ecshost ~]# mount /dev/vdb2 /mnt
    ```


## 相关操作 {#section_nop_fuk_f6y .section}

-   [扩展分区和文件系统\_Linux系统盘](intl.zh-CN/块存储/云盘/扩容云盘/扩展分区和文件系统_Linux系统盘.md#)
-   [扩展分区和文件系统\_Windows](intl.zh-CN/块存储/云盘/扩容云盘/扩展分区和文件系统_Windows.md#)

