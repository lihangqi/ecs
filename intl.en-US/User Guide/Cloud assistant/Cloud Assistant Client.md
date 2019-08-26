# Cloud Assistant Client {#concept_wtg_32x_ydb .concept}

The cloud assistant client is an agent facilitating cloud assistant command invocation on ECS instances. The cloud assistant client does not perform any operations. You can start all the operations and within your controllable range. Instances that are created later than Dec 1, 2017 are pre-installed with the cloud assistant client by default. If your ECS instance was created earlier than Dec 1, 2017, and you want to use cloud assistant service, you can install the cloud assistant client by yourself. This topic illustrates how to install, update, and disable the cloud assistant client in an instance.

## Install cloud assistant client {#section_e5n_k2x_ydb .section}

**Windows instance**

1.  [Connect to a Windows instance](reseller.en-US/User Guide/Connect to instances/Connect to a Windows instance.md#).
2.  [Download](https://repo-aliyun-assist.oss-cn-beijing.aliyuncs.com/download/aliyun_agent_setup.exe) the cloud assistant client.
3.  Double-click the client file and follow the instructions to install the client.

**Linux instance**

Based on the distribution of Linux, to install cloud assistant client, select the most appropriate approach from the following.

-   Install the RPM package:

    1.  [Connect to a Linux instance by using a password](reseller.en-US/User Guide/Connect to instances/Connect to a Linux instance by using a password.md#).
    2.  Run `wget https://repo-aliyun-assist.oss-cn-beijing.aliyuncs.com/download/aliyun_assist.rpm` to download the RPM package of the cloud assistant client.
    3.  Run `rpm -ivh aliyun_assist.rpm`  to install the cloud assistant client.
-   Install the DEB package:

    1.  Connect to your Linux instance.
    2.  Run `wget https://repo-aliyun-assist.oss-cn-beijing.aliyuncs.com/download/aliyun_assist.deb` to download the DEB package of the cloud assistant client.
    3.  Run `dpkg -i aliyun_assist.deb` to install the cloud assistant client.
-   Install with the compilation file of source code:

    1.  Connect to your Linux instance.
    2.  Run `git clone https://github.com/aliyun/aliyun_assist_client` to download the cloud assistant client source code.
    3.  Enter the source code directory.
    4.  Run `cmake .` to generate the compilation file.
    5.  Run `make` to start compilation.
    6.  Run `cmake_install.sh`  to install the cloud assistant client.

## Update the cloud assistant client {#section_r34_32x_ydb .section}

The update process of cloud assistant client runs every 1 hour to query update resources for the client. The update process is located at the directory of:

-   Windows instance: C:\\ProgramData\\aliyun\\assist\\$\{version\}/aliyun\_assist\_update

-   Linux instance: /usr/local/share/aliyun-assist/$\{version\}/aliyun\_assist\_update


Generally, the update process is one of the startup items in the instance. However, you can disable the update process:

-   Windows instance: Run `rename aliyun_assist_update` in CMD or PowerShell.

-   Linux instance: Run `chmod a-x aliyun_assist_update`.


## Disable the cloud assistant client {#section_rlc_n2x_ydb .section}

**Note:** The cloud assistant client is managed by the *Aliyun* service. Once you disable the client, *Aliyun* service is also disabled and stopping the instance in the ECS console may fail. We recommend that you perform with caution to disable the client.

**Windows instance**

1.  [Connect to a Windows instance](reseller.en-US/User Guide/Connect to instances/Connect to a Windows instance.md#).
2.  Select **Computer Management** \> **Services and Applications** \> **Services****AliyunService**
3.  Click **Stop the service**.

    ![](images/5250_en-US_source.png)


**Linux instance**

1.  [Connect to a Linux instance by using a password](reseller.en-US/User Guide/Connect to instances/Connect to a Linux instance by using a password.md#).
2.  Run the following commands to disable the cloud assistant client service.

    ```
    
    systemctl stop agentwatch
    chkconfig agentwatch off
    ```


## References {#section_aj4_32x_ydb .section}

Visit the [GitHub aliyun\_assist\_client](https://github.com/aliyun/aliyun_assist_client) to explore the open source stack of cloud assistant.

You can use the cloud assistant client for the following:

-   [Cloud assistant](reseller.en-US/Product Introduction/Cloud assistant.md#)
-   [InvokeCommand](../../../../reseller.en-US/API Reference/Cloud assistant/InvokeCommand.md#)
-   [Automatically manage instances](../../../../reseller.en-US/Best Practices/Monitor/Automatically manage instances.md#)

