# Alibaba Cloud physical server migration and upgrade notice {#concept_65448_zh .concept}

This notice details the physical servers on Alibaba Cloud that are subject to scheduled hardware and network upgrades in order to improve the performance and stability of ECS instances running on them. We recommend that you go to the [Pending Tasks](https://ecs.console.aliyun.com/#/events/unsettled/securityGroupWarning) page to check the detailed physical server list to learn which physical servers are affected.

## Migration details {#section_i25_pcj_dfb .section}

-   **Migration duration**: Approximately 15 minutes.

-   **Network modification**: From the Classic network to a [VPC](../../../../intl.en-US/Product Introduction/What is VPC?.md#).

-   **Software license code modification**: The software license code may change after the migration.

-   **IP address modifications**:

    -   If the Internet bandwidth of an ECS instance is 0 Mbit/s, the public IP address is automatically released after the migration.
    -   If the Internet bandwidth of an ECS instance is greater than 0 Mbit/s, the public IP address remains unchanged after the migration, but the NIC card is deleted and replaced with NatIP.
    -   The private IP address of an ECS instance is randomly assigned from the CIDR block of the target VSwitch. After the migration is complete, you can also [modify the private IP address](../../../../intl.en-US/Network/Change IPv4 addresses/Change the private IP of an ECS instance.md#) yourself.
-   **I/O performance impact**: After the migration, I/O performance will drop briefly, and the snapshot and disk functions will be disabled temporarily due to the need to append data to the underlying layer. Typically, it takes about four hours to add 100 GiB of data.


The migration process is shown in the following figure:

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10948/155549106544175_en-US.png)

## Prepare migration environment { .section}

1.  [Create a snapshot for your disk](../../../../intl.en-US/Snapshots/Use snapshots/Create a snapshot.md#) and back up the data.

2.  Prepare a secure network, including:
    -   \(Optional\) [VPC](../../../../intl.en-US/User Guide/VPC and subnets/Manage a VPC.md#) and [VSwitch](../../../../intl.en-US/User Guide/VPC and subnets/Manage VSwitches.md#). You can create your own VPC and VSwitch. Alternatively, you can use the default options.
    -   Security group. If there is no security group in the target VPC, you need to [create a security group of VPC type](../../../../intl.en-US/Security/Security groups/Create a security group.md#) or [clone a security group](../../../../intl.en-US//Clone a security group.md#). Besides, you need to check the security group rules to prevent business operations from being affected.
3.  Reserve at least 500 MiB system disk space.

4.  \(Optional\) After your ECS instances are migrated to the target VPC, if they need to communicate with other Classic network ECS instances in the current region, you can:
    -   Use [ClassicLink](../../../../intl.en-US/User Guide/Network connection/ClassicLink/ClassicLink overview.md#) to implement communication between the target VPC and the Classic network.
    -   [Migrate the remaining Classic network ECS instances to the target VPC](../../../../intl.en-US/Best practices/Migrate from the classic network to VPC/Migration overview.md#) at a later date.
5.  \(Optional\) If your ECS instance hosts the ApsaraDB service, you need to set up [hybrid access of ApsaraDB](../../../../intl.en-US/Best practices/Migrate from the classic network to VPC/Database hybrid access/Hybrid access of ApsaraDB.md#) in advance. In the hybrid mode, both Classic network and VPC ECS instances can access the ApsaraDB.
6.  \(Optional\) If your ECS instance hosts services such as ApsaraDB RDS, and you need the services to remain accessible, you need to [add the VSwitch CIDR block to the RDS whitelist](../../../../intl.en-US/User Guide/Security/Set the whitelist.md#) in advance.

7.  Disable or uninstall ECS instance security software.

    **Note:** This migration will update the ECS instance drivers, so yoexceptionsu will need to temporarily disable or uninstall the security software installed on your ECS instance.


## Schedule your migration {#section_icf_3lz_2fb .section}

1.  After you receive a notification about the planned physical server migration \(either by SMS or email\), log on to the [ECS console](https://ecs.console.aliyun.com/) and follow the instructions to schedule your migration.

**Note:** You cannot operate ECS instances that are associated with the target physical servers during a migration, and after the migration you must restart the affected ECS instances.

## \(Optional\) Modify the migration time {#section_pdv_xhj_dfb .section}

If you need to re-schedule the planned migration time, follow these steps:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/).

2.  In the upper right corner of the **Overview** page, click **Pending Tasks**.

3.  Choose **All Tasks** \> **Scheduled Instance Migration**. Then, select the target region \(in this example, **China East 2 \(Shanghai\)** is selected\), and select the instances whose migration time will be modified.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10948/155549106512006_en-US.png)

4.  Specify the new migration time in **Scheduled Date** and **Scheduled Time**.

    **Note:** The new migration time cannot be later than the **Latest Schedule Time**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/10948/155549106512007_en-US.png)

5.  Click **OK**.


## What to do next {#section_khd_llz_2fb .section}

1.  Remove unnecessary intranet IP addresses from other cloud product whitelists \(such as [RDS](../../../../intl.en-US/Product Introduction/What is Apsara DB for RDS.md#), [SLB](../../../../intl.en-US/Product Introduction/What is Server Load Balancer?.md#), [OSS](../../../../intl.en-US/Product Introduction/What is OSS?.md#), or [Container Service](../../../../intl.en-US/Product Introduction/What is Container Service.md#)\).

2.  Review the software license code changes caused by the deletion of the Network Interface Card \(NIC\). If the software on your ECS instance is associated with the MAC address of the NIC, and the software vendor approves the migration certificate of Alibaba Cloud, you can re-authorize your software. Otherwise, you need to make adjustments as needed or choose to roll back your system.

3.  \(Optional\) If your ECS instance has not been restarted for a long time, or was not restarted after the kernel upgrade, the system checks the file system and updates related configurations upon reboot. If issues occur [open a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to contact Alibaba Cloud.


## Subsidy scheme { .section}

This migration may impact your services. Alibaba Cloud apologizes for any inconvenience caused to you. If any exceptions occur, please promptly [open a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) or call 95187 to contact Alibaba Cloud \(users based in Mainland China only\).

Approximately seven working days after the completion of the migration, Alibaba Cloud will credit your account with vouchers that will allow you to purchase a [Subscription](../../../../intl.en-US/Pricing/Subscription.md#) instances or instances of the same configuration as your migrated ECS instances \(excluding the Internet bandwidth\) and which will cover the cost of the running instance or instances for one month thereafter.

## Troubleshooting { .section}

**Issue: The server migration is completed, but my website cannot be opened, my service is unavailable, or my database cannot be read from or written to anymore. What can I do**?

Check whether the new security group rules have disabled the corresponding communication port. If so, you can [clone the original security group rules](../../../../intl.en-US//Clone a security group.md#).

**Issue: Why is my software license code regarded as expired, invalid, or unavailable after the server migration**?

There are two possible causes:

-   The software has no license mobility program. In this case, we recommend that you contact the software vendor or distributor for re-authorization.
-   Some software applications register the valid environment by associating the NIC MAC address. However, after being migrated to the target VPC, the MAC address is lost. In this case, we recommend that you contact the software vendor to check if the software registers your instance by associating the NIC MAC address. If yes, you need to associate the instance primary NIC again. For more information, see [ENIs](../../../../intl.en-US/Network/Elastic Network Interfaces/ENI overview.md#).

**Issue: Why is the FTP service unavailable after migration**?

After the migration, the NIC card is deleted and the FTP service is unavailable. To resolve this issue, you can:

1.  [Convert the instance Internet IP to an Elastic Internet IP \(EIP\)](../../../../intl.en-US/Network/Change IPv4 addresses/Convert public IP address to EIP address.md#).
2.  [Configure the cut-through mode](../../../../intl.en-US/User Guide/Configure the cut-through mode.md#).

**Note:** Some of the [phased-out instance types](https://www.alibabacloud.com/help/faq-detail/55263.htm) and [last generation of entry-level instance type families](../../../../intl.en-US/Instances/Instance type families/Instance type families.md#xn4-n4-mn4-e4) do not support ENIs. We recommend that you [upgrade instance types](../../../../intl.en-US/Instances/Change configurations/Overview of configuration changes.md#) before implementing the above plan.

## References { .section}

For more information about migrating ECS instances to VPCs, see:

-   [Overview of migration to VPCs](../../../../intl.en-US/Best practices/Migrate from the classic network to VPC/Migration overview.md#)

-   [Notes for migrating ECS instances to VPCs](intl.en-US/ECS/ECS bulletin board/Notes for migrating ECS instances to VPCs.md#)


