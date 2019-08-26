# Cloud Migration tool FAQ {#ServerMigrationFAQ .reference}

-   [What scenarios can I use the Cloud Migration tool for?](#)
-   [What is the migration process of the Cloud Migration tool?](#)
-   [Does the Cloud Migration tool support resumable transfers?](#)
-   [Does the migration tool support incremental migration?](#)
-   [What are the results after the cloud migration is complete?](#)
-   [What do I do when the migration is complete and a custom image is displayed?](#)
-   [What can I do if the connection for cloud migration is closed or if migration fails?](#)
-   [What do I need to know about the intermediate instance?](#)
-   [What do I need to know about user\_config.json?](#)
-   [When do I need to filter a directory or file?](#)
-   [What do I need to know about the client\_data file?](#)
-   [When do I need to clear the client\_data file?](#)
-   [After cloud migration has been completed, how do I perform a new cloud migration?](#)
-   [What do I do if I released an intermediate instance by mistake?](#)
-   [Why have I received “NotEnoughBalance” error message?](#)
-   [Why have I received a “Forbidden.RAM” error message?](#)
-   [Why have I received a “Forbidden.Subuser” error message?](#)
-   [What Internet IP addresses and ports does my server need to access?](#)
-   [How can I check my system after migrating a Windows server?](#)
-   [Which Windows server licenses can Alibaba Cloud support activation for?](#)
-   [Before migrating a Linux server, how can I check that all of the requirements for cloud migration are met?](#)
-   [How can I check my system after migrating a Linux server?](#)

 **1. What scenarios can I use the Cloud Migration tool for?** 

The tool can migrate data from physical servers, virtual machines, and other cloud platform hosts to Alibaba Cloud ECS for most Windows Server and Linux operating systems. For more information, see [What is the Cloud Migration tool and P2V](intl.en-US/User Guide/Cloud Migration tool for P2V and V2V/Cloud Migration tool for P2V and V2V.md#).

 **2. What is the migration process of the Cloud Migration tool?** 

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22635/154872628713350_en-US.png)

-   Checks whether the source server meets the requirements for migration or not.
-   Creates an intermediate instance with a name INSTANCE\_FOR\_GO\_TOALIYUN. The files and the data of source server system are transferred to the intermediate instance.
-   Creates snapshots for the intermediate instance and then use the snapshots to create a custom image.

 **3. Does the Cloud Migration tool support resumable transfers?** 

Yes. The Cloud Migration tool does support resumable transfers. If the data transfer has been interrupted, you can restart the migration tool to continue from the previous stopping point.

 **4. Does the migration tool support incremental migration?** 

Not supported. Incremental data migration is not allowed. We recommend that applications such as databases and container services be paused, or related directories be [filtered](#Excludes) before migration to Alibaba Cloud. Synchronize any data related to those applications after the migration has been completed.

 **5. What are the results after the cloud migration is complete?** 

After a custom image of the source server is created, you can log on to the [ECS console](https://ecs.console.aliyun.com/) and view the custom image from the image list in the corresponding region.

 **6. What do I do after the migration is complete?** 

We recommend that you first create a Pay-As-You-Go instance and make sure that the system is operating normally. After confirming the image is functioning, select [instance types](../intl.en-US/Product Introduction/Instance type families.md#) and [create one or more ECS instances](intl.en-US/User Guide/Instances/Create an instance/Create an instance by using the wizard.md#).

**7. What can I do if the connection for cloud migration is closed or if migration fails?**

-   If the migration tool suddenly closes or becomes frozen, you can try restarting the operation to restore cloud migration.

-   If cloud migration fails and the prompt `Not Finished` is displayed, you can check the log files and directory, and look up the reported errors in the [Cloud Migration tool troubleshooting](intl.en-US/User Guide/Cloud Migration tool for P2V and V2V/Troubleshooting.md#) or [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

    If the issue is still not resolved, we recommend you join the [Cloud Migration Tool Support group on DingTalk](https://h5.dingtalk.com/invite-page/index.html?spm=a2c4g.11186623.2.31.x8X0fd&code=ca190154ff), an enterprise communication and collaboration platform Developed by Alibaba Group. You can also collect the log file and [open a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to contact after-sales customer support for assistance.


**8. What do I need to know about the intermediate instance?**

-   The Cloud Migration tool automatically creates, starts, stops, and releases intermediate instance. To make sure the cloud migration completes successfully, do not interfere with the status of the intermediate instance.

-   The default security group for the intermediate instance is on ports 8080 and 8703 in the inbound direction. As these are the cloud migration service ports, do not modify or delete the security group rules.

-   After cloud migration is complete, the intermediate instance is released automatically. If migration fails, you have to manually [release the instance](intl.en-US/User Guide/Instances/Release an instance.md#).


 **9. What do I need to know about user\_config.json?** 

If cloud migration has already started and the intermediate instance has already been created, do not change the system disk size or data disk size specified in the user\_config.json. If you still need to modify these parameters, you must first clear the client\_data file and then restart migration to cloud.

 **10. When do I need to filter a directory or file?** 

When the source server has data directories or files that do not need to be uploaded, they can be filtered out by configuring the “Excludes” file to improve the efficiency of cloud migration.

In particular, you can filter out databases, Docker containers, and other active data directories and files which cannot be paused to improve the stability of data transmission during migration.

 **11. What do I need to know about the client\_data file?** 

The client\_data file records data from the cloud migration process, including the intermediate instance information and migration progress. Do not manually modify or delete the client\_data file unless necessary, otherwise cloud migration may fail.

 **12. When do I need to clear the client\_data file?** 

To clear the client\_data file, you can use the [CLI command](intl.en-US/User Guide/Cloud Migration tool for P2V and V2V/CLI parameters.md#) `--cleardata`, or through the [Windows GUI](intl.en-US/User Guide/Cloud Migration tool for P2V and V2V/Windows GUI of Cloud Migration tool.md#) Client Data menu.

-   If you want to restart cloud migration after it has begun, you can clear the current client\_data file or use the default client\_data file to override the current file.

-   In cases where cloud migration fails, such as when the intermediate instance, VPC, VSwitch, or other security groups do not exist, you can try clearing the client\_data operation to resolve the issue.


 **13. After cloud migration has been completed, how do I perform a new cloud migration?** 

Clear the client\_data file, and then run the Cloud Migration tool again to perform a new cloud migration.

 **14. What do I do if I released an intermediate instance by mistake?** 

Clear the client\_data file, and then run the Cloud Migration tool again to perform a new cloud migration.

 **15. Why have I received “NotEnoughBalance” error message?** 

The Cloud Migration tool itself is free, but a [Pay-As-You-Go](../intl.en-US/Pricing/Pay-As-You-Go.md#) intermediate instance is created by default during cloud migration. Creating a Pay-As-You-Go instance requires the balance of any of your payment methods to be no less than 100 RMB to complete.

 **16. Why have I received a “Forbidden.RAM” error message?** 

The AccessKey created by your RAM user account does not have the permissions to manage ECS and VPC resources. We recommend that you contact the Alibaba Cloud user to grant [`AliyunECSFullAccess`](https://ram.console.aliyun.com/?#/policy/detail/system/AliyunECSFullAccess/info) and [`AliyunVPCFullAccess`](https://ram.console.aliyun.com/?#/policy/detail/system/AliyunVPCFullAccess/info) permissions.

 **17. Why have I received a “Forbidden.Subuser” error message?** 

The Cloud Migration tool must use the account AccessKeyID and AccessKeySecret to create an intermediate instance. If the RAM account does not have permission to create instances, a Forbidden.SubUser error occurs. We recommend that you use the Alibaba Cloud account to perform the cloud migration.

**18. What Internet IP addresses and ports does my server need to access?**

The on-premises server must be able to reach the following network address and communication port to access the related Alibaba Cloud services, uninterruptedly:

-   The nearest ECS endpoint: `https://ecs.aliyuncs.com:443`. For other regional endpoints, see API Reference [Request structure](../intl.en-US/API Reference/Getting started/Request structure.md#).

-   Virtual Private Cloud \(VPC\): `http://vpc.aliyuncs.com:443`.

-   Security Token \(STS\): `https://sts.aliyuncs.com:443`.

-   The intermediate instance: `https://xxx.xx.xxx.xx:8080` and `https://xxx.xx.xxx.xx:8703`. The `xxx.xx.xxx.xx` indicates the Internet IP address of the intermediate instance.


**Note:** The source server does not need to open any inbound ports, but it needs to have access in the outbound direction to the Internet IP addresses and ports.

 **19. How can I check my system after migrating a Windows server?** 

When you first start an instance of Windows after migration:

1.  Check whether the system disk data is complete or not.

2.  Go to the disc manager to check whether the disk is missing.

3.  If you are using Windows Server 2008 or a later system, wait for a moment while the automatic recovery of the file system access permission is processing.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22635/154872628713956_en-US.png)

    **Note:** If the Goto Aliyun Restore Tool is not started at the first startup attempt, you can run the C:\\go2aliyun\_prepare\\go2aliyun\_restore.exe to manually invoke the automatic recovery process. However, make sure that your ECS instance have mounted the same number of disks as the source server does.

4.  Check whether the network service is normal.

5.  Check that other system application services are operating normally.


 **20. Which Windows server licenses can Alibaba Cloud support activation for?** 

Alibaba Cloud allows you to activate licenses on Windows Server 2003, 2008, 2012, and 2016. For other versions of Windows not listed here, if they are migrated to ECS, you must [apply for a licensed mobility certificate](https://www.alibabacloud.com/help/doc-detail/84749.html).

 **21. Before migrating a Linux server, how can I check that all of the requirements for cloud migration are met?** 

You can use the client\_check tool that comes with the Cloud Migration tool. Run the `./client_check --check` when ready, if the test prompt displays `OK`, all the cloud migration requirements are met.

 **22. How can I check my system after migrating a Linux server?** 

When you first start a Linux instance after migration:

-   Check whether the system disk data is complete or not.
-   If a data disk exists, you must [mount the data disk](intl.en-US/User Guide/Cloud disks/Attach a cloud disk.md#).
-   Check whether the network service is running normally.
-   Check whether other system services are operating normally.

