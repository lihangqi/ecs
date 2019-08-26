# CentOS 7实例重启系统后主机名大写字母被修改 {#concept_ulc_fxf_1hb .concept}

第一次重启ECS实例后，部分CentOS 7实例的主机名（hostname）存在大写字母变成小写字母的现象。本文列举了受影响的镜像类型以及修改hostname的解决方法。

## 现象示例 {#section_pcd_3xf_1hb .section}

下表为含有大写字母hostname的CentOS实例初次重启前后的变化举例。

|实例hostname示例|第一次重启后示例|后续是否保持小写不变|
|:-----------|:-------|:---------|
|iZm5e1qe09gy5sxx1ps5zX|izm5e1qe09gy5sxx1ps5z6x|是|
|ZZHost|zzhost|是|
|NetworkNode|networknode|是|

## 影响范围 {#section_ps5_kxf_1hb .section}

**受影响的镜像列表**

以下CentOS公共镜像，和基于以下公共镜像创建的自定义镜像会受到影响。

-   centos\_7\_2\_64\_40G\_base\_20170222.vhd
-   centos\_7\_3\_64\_40G\_base\_20170322.vhd
-   centos\_7\_03\_64\_40G\_alibase\_20170503.vhd
-   centos\_7\_03\_64\_40G\_alibase\_20170523.vhd
-   centos\_7\_03\_64\_40G\_alibase\_20170625.vhd
-   centos\_7\_03\_64\_40G\_alibase\_20170710.vhd
-   centos\_7\_02\_64\_20G\_alibase\_20170818.vhd
-   centos\_7\_03\_64\_20G\_alibase\_20170818.vhd
-   centos\_7\_04\_64\_20G\_alibase\_201701015.vhd

**受影响的hostname类型**

如果您的应用有hostname大小写敏感现象，重启实例后会影响业务。以下hostname类型可以根据本文步骤修复hostname。

|hostname类型|是否受影响|何时受影响|是否继续阅读文档|
|:---------|:----|:----|:-------|
|在控制台或通过API创建实例时，hostname中有大写字母|是|第一次重启实例|是|
|在控制台或通过API创建实例时，hostname中全是小写字母|否|不适用|否|
|hostname中有大写字母，您登录实例后自行修改了hostname|否|不适用|是|

## 解决方法 {#section_igh_hxf_1hb .section}

如果重启实例后需要保留带大写字母的hostname时，可以按如下步骤操作：

1.  远程连接实例。
2.  查看现有的hostname。

    ```
    [root@izbp193nf1pk3i161uynzzx ~]# hostname
    izbp193nf1pk3i161uynzzx
    ```

3.  执行以下命令固化hostname：

    ```
    hostnamectl set-hostname --static iZbp193nf1pk3i161uynzzX
    ```

4.  查看更新后的hostname。

    ```
    [root@izbp193nf1pk3i161uynzzx ~]# hostname
    iZbp193nf1pk3i161uynzzX
    ```


## 下一步 {#section_eb3_1bh_1hb .section}

如果您使用的是自定义镜像，请更新至最新的cloud-init软件后再次创建自定义镜像。避免使用受影响的自定义镜像创建新实例后发生相同问题。更多详情，请参见[安装cloud-init](intl.zh-CN/镜像/自定义镜像/导入镜像/安装cloud-init.md#)和[使用实例创建自定义镜像](intl.zh-CN/镜像/自定义镜像/创建自定义镜像/使用实例创建自定义镜像.md#)。

