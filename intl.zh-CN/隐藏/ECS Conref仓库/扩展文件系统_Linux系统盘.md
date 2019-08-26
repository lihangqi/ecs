# 扩展文件系统\_Linux系统盘 {#concept_ocb_htw_dhb .concept}

本文提供了如何使用growpart和resize2fs工具完成Linux系统盘扩容及文件系统扩展的操作指导，适用于扩容前已挂载到Linux实例的系统盘。

## 扩容指引 { .section}

本文通过growpart和resize2fs扩展系统盘/dev/vda的已有分区/dev/vda1。

-   如果您在[扩容云盘](intl.zh-CN/隐藏/ECS Conref仓库/在线扩容云盘.md#)时勾选了**在线扩容**，且满足以下条件则无需重启便能完成扩容。该情况请参见[在线扩容操作步骤](#section_gxq_3tw_dhb)。
    -   分区格式支持：mbr、gpt
    -   文件系统支持：ext、xfs、btrfs、ufs
    -   操作系统支持：通过`uname -a`查看到的内核版本大于3.6.0
-   操作系统内核版本较低（小于3.6.0），如CentOS 6、Debian 7和SUSE Linux Enterprise Server 11 SP4等发行版，需要经过一次重启才能完成扩容。该情况请参见[离线扩容操作步骤](#section_vxq_3tw_dhb)。
-   如果您需要扩展数据盘已有分区，可以将本文操作步骤中的磁盘挂载点和分区修改成对应数据盘。如果新磁盘空间用于增加新的分区，请参见[扩展文件系统\_Linux数据盘](intl.zh-CN/隐藏/ECS Conref仓库/扩展文件系统_Linux数据盘.md#)。

## 准备工作 {#section_h25_n5w_dhb .section}

1.  通过ECS控制台或者API[扩容云盘](intl.zh-CN/隐藏/ECS Conref仓库/在线扩容云盘.md#)。
2.  [创建快照](intl.zh-CN/快照/使用快照/创建快照.md#)以备份数据。
3.  云盘已挂载到实例上，实例已处于**运行中**状态。连接方式请参见[连接方式导航](../../../../../intl.zh-CN/实例/连接实例/连接方式导航.md#)。
4.  根据操作系统安装growpart扩容格式化工具。

    |操作系统发行版|安装growpart工具|
    |:------|:-----------|
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
    |Debian 8|使用上游版本（upstream）的growpart工具|
    |OpenSUSE 42.3|
    |OpenSUSE 13.1|
    |SUSE Linux Enterprise Server 12 SP2|


## 在线扩容操作步骤 {#section_gxq_3tw_dhb .section}

此处以CentOS 7实例为例演示分区在线扩展的步骤。

1.  根据操作系统安装growpart扩容格式化工具。

    ```
    [root@localhost ~]# yum install -y cloud-utils-growpart
    ```

2.  运行`fdisk -l`查看现有磁盘大小。示例返回磁盘（/dev/vda）容量是100 GiB。

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

3.  运行`df -h`查看磁盘分区大小。示例返回分区容量（/dev/vda1）是20 GiB。

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

4.  运行`growpart <DeviceName\><PartionNumber\>`调用growpart为需要扩容的磁盘和对应的第几个分区扩容。示例命令表示为系统盘的第一个分区扩容。

    ```
    [root@localhost ~]# growpart /dev/vda 1
    CHANGED: partition=1 start=2048 old: size=41940992 end=41943040 new: size=209710462,end=209712510
    ```

5.  运行`resize2fs <PartitionName\>`调用resize2fs扩容文件系统。示例命令表示为系统盘的/dev/vda1分区扩容文件系统。

    ```
    [root@localhost ~]# resize2fs /dev/vda1
    resize2fs 1.42.9 (28-Dec-2013)
    Filesystem at /dev/vda1 is mounted on /; on-line resizing required
    old_desc_blocks = 2, new_desc_blocks = 7
    The filesystem on /dev/vda1 is now 26213807 blocks long.
    ```

6.  运行`df -h`查看磁盘分区大小。返回分区（/dev/vda1）是100 GiB，表示已经成功扩容。

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


## 离线扩容操作步骤 {#section_vxq_3tw_dhb .section}

此处以CentOS 6实例为例演示分区离线扩展的步骤。

1.  安装growpart和dracut-modules-growroot工具。

    ```
    [root@AliYunOS ~]# yum install -y cloud-utils-growpart dracut-modules-growroot
    [root@AliYunOS ~]# dracut -f
    ```

2.  运行`fdisk -l`查看现有磁盘大小。示例返回磁盘（/dev/vda）容量是100 GiB。

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

3.  运行`df -h`查看磁盘分区大小。示例返回分区容量（/dev/vda1）是20 GiB。

    ```
    [root@AliYunOS ~]# df -h
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/vda1        20G  1.1G   18G   6% /
    tmpfs           7.8G     0  7.8G   0% /dev/shm
    ```

4.  运行`growpart <DeviceName\><PartionNumber\>`调用growpart为需要扩容的磁盘和对应的第几个分区扩容。示例命令表示为系统盘的第一个分区扩容。

    ```
    [root@AliYunOS ~]# growpart /dev/vda 1
    CHANGED: partition=1 start=2048 old: size=41940992 end=41943040 new: size=209710462,end=209712510
    ```

5.  重启实例。

    ```
    [root@AliYunOS ~]# reboot
    ```

6.  再次远程连接实例。
7.  运行`resize2fs <PartitionName\>`调用resize2fs扩容文件系统。示例命令表示为系统盘的/dev/vda1分区扩容文件系统。

    ```
    [root@AliYunOS ~]# resize2fs /dev/vda1
    resize2fs 1.41.12 (17-May-2010)
    Filesystem at /dev/vda1 is mounted on /; on-line resizing required
    old desc_blocks = 2, new_desc_blocks = 7
    Performing an on-line resize of /dev/vda1 to 26213807 (4k) blocks.
    The filesystem on /dev/vda1 is now 26213807 blocks long.
    ```

8.  运行`df -h`查看磁盘分区大小。返回分区（/dev/vda1）是100 GiB，表示已经成功扩容。

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


