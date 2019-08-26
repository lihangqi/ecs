# Migrate your VMware VM to Alibaba Cloud ECS {#concept_cjl_wzp_fgb .concept}

This topic describes how to migrate your VMware Virtual Machine \(VM\) to Alibaba Cloud ECS.

## Migrate your VMWare Windows VM to Alibaba Cloud {#section_fww_mhp_fgb .section}

**Preparations**

1.  Create a snapshot to back up your data.
2.  Make sure that the system time is the same as the standard time of the local region.
3.  Ensure that your VM can access the following websites and ports:
    1.  ECS: `https://ecs.aliyuncs.com:443`.

        **Note:** For information about ECS API endpoints of other regions, see [Endpoints](../../../../../reseller.en-US/API Reference/Getting started/Request structure.md#section_mtp_xvb_wdb).

    2.  VPC: `https://vpc.aliyuncs.com:443`.
    3.  STS: `https://sts.aliyuncs.com:443`.
    4.  Intermediate instance: port 8080 and port 8703.

        **Note:** An intermediate instance is a temporary instance that is automatically created during the running of the Cloud Migration tool. If a network connection error occurs during the migration, you need to ensure that the VM to be migrated has access to port 8080 and port 8703 of the intermediate instance by running the following commands:

        ```
        telnet xxx.xx.xxx.xx 8080  # where, xxx.xx.xxx.xx is the Internet IP address of the intermediate instance. When you perform the migration through VPC, xxx.xx.xxx.xx is the private IP address of the intermediate instance.
        telnet xxx.xx.xxx.xx 8703  # where, xxx.xx.xxx.xx is the Internet IP address of the intermediate instance.When you perform the migration through VPC, xxx.xx.xxx.xx is the private IP address of the intermediate instance.
        ```

4.  Ensure that the Windows VSS service is enabled.
5.  Check whether you have installed the qemu-agent tool. If so, uninstall it. For more information, see [Cloud Migration tool FAQ](reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Cloud Migration tool FAQ.md#).
6.  Check the validity of your application licenses.

    **Note:** After your VM is migrated to Alibaba Cloud, the underlying hardware devices of the system will change, which may result in the associated application licenses becoming invalid.

7.  We recommend that you use a test machine to conduct migration tests before completing the actual procedure to ensure the migration is successful.

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


## Migrate your VMWare Linux VM to Alibaba Cloud {#section_lld_spp_fgb .section}

**Preparations**

1.  Create a snapshot to back up your data.
2.  Make sure that the system time is the same as the standard time of the local region.
3.  Ensure that your VM can access the following websites and ports:
    1.  ECS: `https://ecs.aliyuncs.com:443`.

        **Note:** For information about ECS API endpoints of other regions, see [Endpoints](../../../../../reseller.en-US/API Reference/Getting started/Request structure.md#section_mtp_xvb_wdb).

    2.  VPC: `https://vpc.aliyuncs.com:443`.
    3.  STS: `https://sts.aliyuncs.com:443`.
    4.  Intermediate instance: port 8080 and port 8703.

        **Note:** An intermediate instance is a temporary instance that is automatically created during the running of the Cloud Migration tool. If a network connection error occurs during the migration, you need to ensure that the VM to be migrated has access to port 8080 and port 8703 of the intermediate instance by running the following commands:

        ```
        telnet xxx.xx.xxx.xx 8080  # where, xxx.xx.xxx.xx is the Internet IP address of the intermediate instance. When you perform the migration through VPC, xxx.xx.xxx.xx is the private IP address of the intermediate instance.
        telnet xxx.xx.xxx.xx 8703  # where, xxx.xx.xxx.xx is the Internet IP address of the intermediate instance.When you perform the migration through VPC, xxx.xx.xxx.xx is the private IP address of the intermediate instance.
        ```

4.  [Download and install the Cloud Migration tool](../../../../../reseller.en-US/Migration service/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#section_twq_sxz_jfb).
5.  Go to the directory where the Cloud Migration tool is located. Run the `./Check/client_check --check` command to check whether the VM to be migrated meets the migration conditions.

    **Note:** If all check items are `OK`, you can start the migration. Otherwise, you need to conduct the following additional checks:

    1.  Check SELinux. For CentOS or Red Hat systems, check whether SELinux is disabled. If SELinux is enabled, disable it by using either of the following methods:
        1.  Run the `setenforce 0` command to disable SELinux temporarily.
        2.  Modify the /etc/selinux/config file to set `SELINUX=disabled` to disable SELinux permanently.
    2.  Check the virtualization driver. For more information, see [Install the virtio driver](../../../../../reseller.en-US/Images/Custom image/Import images/Install virtio driver.md#).
    3.  Check the GRUB bootloader and upgrade GRUB to 1.99 or a later version for systems with earlier kernel versions \(such as CentOS 5, Red Hat 5, and Debian 7\). For more information, see [Update GRUB 1.99 for a Linux server](https://partners-intl.aliyun.com/help/product/62807.htm).
6.  Check the validity of your application licenses.

    **Note:** After your VM is migrated to Alibaba Cloud, the underlying hardware devices of the system will change, which may result in the associated application licenses becoming invalid.


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

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65301/155488187938196_en-US.png)


**Note:** After your VMware VM is successfully migrated to Alibaba Cloud ECS, you no longer need VMtools to manage the relevant instance in Alibaba Cloud.

