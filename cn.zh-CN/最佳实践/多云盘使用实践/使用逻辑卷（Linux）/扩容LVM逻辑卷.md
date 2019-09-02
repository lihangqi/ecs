# 扩容LVM逻辑卷 {#task_1797418 .task}

本文介绍了如何扩容一个由多块云盘组成的逻辑卷（Logical Volume Manager，LVM），适用于Linux系统ECS实例。

您已经创建了一个逻辑卷。详细步骤请参见[创建LVM逻辑卷](cn.zh-CN/最佳实践/多云盘使用实践/使用逻辑卷（Linux）/创建LVM逻辑卷.md#)。

云盘有尚未分配的容量。或者云盘已经完成扩容，详情请参见[扩容概述](cn.zh-CN/块存储/云盘/扩容云盘/扩容概述.md#)。

## 操作步骤 {#section_uki_qz8_7el .section}

1.  以root权限远程连接ECS实例。连接方式请参见[连接方式导航](../cn.zh-CN/实例/连接实例/连接方式导航.md#)。
2.  使用lvdisplay命令查看ECS实例中已经创建的逻辑卷（LV）信息。 

    假设您已经创建了/dev/lvm\_01/lv01逻辑卷，拥有5TiB物理空间。

    ``` {#codeblock_izs_2u7_d6k}
    root@lvs06:~# lvdisplay
      --- Logical volume ---
      LV Path                /dev/lvm_01/lv01
      LV Name                lv01
      VG Name                lvm_01
      LV UUID                svB00x-l6Ke-ES6M-ctsE-9P6d-dVj2-o0h***
      LV Write Access        read/write
      LV Creation host, time lvs06, 2019-06-0615:27:19 +0800
      LV Status              available
      # open                 0
      LV Size                5.00 TiB
      Current LE             1310720
      Segments               6
      Allocation             inherit
      Read ahead sectors     auto
      - currently set to     256
      Block device           253:0
    ```

3.  使用pvs命令查看物理卷（PV）使用情况。 

    假设数据盘/dev/vdg有500GiB待分配空间。

    ``` {#codeblock_7ij_ku3_8l0}
    root@lvs06:~# pvs
      PV         VG     Fmt  Attr PSize     PFree
      /dev/vdb   lvm_01 lvm2 a--  <1024.00g       0
      /dev/vdc   lvm_01 lvm2 a--  <1024.00g       0
      /dev/vdd   lvm_01 lvm2 a--  <1024.00g       0
      /dev/vde   lvm_01 lvm2 a--  <1024.00g       0
      /dev/vdf   lvm_01 lvm2 a--  <1024.00g       0
      /dev/vdg   lvm_01 lvm2 a--  <1024.00g <523.98g
    ```

4.  使用lvextend命令扩容逻辑卷。 

    ``` {#codeblock_0ol_7mz_xng}
    lvextend [-L +/- <增减容量>] <逻辑卷名称>
    ```

    **说明：** 

    -   增减容量：卷组（VG）必须有剩余容量时才可以执行扩容逻辑卷操作。本文假设逻辑卷从5TiB被扩容到5.5TiB。
    -   逻辑卷名称：填写待扩容的逻辑卷名称。
    假设您为逻辑卷/dev/lvm\_01/lv01扩容了500GiB物理空间。

    ``` {#codeblock_3fd_mi7_2zm}
    root@lvs06:~# lvextend -L +500GB /dev/lvm\_01/lv01
    Size of logical volume lvm_01/lv01 changed from5.00 TiB (1310720 extents) to <5.49 TiB (1438720 extents).
    Logical volume lvm_01/lv01 successfully resized.
    ```

5.  使用resize2fs命令扩容逻辑卷文件系统。 

    ``` {#codeblock_b0o_y3s_6gf}
    root@lvs06:~# resize2fs /dev/lvm\_01/lv01
    resize2fs 1.44.1 (24-Mar-2018)
    Filesystem at /dev/lvm_01/lv01 is mounted on /media/lv01; on-line resizing required
    old_desc_blocks = 640, new_desc_blocks = 703
    The filesystem on /dev/lvm_01/lv01 is now 1473249280 (4k) blocks long.
    ```

6.  使用df命令查看文件系统扩容结果。 

    显示逻辑卷的总容量为5.5TiB，表示扩容成功。

    ``` {#codeblock_42v_8tw_ihl}
    root@lvs06:~# df -h
    Filesystem               Size  Used Avail Use% Mounted on
    udev                      12G     012G   0% /dev
    tmpfs                    2.4G  3.7M  2.4G   1% /run
    /dev/vda1                 40G  3.6G   34G  10% /
    tmpfs                     12G     0   12G   0% /dev/shm
    tmpfs                    5.0M     05.0M   0% /run/lock
    tmpfs                     12G     012G   0% /sys/fs/cgroup
    tmpfs                    2.4G     02.4G   0% /run/user/0
    /dev/mapper/lvm_01-lv01  5.5T   83M  5.2T   1% /media/lv01
    ```


**相关文档**  


[创建LVM逻辑卷](cn.zh-CN/最佳实践/多云盘使用实践/使用逻辑卷（Linux）/创建LVM逻辑卷.md#)

