# Migrate your instance within Alibaba Cloud ECS {#concept_pp2_xjw_fgb .concept}

This topic describes how to migrate your instance within Alibaba Cloud ECS.

If you want to migrate your ECS instance within Alibaba Cloud ECS, we recommend that you [Copy images](../../../../../reseller.en-US/Images/Custom image/Copy images.md#) and [Share images](../../../../../reseller.en-US/Images/Custom image/Share images.md#). If these two methods do not apply, you can use the following procedures as needed.

## Migrate your ECS instance within the same VPC {#section_azd_vsw_fgb .section}

This method applies to scenarios where you need to shrink your ECS disk volume. For more information, see [Shrink disk volume](reseller.en-US/Best Practices/Shrink disk volume.md#).

In these scenarios, we recommend that you migrate your instance through VPC to maximize transfer efficiency. For more information, see [VPC-based migration](reseller.en-US/Migration service/Migration service/Migration solutions/VPC-based migration.md#).

## Migrate your ECS Windows instance between different VPCs {#section_zdh_5tw_fgb .section}

This method applies to scenarios where you need to migrate your ECS Windows instance between different accounts, regions, or VPCs.

**Preparations**

1.  Create a snapshot to back up your data.
2.  Check the validity of your application licenses.

    **Note:** After your ECS instance is migrated between different Alibaba Cloud VPCs, the underlying hardware devices of the system will change, which may result in the associated application licenses becoming invalid.

3.  Check your network environment.
    -   If your network uses international regions, the migration may be slow due to unstable network connections.
    -   If your network can connect to VPC, see [VPC-based migration](reseller.en-US/Migration service/Migration service/Migration solutions/VPC-based migration.md#).
4.  Verify that the Windows VSS service is enabled.
5.  Check whether you have installed the qemu-agent tool. If so, uninstall it. For more information, see [Cloud Migration tool FAQ](reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Cloud Migration tool FAQ.md#).
6.  We recommend that you use a test machine to conduct migration tests before completing the actual procedure to ensure the migration is successful.

**Procedure**

1.  [Download and install the Cloud Migration tool](../../../../../reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#section_twq_sxz_jfb) onto the server to be migrated.
2.  Configure the user\_config.json file.

    The user\_config.json file contains the following configuration items:

    -   The AccessKey information of your Alibaba Cloud account
    -   The target zone of migration and the name of the target image
    -   \(Optional\) The size of the target system disk and the configuration of the target data disks
    -   The platform and architecture of the source system to be migrated
    For the configuration methods of these items, see [Configure the user\_config.json file](../../../../../reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#section_p5x_xzz_jfb).

3.  \(Optional\) Configure the directories or files that do not need to be migrated. For more information, see [Exclude files or directories from migration](../../../../../reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#section_tzq_sxz_jfb).
4.  Run the main program of the Cloud Migration tool.

    Run go2aliyun\_client.exe or go2aliyun\_gui.exe as the administrator. If the main program is a GUI version, click the **Start** button to start the migration.


## Migrate your ECS Linux instance between different VPCs {#section_mbw_s1k_pgb .section}

This method applies to scenarios where you need to migrate your ECS Linux instance between different accounts, regions, or VPCs.

**Preparations**

1.  Create a snapshot to back up your data.
2.  Check the validity of your application licenses.

    **Note:** After your ECS instance is migrated between different Alibaba Cloud VPCs, the underlying hardware devices of the system will change, which may result in the associated application licenses becoming invalid.

3.  Check your network environment.
    -   If your network uses international regions, the migration may be slow due to unstable network connections.
    -   If your network can connect to VPC, see [VPC-based migration](reseller.en-US/Migration service/Migration service/Migration solutions/VPC-based migration.md#).
4.  [Download and install the Cloud Migration tool](../../../../../reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#section_twq_sxz_jfb).
5.  Go to the directory where the Cloud Migration tool is located. Run the `./Check/client_check --check` command to check whether the EC2 instance to be migrated meets the migration conditions.

    **Note:** If all check items are `OK`, you can start the migration. Otherwise, you need to check the GRUB bootloader and [Upgrade GRUB to 1.99 or a later version](https://partners-intl.aliyun.com/help/product/62807.htm) \(applicable to systems with earlier kernels \(such as CentOS 5, Red Hat 5, and Debian 7\)\) as the root user.

6.  We recommend that you use a test machine to conduct migration tests before completing the actual procedure to ensure the migration is successful.

**Procedure**

1.  Configure the user\_config.json file.

    The user\_config.json file contains the following configuration items:

    -   The AccessKey information of your Alibaba Cloud account
    -   The target zone of migration and the name of the target image
    -   \(Optional\) The size of the target system disk and the configuration of the target data disks
    -   The platform and architecture of the source system to be migrated
    For the configuration methods of these items, see [Configure the user\_config.json file](../../../../../reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#section_p5x_xzz_jfb).

2.  \(Optional\) Configure the directories or files that do not need to be migrated. For more information, see [Exclude files or directories from migration](../../../../../reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#section_tzq_sxz_jfb).
3.  Run the following command as the root user to grant the execution permission to the main program, and then run this program.

    ```
    chmod +x go2aliyun_client
    ./go2aliyun_client
    ```

4.  Wait until the main program of the Cloud Migration tool has been completely executed. When the message Go to Aliyun Finished! is displayed, the migration is successfully completed.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65301/155488212838196_en-US.png)


