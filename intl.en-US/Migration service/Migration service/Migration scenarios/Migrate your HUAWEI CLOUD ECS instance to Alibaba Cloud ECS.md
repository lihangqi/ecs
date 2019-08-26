# Migrate your HUAWEI CLOUD ECS instance to Alibaba Cloud ECS {#concept_s3g_lcw_fgb .concept}

This topic describes how to migrate your HUAWEI CLOUD ECS instance to Alibaba Cloud ECS.

## Migrate your HUAWEI CLOUD ECS Windows instance to Alibaba Cloud {#section_r4w_rcw_fgb .section}

**Preparations**

1.  Create a snapshot to back up your data.
2.  Ensure that your ECS instance can access the following websites and ports:
    1.  ECS: `https://ecs.aliyuncs.com:443`.

        **Note:** For information about ECS API endpoints of other regions, see [Endpoints](../../../../../intl.en-US/API Reference/Getting started/Request structure.md#section_mtp_xvb_wdb).

    2.  VPC: `https://vpc.aliyuncs.com:443`.
    3.  STS: `https://sts.aliyuncs.com:443`.
    4.  Intermediate instance: port 8080 and port 8703.

        **Note:** An intermediate instance is a temporary instance that is automatically created during the running of the Cloud Migration tool. If a network connection error occurs during the migration, you need to ensure that the ECS instance to be migrated has access to port 8080 and port 8703 of the intermediate instance by running the following commands:

        ```
        telnet xxx.xx.xxx.xx 8080  # where, xxx.xx.xxx.xx is the Internet IP address of the intermediate instance. When you perform the migration through VPC, xxx.xx.xxx.xx is the private IP address of the intermediate instance.
        telnet xxx.xx.xxx.xx 8703  # where, xxx.xx.xxx.xx is the Internet IP address of the intermediate instance.When you perform the migration through VPC, xxx.xx.xxx.xx is the private IP address of the intermediate instance.
        ```

3.  Check whether you have installed QEMU Guest Agent VSS Provider. If so, go to the installation directory \(for example, `C:\Program Files (x86)\virtio\monitor`\), and then locate and run the uninstall.bat script to uninstall QEMU Guest Agent.
4.  Ensure that the Windows VSS service is enabled.
5.  Check whether you have installed the qemu-agent tool. If so, uninstall it. For more information, see [Cloud Migration tool FAQ](intl.en-US/Migration service/Cloud Migration tool for P2V and V2V/Cloud Migration tool FAQ.md#).
6.  Check the validity of your application licenses.

    **Note:** After your instance is migrated to Alibaba Cloud, the underlying hardware devices of the system will change, which may result in the associated application licenses becoming invalid.

7.  We recommend that you use a test machine to conduct migration tests before completing the actual procedure to ensure the migration is successful. 

**Procedure**

1.  [Download and install the Cloud Migration tool](../../../../../intl.en-US/Migration service/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#section_twq_sxz_jfb) onto the server to be migrated.
2.  Configure the user\_config.json file.

    The user\_config.json file contains the following configuration items:

    -   The AccessKey information of your Alibaba Cloud account
    -   The target zone of migration and the name of the target image
    -   \(Optional\) The size of the target system disk and the configuration of the target data disks
    -   The platform and architecture of the source system to be migrated
    For the configuration methods of these items, see [Configure the user\_config.json file](../../../../../intl.en-US/Migration service/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#section_p5x_xzz_jfb).

3.  \(Optional\) Configure the directories or files that do not need to be migrated. For more information, see [Exclude files or directories from migration](../../../../../intl.en-US/Migration service/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#section_tzq_sxz_jfb).
4.  Run the main program of the Cloud Migration tool.

    Run go2aliyun\_client.exe or go2aliyun\_gui.exe as the administrator. If the main program is a GUI version, click the **Start** button to start the migration.


## Migrate your HUAWEI CLOUD ECS Linux instance to Alibaba Cloud {#section_tjp_fv4_4gb .section}

**Preparations**

1.  Create a snapshot to back up your data.
2.  Ensure that your ECS instance can access the following websites and ports:
    1.  ECS: `https://ecs.aliyuncs.com:443`.

        **Note:** For information about ECS API endpoints of other regions, see [Endpoints](../../../../../intl.en-US/API Reference/Getting started/Request structure.md#section_mtp_xvb_wdb).

    2.  VPC: `https://vpc.aliyuncs.com:443`.
    3.  STS: `https://sts.aliyuncs.com:443`.
    4.  Intermediate instance: port 8080 and port 8703.

        **Note:** An intermediate instance is a temporary instance that is automatically created during the running of the Cloud Migration tool. If a network connection error occurs during the migration, you need to ensure that the ECS instance to be migrated has access to port 8080 and port 8703 of the intermediate instance by run the following commands:

        ```
        telnet xxx.xx.xxx.xx 8080  # where, xxx.xx.xxx.xx is the Internet IP address of the intermediate instance. When you perform the migration through VPC, xxx.xx.xxx.xx is the private IP address of the intermediate instance.
        telnet xxx.xx.xxx.xx 8703  # where, xxx.xx.xxx.xx is the Internet IP address of the intermediate instance.When you perform the migration through VPC, xxx.xx.xxx.xx is the private IP address of the intermediate instance.
        ```

3.  Check the validity of your application licenses.

    **Note:** After your instance is migrated to Alibaba Cloud, the underlying hardware devices of the system will change, which may result in the associated application licenses becoming invalid.

4.  We recommend that you use a test machine to conduct migration tests before completing the actual procedure to ensure the migration is successful. 

**Procedure**

1.  Download and decompress the Cloud Migration tool.
2.  Run the client\_check script of the tool to check whether the ECS instance to be migrated meets the migration conditions.
    1.  Run the following command to download the Cloud Migration tool to the server to be migrated:

        ```
        wget http://p2v-tools.oss-cn-hangzhou.aliyuncs.com/Alibaba_Cloud_Migration_Tool.zip
        ```

    2.  Run the following command to decompress the Cloud Migration tool:

        ```
        unzip Alibaba_Cloud_Migration_Tool.zip
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65301/155255866638160_en-US.png)

    3.  Run the following command to view the hardware architecture of the Linux server to be migrated and decompress the Cloud Migration tool package that applies to this hardware architecture:

        ```
        uname -a 
        unzip <the Cloud Migration tool package that applies to the hardware architecture of the Linux system to be migrated>
        ```

        In this example, the Linux hardware architecture is `x86_64`. Therefore, the Cloud Migration tool package that applies to this hardware architecture is go2aliyun\_client1.3.2.3\_linux\_x86\_64.zip.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65301/155255866638161_en-US.png)

    4.  Run the following command to access the directory where the decompressed Cloud Migration tool is located:

        ```
        cd <the directory where the decompressed Cloud Migration tool is located>
        ```

        In this example, the command is `cd go2aliyun_client1.3.2.3_linux_x86_64`.

    5.  Run the following command to check whether the Linux server meets the migration conditions:

        ```
        chmod +x ./Check/client_check
        ./Check/client_check --check
        ```

        If all check items are OK, it means that the Linux server meets the migration conditions and you can start the migration.

3.  Set the migration parameters as needed, and then run the Cloud Migration tool.
    1.  Configure the user\_config.json file.

        The user\_config.json file contains the following configuration items:

        -   The AccessKey information of your Alibaba Cloud account
        -   The target zone of migration and the name of the target image
        -   \(Optional\) The size of the target system disk and the configuration of the target data disks
        -   The platform and architecture of the source system to be migrated
        For the configuration methods of these items, see [Configure the user\_config.json file](../../../../../intl.en-US/Migration service/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#section_p5x_xzz_jfb).

    2.  \(Optional\) Configure the directories or files that do not need to be migrated. For more information, see [Exclude files or directories from migration](../../../../../intl.en-US/Migration service/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#section_tzq_sxz_jfb).
    3.  Run the following command as the root user to grant the execution permission to the main program, and then run this program.

        ```
        chmod +x go2aliyun_client
        ./go2aliyun_client
        ```

    4.  Wait until the main program of the Cloud Migration tool has been completely executed. When the message Go to Aliyun Finished! is displayed, the migration is successfully completed.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65301/155255866638196_en-US.png)


