# Notes for migrating ECS instances to VPCs {#concept_65497_zh .concept}

This topic describes precautions related to the migration of Classic network ECS instances to VPCs. We recommend that you undertake this migration strategy because VPCs offer better network security.

## VPC network segment planning {#section_oty_zmg_jhb .section}

If the Classic network ECS instances to be migrated to the VPC need to communicate with other Classic network ECS instances in the same region after the migration, you can implement ClassicLink. The VPC network segments that can communicate with the Classic network are 10.111.0.0/16, 172.16.0.0/12, and 192.168.0.0/16. For more information about ClassicLink, see [ClassicLink migration](../../../../intl.en-US/User Guide/Network connection/ClassicLink/ClassicLink overview.md#).

## IP address { .section}

-   A migration does not change the public IP address of your ECS instance. However, the associated Network Interface Card \(NIC\) is deleted.

-   After a migration, the private IP address of your ECS instance is randomly assigned from the CIDR block of the target VSwitch. You can create a [VPC](../../../../intl.en-US/User Guide/VPC and subnets/Manage a VPC.md#) and [VSwitch](../../../../intl.en-US/User Guide/VPC and subnets/Manage VSwitches.md#). Alternatively, you can use the default options. You can also [modify the private IP address](../../../../intl.en-US/Network/Change IPv4 addresses/Change the private IP of an ECS instance.md#) after the migration.


## ApsaraDB setup { .section}

-   If your ECS instance hosts the ApsaraDB service, we recommend that you set up the [hybrid access of ApsaraDB](../../../../intl.en-US/Best practices/Migrate from the classic network to VPC/Database hybrid access/Hybrid access of ApsaraDB.md#) in advance because both Classic network and VPC ECS instances can access the ApsaraDB in this mode.

-   The private IP address of your ECS instance will change. Please [set the whitelist](../../../../intl.en-US/Quick Start for MySQL/Initial configuration/Set the whitelist.md#) to add the VSwitch CIDR block to the RDS whitelist in advance.


## Migration duration { .section}

A typical migration takes approximately 15 minutes. During the migration, you cannot operate the target instances. After migration, you will need to restart the affected ECS instances. We recommend that you schedule the migration during off-peak business hours to avoid major impacts to your services.

## Other issues to note { .section}

-   Before the migration, we recommend that you configure your applications as auto run upon instance start. We also recommend that availability monitoring is enabled.
-   After the migration, check whether:
    -   The software license code is changed.
    -   The zone of your ECS instance is changed. If the zone is changed, the associated services may be impacted \(such as ApsaraDB RDS, Redis or MongoDB\). We recommend that you migrate the zone to make sure your business run normally.
    -   The underlying virtualization technology is upgraded. If so, the ECS disk ID will be changed. In a Linux instance, disks will be marked as vda, vdb, and vdc.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10947/155909814843662_en-US.png)

        Alibaba Cloud will automatically restore the /etc/fstab file for Linux instances. However, you need to determine if other applications are dependent on the previous device names.

    -   Your ECS instance has been restarted or the kernel has been upgraded recently. If not, and no restart or upgrade has been performed for a long time, a restart may be subject to file system checks which can result in configuration change failure and restart failure.
    -   Data is synchronized on the disks in the background, and the duration depends on the disk capacity. Usually, it takes about four hours to synchronize 100 GiB of data. During the synchronization, the disk operations are suspended and the I/O performance will drop temporarily. After the synchronization, disk operations and the I/O performance will return to normal.

If exceptions occur, [open a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex). For users in Mainland China, you can also call 95187 to contact Alibaba Cloud.

## References { .section}

For more information about migrating ECS instances to VPCs, see [Alibaba Cloud physical server migration and upgrade notice](intl.en-US/ECS/ECS bulletin board/Alibaba Cloud physical server migration and upgrade notice.md#).

