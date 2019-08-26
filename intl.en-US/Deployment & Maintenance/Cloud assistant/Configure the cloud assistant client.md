# Configure the cloud assistant client {#concept_wtg_32x_ydb .concept}

The cloud assistant client is an agent that is used to run cloud assistant commands on ECS instances. This topic illustrates how to install, update, start, and stop the cloud assistant client.

## Install the client through a download link {#section_e5n_k2x_ydb .section}

**Note:** 

-   ECS instances created using public images after December 1, 2017 are pre-installed with the cloud assistant client. For ECS instances created before December 1, 2017, manual installation of the cloud assistant client is required.
-   For ECS instances created using custom images or Alibaba Cloud Marketplace images, refer to [Cloud assistant](../reseller.en-US/Deployment & Maintenance/Cloud assistant/Cloud assistant overview.md#) to check whether your instance type and operating system meet the requirements to install the cloud assistant.

See the following steps to install the cloud assistant client for Windows instances:

1.  [Remotely connect to a Windows instance](../reseller.en-US/Instances/Connect to instances/Connect to Windows instances/Connect to a Windows instance.md#).
2.  [Download the cloud assistant client](https://repo-aliyun-assist.oss-cn-beijing.aliyuncs.com/download/aliyun_agent_setup.exe).
3.  Double-click the installation file and follow the instructions to install the client.

    **Note:** By default Windows instance installs the cloud assistant client into the C:\\ProgramData\\aliyun\\assist\\ directory.

4.  \(Only classic network-connected instance\) Create a file in the directory where cloud assistant client is installed, set the file name as region-id, any file format is supported. Open the file and write down the region-id where the ECS instance belongs, for example, cn-hangzhou. For more about optional values of regions, see [Regions and zones](../../../../../reseller.en-US/General Reference/Regions and zones.md#).

Based on the operating system of your Linux instances, select one of the following methods to install the cloud assistant client:

-   RPM package installation applicable to operating systems such as CentOS, RHEL, and SUSE Linux:
    1.  [Remotely connect to a Linux instance](../reseller.en-US/Instances/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using a password.md#).
    2.  Run the `wget https://repo-aliyun-assist.oss-cn-beijing.aliyuncs.com/download/aliyun_assist.rpm` command to download the RPM package of the cloud assistant client.
    3.  Run the `rpm -ivh aliyun_assist.rpm` command to install the cloud assistant client.
    4.  \(Only classic network-connected instance\) Create a file in the directory where cloud assistant client is installed, set the file name as region-id, any file format is supported. Open the file and write down the region-id where the ECS instance belongs, for example, cn-hangzhou. For more about optional values of regions, see [Regions and zones](../../../../../reseller.en-US/General Reference/Regions and zones.md#).
-   Debian package installation applicable to operating systems such as Debian and Ubuntu:
    1.  Remotely connect to a Linux instance.
    2.  Run the `wget https://repo-aliyun-assist.oss-cn-beijing.aliyuncs.com/download/aliyun_assist.deb` command to download the cloud assistant client package.
    3.  Run the `dpkg -i aliyun_assist.deb` command to install the cloud assistant client.
    4.  \(Only classic network-connected instance\) Create a file in the directory where cloud assistant client is installed, set the file name as region-id, any file format is supported. Open the file and write down the region-id where the ECS instance belongs, for example, cn-hangzhou. For more about optional values of regions, see [Regions and zones](../../../../../reseller.en-US/General Reference/Regions and zones.md#).
-   Installation through source code compilation:
    1.  Remotely connect to a Linux instance.
    2.  Run the `git clone https://github.com/aliyun/aliyun_assist_client` command to download the source code of the cloud assistant client.
    3.  Enter the source code directory.
    4.  Run the `cmake .` command to generate the compilation file.

        **Note:** If the `CMAKE_MINIMUM_REQUIRED` error is reported during compilation, go to the [CMake official website](https://cmake.org/download/) to update the CMake service to version 3.1 or later.

    5.  Run the `make` command to start compilation.
    6.  Run the `./cmake_install.sh` command to install the cloud assistant client.
    7.  \(Only classic network-connected instance\) Create a file in the directory where cloud assistant client is installed, set the file name as region-id, any file format is supported. Open the file and write down the region-id where the ECS instance belongs, for example, cn-hangzhou. For more about optional values of regions, see [Regions and zones](../../../../../reseller.en-US/General Reference/Regions and zones.md#).

**Note:** By default Linux instance installs the cloud assistant client into the following directories:

-   CoreOS: /opt/local/share/aliyun-assist/
-   Other Linux distributions \(Such as Ubuntu, Debian, Red Hat, SUSE Linux Enterprise Server, OpenSUSE, and Aliyun Linux\): /usr/local/share/aliyun-assist/

## Install the client through Alibaba Cloud CLI {#section_qkk_yt2_ngb .section}

Prerequisites

-   Alibaba Cloud CLI must be installed.
-   You have obtained the region ID of your instance. For more information about the region ID, see [Regions and zones](../../../../../reseller.en-US/General Reference/Regions and zones.md#).

Procedure

1.  Call [DescribeCloudAssistantStatus](../reseller.en-US/API Reference/Cloud assistant/DescribeCloudAssistantStatus.md#) to check whether the cloud assistant client is installed on the instance.

    ``` {#codeblock_d44_4hy_ttg}
    aliyun ecs DescribeCloudAssistantStatus --RegionId TheRegionId --InstanceId. 1 i-bp1g6zv0ce8ogXXXXXXp --output cols=CloudAssistantStatus
    ```

    If `CloudAssistantStatus=true` is returned, it indicates that the cloud assistant client has been installed on the instance. Otherwise, go to the next step.

2.  Call [InstallCloudAssistant](../reseller.en-US/API Reference/Cloud assistant/InstallCloudAssistant.md#) to install the cloud assistant client on the instance.

    ``` {#codeblock_tw9_dxq_67s}
    aliyun ecs InstallCloudAssistant --RegionId TheRegionId --InstanceId. 1 i-bp1g6zv0ce8ogXXXXXXp
    ```

3.  Call [RebootInstance](../reseller.en-US/API Reference/Instances/RebootInstance.md#) to restart the instance.

    ``` {#codeblock_50b_59s_rs7}
    aliyun ecs RebootInstance --RegionId TheRegionId --InstanceId i-bp1g6zv0ce8ogXXXXXXp
    ```

4.  \(Only classic network-connected instance\) Create a file in the directory where cloud assistant client is installed, set the file name as region-id, any file format is supported. Open the file and write down the region-id where the ECS instance belongs, for example, cn-hangzhou. For more about optional values of regions, see [Regions and zones](../../../../../reseller.en-US/General Reference/Regions and zones.md#).

## Update the client {#section_r34_32x_ydb .section}

The update process of the cloud assistant client runs every hour to query the update resources for the client. The update process is located in the following directories:

-   Windows instances: C:\\ProgramData\\aliyun\\assist\\$\{version\}/aliyun\_assist\_update
-   Linux instances: /usr/local/share/aliyun-assist/$\{version\}/aliyun\_assist\_update

When automatic update fails, you can [create an update command](../reseller.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Create a script.md#) or call the [CreateCommand](../reseller.en-US/API Reference/Cloud assistant/CreateCommand.md#) API to update the client at a specified time. This example shows you how to update the client by using a PRM package.

``` {#codeblock_ljn_qwp_01m}
wget https://repo-aliyun-assist.oss-cn-beijing.aliyuncs.com/download/aliyun_assist.rpm
rpm -U aliyun_assist.rpm
```

## Disable client update {#section_r3q_yps_52b .section}

The update process of the cloud assistant client is enabled by default. The following procedure describes how to disable the process:

-   Windows instances: Run the `rename aliyun_assist_update` command in Command Prompt.
-   Linux instances: Run the `chmod a-x aliyun_assist_update` command.

## Start or stop the client {#section_rlc_n2x_ydb .section}

Windows instances

1.  [Remotely connect to a Windows instance](../reseller.en-US/Instances/Connect to instances/Connect to Windows instances/Connect to a Windows instance.md#).
2.  Choose **Computer Management** \> **Services and Applications** \> **Services** and locate **AliyunService**.

    **Warning:** **AliyunService** is the process name of the cloud assistant client. Stopping **AliyunService** will also stop the cloud assistant client. As a result, ECS instance exceptions may occur and running ECS instances cannot be stopped in the ECS console. Use caution when you stop AliyunService.

3.  Choose **Stop** or **Restart** from the shortcut menu.

    ![Restart](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9582/15635138565250_en-US.png)


Linux instances

1.  [Remotely connect to a Linux instance](../reseller.en-US/Instances/Connect to instances/Connect to Linux instances/Connect to a Linux instance by using a password.md#).
2.  Run the following command to check the version of the cloud assistant client.

    ``` {#codeblock_8s6_kwt_1ql}
    aliyun-service -v
    ```

    **Note:** Cloud assistant clients later than V1.0.1.308 no longer use agentwatch to manage cloud assistant client services. You need to determine how to stop or start the cloud assistant client based on the returned version number of the cloud assistant client.

3.  Based on the version of your cloud assistant client, choose one of the following methods:
    -   For cloud assistant clients V1.0.1.308 and earlier, run the corresponding commands based on the init system of the ECS instance.
        -   Operating systems such as Debian, CentOS, and Red Hat:

            ``` {#codeblock_485_gd4_kku}
            # Stop the cloud assistant client.
            systemctl stop agentwatch
            # Start the cloud assistant client.
            systemctl start agentwatch
            ```

        -   Operating systems using other init systems:

            ``` {#codeblock_i8q_5pp_ov8}
            # Stop the cloud assistant client.
            chkconfig agentwatch off
            # Start the cloud assistant client.
            chkconfig agentwatch on
            ```

    -   For cloud assistant clients later than V1.0.1.308, run the corresponding commands based on the init system of the ECS instance.
        -   For Linux systems with new versions of the Linux kernel that typically use the systemd initialization process, perform the following operations:

            ``` {#codeblock_rov_4xt_5hx}
            # Check whether your ECS instance uses the systemd initialization process. If a message is returned, it indicates that systemd is used.
            strings /sbin/init | grep "/lib/system"
            # Stop the cloud assistant client.
            systemctl stop aliyun.service
            # Start the cloud assistant client.
            systemctl start aliyun.service
            ```

        -   For Linux systems with Ubuntu 14 or earlier versions that use the UpStart initialization process, perform the following operations:

            ``` {#codeblock_r9l_pfg_adz}
            # Check whether your ECS instance uses the UpStart initialization process. If a message is returned, it indicates that systemd is used.
            strings /sbin/init | grep "upstart"
            # Stop the cloud assistant client.
            /sbin/initctl stop aliyun-service
            # Start the cloud assistant client.
            /sbin/initctl start aliyun-service
            ```

        -   For Linux systems with earlier versions of the Linux kernel that use the sysvinit initialization process, perform the following operations:

            ``` {#codeblock_mg0_et7_syw .lanuage-shell}
            # Check whether your ECS instance uses the sysvinit initialization process. If a message is returned, it indicates that sysvinit is used.
            strings /sbin/init | grep "sysvinit"
            # Stop the cloud assistant client.
            /etc/init.d/aliyun-service stop
            # Start the cloud assistant client.
            /etc/init.d/aliyun-service start
            ```


## Related topics {#section_aj4_32x_ydb .section}

-   To explore the open source stack of the cloud assistant client, visit [GitHub aliyun\_assist\_client](https://github.com/aliyun/aliyun_assist_client).
-   [Cloud assistant overview](reseller.en-US/Deployment & Maintenance/Cloud assistant/Cloud assistant overview.md#)
-   [InvokeCommand](../reseller.en-US/API Reference/Cloud assistant/InvokeCommand.md#)
-   [Use the cloud assistant for automatic O&M](../reseller.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant for automatic O&M.md#)

