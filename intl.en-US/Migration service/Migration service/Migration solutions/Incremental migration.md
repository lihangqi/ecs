# Incremental migration {#concept_c43_tkk_yfb .concept}

After you perform a full migration, we recommend that you suspend your services and perform an incremental migration to synchronize any data changes from the source server to the target ECS instance.

If you want to synchronize the incremental data online, we recommend that you use the [Alibaba Cloud Data Transmission Service \(DTS\)](https://www.aliyun.com/solution/dts).

## Prerequisite {#section_ztr_njp_yfb .section}

You have successfully performed a [Full migration](intl.en-US/Migration service/Migration service/Migration solutions/Full migration.md#), which has generated a custom image \(that is, a full image\) in the ECS console.

## Procedure {#section_jth_n3p_yfb .section}

1.  Suspend your services.

2.  Use the full image to [create a Pay-As-You-Go instance](../../../../../intl.en-US/Instances/ECS instance life cycle/Create an instance/Create an instance by using a custom image.md#), and configure the network to connect to the source system.

3.  Using an incremental synchronization tool to synchronize the incremental data from the source system to the target ECS instance.

    We recommend that you use the rsync or goodsync synchronization tool. In this example, rsync is used to describe how to synchronize incremental data from the source system to the target ECS instance. If the IP address of your target ECS instance is 10.0.0.11 and the directory that you need to synchronize is `/disk1`, then the example code of the rsync command is `rsync -azvASX --partial --progress -e "ssh " /disk1/ root@10.0.0.11:/disk1/`. For more information, see the [parameter descriptions on the rsync official website](https://download.samba.org/pub/rsync/rsync.html).

    **Note:** For incremental database synchronization, you can use the Alibaba Cloud DTS service.


