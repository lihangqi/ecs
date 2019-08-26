# 扩展分区和文件系统\_Linux系统盘 {#concept_ocb_htw_dhb .concept}

本文提供了如何使用growpart和resize2fs工具完成Linux系统盘分区扩容及文件系统扩展的操作指导。

## 适用范围 {#section_u9c_3g5_ljs .section}

本文的操作步骤适用于以下分区和文件系统格式的云盘：

-   分区格式支持mbr、gpt
-   文件系统支持ext\*、xfs、btrfs

## 准备工作 {#section_h25_n5w_dhb .section}

1.  [创建快照](cn.zh-CN/快照/使用快照/创建快照.md#)以备份数据，防止操作失误导致数据丢失。
2.  通过ECS控制台或者API[扩容云盘容量](cn.zh-CN/块存储/云盘/扩容云盘/离线扩容云盘.md#)。
3.  远程连接ECS实例。连接方式请参见[连接方式导航](../../../../cn.zh-CN/实例/连接实例/连接方式导航.md#)。
4.  根据操作系统安装growpart或者xfsprogs扩容格式化工具。

    -   CentOS 7、Aliyun Linux：

        ``` {#codeblock_lnb_89n_iih}
        yum install cloud-utils-growpart
        yum install xfsprogs
        ```

    -   Ubuntu 14、Ubuntu 16、Ubuntu 18、Debian 9：

        ``` {#codeblock_x6x_nv9_rlb}
        apt install cloud-guest-utils
        apt install xfsprogs
        ```

    -   Debian 8、OpenSUSE 42.3、OpenSUSE 13.1、SUSE Linux Enterprise Server 12 SP2：请使用上游版本（upstream）的growpart或者xfsprogs工具
    **说明：** 当出现因扩容格式化工具问题导致的扩容失败时，您可以卸载工具后重新安装。

5.  检查实例的内核版本，如通过`uname -a`查看内核版本。
    -   内核版本大于3.6.0，该情况请参见[高内核版本的操作步骤](#section_gxq_3tw_dhb)。
    -   内核版本小于3.6.0，该情况请参见[低内核版本的操作步骤](#section_vxq_3tw_dhb)。如CentOS 6、Debian 7和SUSE Linux Enterprise Server 11 SP4等发行版，需要经过一次控制台重启或者API重启才能完成分区扩容。

## 高内核版本的操作步骤 {#section_gxq_3tw_dhb .section}

此处以CentOS 7操作系统为例演示分区扩展的步骤。

1.  运行`fdisk -l`查看现有云盘大小。

    示例返回云盘（/dev/vda）容量是100GiB。

    ``` {#codeblock_2wt_omi_qd8}
    [root@ecshost ~]# fdisk -l
    Disk /dev/vda: 107.4 GB, 107374182400 bytes, 209715200 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x0008d73a
    
       Device Boot      Start         End      Blocks   Id  System
    /dev/vda1   *        2048    41943039    20970496   83  Linux
    ```

2.  运行`df -h`查看云盘分区大小。

    示例返回分区容量（/dev/vda1）是20GiB。

    ``` {#codeblock_ui3_rtz_duk}
    [root@ecshost ~]# df -h
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/vda1        20G  1.5G   18G   8% /
    devtmpfs        7.8G     0  7.8G   0% /dev
    tmpfs           7.8G     0  7.8G   0% /dev/shm
    tmpfs           7.8G  344K  7.8G   1% /run
    tmpfs           7.8G     0  7.8G   0% /sys/fs/cgroup
    tmpfs           1.6G     0  1.6G   0% /run/user/0
    ```

3.  运行`growpart <DeviceName\><PartionNumber\>`调用growpart为需要扩容的云盘和对应的第几个分区扩容。

    示例命令表示为系统盘的第一个分区扩容。

    ``` {#codeblock_5j1_isw_vt9}
    [root@ecshost ~]# growpart /dev/vda 1
    CHANGED: partition=1 start=2048 old: size=41940992 end=41943040 new: size=209710462,end=209712510
    ```

4.  运行`resize2fs <PartitionName\>`调用resize2fs扩容文件系统。

    示例命令表示为系统盘的/dev/vda1分区扩容文件系统。

    ``` {#codeblock_ojc_rie_69u}
    [root@ecshost ~]# resize2fs /dev/vda1
    resize2fs 1.42.9 (28-Dec-2013)
    Filesystem at /dev/vda1 is mounted on /; on-line resizing required
    old_desc_blocks = 2, new_desc_blocks = 7
    The filesystem on /dev/vda1 is now 26213807 blocks long.
    ```

    **说明：** 如果您使用的是xfs文件系统，运行`xfs_growfs /dev/vda1`扩容文件系统。

5.  运行`df -h`查看云盘分区大小。

    返回分区（/dev/vda1）是100GiB，表示已经成功扩容。

    ``` {#codeblock_dxd_5wk_ijc}
    [root@ecshost ~]# df -h
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/vda1        99G  1.6G   93G   2% /
    devtmpfs        7.8G     0  7.8G   0% /dev
    tmpfs           7.8G     0  7.8G   0% /dev/shm
    tmpfs           7.8G  500K  7.8G   1% /run
    tmpfs           7.8G     0  7.8G   0% /sys/fs/cgroup
    tmpfs           1.6G     0  1.6G   0% /run/user/0
    ```


## 低内核版本的操作步骤 {#section_vxq_3tw_dhb .section}

此处以CentOS 6操作系统为例演示分区扩展的步骤。

1.  安装dracut-modules-growroot工具。

    ``` {#codeblock_spo_ed5_l62}
    [root@ecshost ~]# yum install -y dracut-modules-growroot
    ```

    如果您使用的是其他软件包管理器，请将yum修改为对应的命令。

2.  覆盖已有的initramfs文件。

    ``` {#codeblock_fez_t5m_qh6}
    [root@ecshost ~]# dracut -f
    ```

3.  运行`fdisk -l`查看现有云盘大小。

    示例返回云盘（/dev/vda）容量是100GiB。

    ``` {#codeblock_89d_7qe_lf3}
    [root@ecshost ~]# fdisk -l
    Disk /dev/vda: 107.4 GB, 107374182400 bytes
    255 heads, 63 sectors/track, 13054 cylinders
    Units = cylinders of 16065 * 512 = 8225280 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk identifier: 0x0003a7b4
    
       Device Boot      Start         End      Blocks   Id  System
    /dev/vda1   *           1        2611    20970496   83  Linux
    ```

4.  运行`df -h`查看云盘分区大小。

    示例返回分区容量（/dev/vda1）是20GiB。

    ``` {#codeblock_0fw_5w3_4d9}
    [root@ecshost ~]# df -h
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/vda1        20G  1.1G   18G   6% /
    tmpfs           7.8G     0  7.8G   0% /dev/shm
    ```

5.  运行`growpart <DeviceName\><PartionNumber\>`调用growpart为需要扩容的云盘和对应的第几个分区扩容。

    示例命令表示为系统盘的第一个分区扩容。

    ``` {#codeblock_6lb_aln_3fy}
    [root@ecshost ~]# growpart /dev/vda 1
    CHANGED: partition=1 start=2048 old: size=41940992 end=41943040 new: size=209710462,end=209712510
    ```

6.  在控制台重启实例或者调用API RebootInstance。详细步骤请参见[重启实例](../../../../cn.zh-CN/实例/管理实例/重启实例.md#)和[RebootInstance](../../../../cn.zh-CN/API参考/实例/RebootInstance.md#)。
7.  再次远程连接实例。
8.  运行`resize2fs <PartitionName\>`调用resize2fs扩容文件系统。

    示例命令表示为系统盘的/dev/vda1分区扩容文件系统。

    ``` {#codeblock_9ma_xwj_r94}
    [root@ecshost ~]# resize2fs /dev/vda1
    resize2fs 1.41.12 (17-May-2010)
    Filesystem at /dev/vda1 is mounted on /; on-line resizing required
    old desc_blocks = 2, new_desc_blocks = 7
    Performing an on-line resize of /dev/vda1 to 26213807 (4k) blocks.
    The filesystem on /dev/vda1 is now 26213807 blocks long.
    ```

    **说明：** 如果您使用的是xfs文件系统，运行`xfs_growfs /dev/vda1`扩容文件系统。

9.  运行`df -h`查看云盘分区大小。

    返回分区（/dev/vda1）是100GiB，表示已经成功扩容。

    ``` {#codeblock_x71_1oh_4rb}
    [root@ecshost ~]# df -h
    Filesystem      Size  Used Avail Use% Mounted on
    /dev/vda1        99G  1.1G   93G   2% /
    tmpfs           7.8G     0  7.8G   0% /dev/shm
    ```


## 相关操作 {#section_gy7_ue1_3tg .section}

[扩展分区和文件系统\_Linux数据盘](cn.zh-CN/块存储/云盘/扩容云盘/扩展分区和文件系统_Linux数据盘.md#)

