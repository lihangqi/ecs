# Linux格式化数据盘 {#concept_jl1_qzd_wdb .concept}

本文描述如何为Linux实例的全新数据盘创建一个单分区并挂载文件系统。您也可以根据业务需要，对数据盘进行多分区配置。

**说明：** 本文操作仅适用小于等于2 TiB的数据盘。大于2 TiB的数据盘，请参见[分区格式化大于2 TiB云盘](../../../../intl.zh-CN/块存储/云盘/分区格式化数据盘/分区格式化大于2 TiB云盘.md#)。

## 风险提示 { .section}

-   磁盘分区和格式化是高风险行为，请慎重操作。本文描述如何处理一块全新的数据盘，如果您的数据盘上有数据，请务必为数据盘[创建快照](../../../../intl.zh-CN/快照/使用快照/创建快照.md#)，避免数据丢失。
-   云服务器ECS仅支持**数据盘**分区操作，不支持**系统盘**分区操作。如果您强行使用第三方工具对系统盘做分区操作，可能引发系统崩溃和数据丢失等未知风险。仅允许在扩容系统盘后做扩展分区或新增分区操作，具体操作请参见[扩展分区与文件系统\_Linux系统盘](../../../../intl.zh-CN/块存储/云盘/扩容云盘/扩展分区与文件系统_Linux系统盘.md#)。

## 准备工作 {#section_dqp_xc2_wdb .section}

-   单独[购买的数据盘](../../../../intl.zh-CN/块存储/云盘/创建云盘/创建按量付费云盘.md#)必须先[挂载数据盘](../../../../intl.zh-CN/块存储/云盘/挂载云盘.md#)才能格式化。随实例一起购买的数据盘，无需挂载。
-   在ECS控制台的云盘页面中，选择**更多** \> **修改属性**查看数据盘的设备名。

    **说明：** 数据盘的设备名默认由系统分配，I/O优化实例的数据盘设备名从/dev/vdb递增排列，包括/dev/vdb−/dev/vdz。如果数据盘设备名为`dev/xvd*`（`*`是a−z的任意一个字母），表示您使用的是非I/O优化实例。


## 操作步骤 {#section_xtx_yc2_wdb .section}

本示例使用I/O优化实例，操作系统为CentOS 7.6，为一块新的20 GiB数据盘（设备名为/dev/vdb）创建一个单分区，分区格式使用MBR，挂载的是ext4文件系统。

**说明：** 如果您需要使用GPT分区格式，请参见[分区格式化大于2 TiB云盘](../../../../intl.zh-CN/块存储/云盘/分区格式化数据盘/分区格式化大于2 TiB云盘.md#)。

1.  [远程连接实例](intl.zh-CN/个人版快速入门/步骤 3：连接ECS实例.md#)。
2.  运行`fdisk -l`命令查看实例上的数据盘。

    **说明：** 执行命令后，如果不存在/dev/vdb，表示您的实例没有数据盘。确认数据盘是否已挂载。

3.  依次执行以下命令以创建一个单分区数据盘：
    1.  运行`fdisk -u /dev/vdb`：分区数据盘。
    2.  输入p：查看数据盘的分区情况。本示例中，数据盘没有分区。
    3.  输入n：创建一个新分区。
    4.  输入p：选择分区类型为主分区。

        **说明：** 本示例中创建一个单分区数据盘，所以只需要创建主分区。如果要创建四个以上分区，您应该创建至少一个扩展分区，即选择e（extended）。

    5.  输入分区编号并按回车键。本示例中，仅创建一个分区，输入1。
    6.  输入第一个可用的扇区编号：按回车键采用默认值2048。
    7.  输入最后一个扇区编号：本示例仅创建一个分区，按回车键采用默认值。
    8.  输入p：查看该数据盘的规划分区情况。
    9.  输入w：开始分区，并在分区后退出。

        ```
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

4.  运行命令`fdisk -lu /dev/vdb` 查看新分区。

    如果出现以下信息，表示新分区`/dev/vdb1`创建成功。

    ```
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

5.  运行命令`mkfs.ext4 /dev/vdb1`在新分区上创建一个文件系统。

    本示例中，创建一个ext4文件系统。您也可以根据自己的需要，选择创建其他文件系统，例如：如果您需要在 Linux、Windows和Mac系统之间共享文件，可以使用`mkfs.vfat`创建VFAT文件系统。

    **说明：** 创建文件系统所需时间取决于数据盘大小。

    ```
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

6.  （建议）运行命令`cp /etc/fstab /etc/fstab.bak`备份etc/fstab文件。
7.  运行命令`echo /dev/vdb1 /mnt ext4 defaults 0 0 >> /etc/fstab`向/etc/fstab写入新分区信息。

    **说明：** Ubuntu 12.04系统不支持barrier，您需要运行命令`echo '/dev/vdb1 /mnt ext4 barrier=0 0 0' >> /etc/fstab`。

    如要把数据盘单独挂载到某个文件夹，例如单独用来存放网页，则将命令中`/mnt`替换成所需的挂载点路径。

8.  运行命令`cat /etc/fstab`查看/etc/fstab中的新分区信息。

    ```
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

9.  运行命令`mount /dev/vdb1 /mnt`挂载文件系统。
10. 运行命令`df -h` 查看目前磁盘空间和使用情况。

    出现新建文件系统的信息，表示挂载成功，您不需要重启实例即可以使用新的文件系统。

    ```
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


