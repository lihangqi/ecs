# Migrate your Azure instance to Alibaba Cloud ECS {#concept_o3c_xgv_fgb .concept}

This topic describes how to migrate your Azure instance to Alibaba Cloud ECS.

## Migrate your Azure Windows instance to Alibaba Cloud {#section_lvr_zf4_4gb .section}

**Preparations**

1.  Create a snapshot to back up your data.
2.  Check the validity of your application licenses.

    **Note:** After your Azure instance is migrated to Alibaba Cloud, the underlying hardware devices of the system will change, which may result in the associated application licenses becoming invalid.

3.  Check your network environment.
    -   If your network uses international regions, see [Cloud migration across international regions](#section_GlobalP2V).
    -   If your network can connect to VPC, see [VPC-based migration](reseller.en-US/Migration service/Migration service/Migration solutions/VPC-based migration.md#).
4.  Ensure that the Windows VSS service is enabled.
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


## Migrate your Azure Linux instance to Alibaba Cloud {#section_qn4_zbv_fgb .section}

**Preparations**

1.  Create a snapshot to back up your data.
2.  Check the validity of your application licenses.

    **Note:** After your Azure instance is migrated to Alibaba Cloud, the underlying hardware devices of the system will change, which may result in the associated application licenses becoming invalid.

3.  Check your network environment.
    -   If your network uses international regions, see [Cloud migration across international regions](#section_GlobalP2V).
    -   If your network can connect to VPC, see [VPC-based migration](reseller.en-US/Migration service/Migration service/Migration solutions/VPC-based migration.md#).
4.  [Download and install the Cloud Migration tool](../../../../../reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#section_twq_sxz_jfb).
5.  Go to the directory where the Cloud Migration tool is located. Run the `./Check/client_check --check` command to check whether the Azure instance to be migrated meets the migration conditions.

    **Note:** If all check items are `OK`, you can start the migration. Otherwise, you need to perform the following additional checks:

    -   Check the cloud-init service. For more information, see [Install cloud-init](../../../../../reseller.en-US/Images/Custom image/Import images/Install cloud-init for Linux images.md#).
    -   Check the GRUB bootloader. [Upgrade GRUB to 1.99 or a later version](https://partners-intl.aliyun.com/help/product/62807.htm) for systems with earlier kernel versions \(such as CentOS 5, Red Hat 5, and Debian 7\) as the root user.
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

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65301/155488195938196_en-US.png)


## Cloud migration across international regions {#section_GlobalP2V .section}

1.  Migrate the Azure instance to the corresponding international region of Alibaba Cloud. For more information, see [Full migration](reseller.en-US/Migration service/Migration service/Migration solutions/Full migration.md#). For example, if the Azure instance is located in a region in the United States \(such as US East \(N. Virginia\)\), you can migrate it to an Alibaba Cloud region that is also in the United States \(such as US East 1\). For information about regions and their corresponding IDs, see [Regions and zones](../../../../../reseller.en-US/General Reference/Regions and Zones.md#section_ug5_k5k_xdb).
2.  Copy the newly created image to the target Alibaba Cloud region. For more information, see [Copy images](../../../../../reseller.en-US/Images/Custom image/Copy images.md#).
3.  Use this image to create an instance in the target Alibaba Cloud region. For more information, see [Create an instance by using a custom image](../../../../../reseller.en-US/Instances/Create an instance/Create an instance by using a custom image.md#).

