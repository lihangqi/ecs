# VPC-based migration {#concept_dxp_5kk_yfb .concept}

If you can directly access a VPC from your on-premises IDC, virtual machine, or cloud host, but want to fully migrate your services to Alibaba Cloud, you can connect your source server with your target VPC to easily migrate your services. Compared with migrating your cloud services through the Internet, migrating your cloud services using Alibaba Cloud VPC transfers data at faster speeds and with greater stability.

You can use [Express Connect](../../../../../intl.en-US/Product Introduction/What is Express Connect?.md#) and [VPN](../../../../../intl.en-US/Product Overview/What is VPN Gateway?.md#) to connect with the VPC, and then use the Cloud Migration tool to perform a VPC-based migration.

## Context {#section_a2f_3lp_yfb .section}

The V1.2.8 Cloud Migration tool and later versions support VPC-based migration. To perform a VPC-based migration, you need to set the net\_mode field of client\_data to 1 or 2.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65304/155471428833339_en-US.png)

The options of the net\_mode parameter are described as follows:

-   0: the default value, which indicates Internet-based migration. The system to be migrated must support data transfer through the Internet.
-   1: indicates that the system to be migrated can access the specified VPC. The migration process is divided into phase 1, phase 2, and phase 3. In phase 2, data is transferred in the current system. In phase 1 and phase 3, data is transferred in other Internet environments.
-   2: indicates that the system to be migrated can access the Internet and the specified VPC. Data is transferred through the specified VPC.

Different parameter settings apply to different migration methods.

## Method 1 {#section_l1v_55p_yfb .section}

If you set net\_mode to 1, follow these steps to migrate the system:

1.  Create an intermediate instance in the Internet environment.

    1.  Log on to the target system \(system A, in this example\) that has access to the Internet, and then download the Cloud Migration tool.
    2.  Configure the user\_config.json file.
    3.  Set the target vpc\_id, vswitch\_id, and zone\_id in the client\_data file. For more information, see [Configure the client\_data file to the specified VPC](#).
    4.  Run the Cloud Migration tool until the message `Stage 1 is done!` is displayed.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65304/155471428933354_en-US.png)

2.  Transfer system data in the VPC.

    1.  Log on to the system to be migrated to the VPC \(system B, in this example\).
    2.  Copy the Cloud Migration tool from system A to system B.

        **Note:** The user\_config.json file and the client\_data file in system B must be the same as those in the Cloud Migration tool in system A.

    3.  Run the Cloud Migration tool until the message `Stage 2 is done!` is displayed.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65304/155471428933355_en-US.png)

3.  Create an image in the Internet environment.

    1.  Go back to system A, and then copy the Cloud Migration tool from system B to system A.

        **Note:** The user\_config.json file and the client\_data file must be the same as those in the Cloud Migration tool in system A.

    2.  Run the Cloud Migration tool until the message `Stage 3 is done!` is displayed, which indicates the cloud migration is finished.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65304/155471429033356_en-US.png)


## Method 2 {#section_jtg_jwp_yfb .section}

If you set net\_mode to 2, follow these steps to migrate the system:

1.  Log on to the system to be migrated, and then download the Cloud Migration tool.
2.  Configure the user\_config.json file.
3.  Set the target vpc\_id, vswitch\_id, and zone\_id in the client\_data file. For more information, see [Configure the client\_data file to the specified VPC](#).
4.  Run the Cloud Migration tool until the migration is completed.

**Note:** During the migration, data is transferred through the VPC in the data migration phase, or through the Internet in other phases.

## Configure the client\_data file. {#clientData .section}

To configure the client\_data file to the specified VPC, follow these steps:

1.  Set vpc\_id to the ID of the specified VPC.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65304/155471429033357_en-US.png)

2.  Set vswitch\_id to the ID of the specified VSwitch.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65304/155471429033358_en-US.png)

3.  Set zone\_id to the ID of the specified zone.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65304/155471429133359_en-US.png)

4.  \(Optional\) Set security\_group\_id to the ID of the specified security group. If you do not set this parameter, it will be automatically created.

    **Note:** The specified security group must enable port 8080 and port 8703 in the inbound direction.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65304/155471429133360_en-US.png)


