# Migrate to the cloud through Alibaba Cloud VPC {#ExpressConnectMigration .concept}

This topic describes how to connect source servers to Alibaba Cloud VPC to achieve seamless migration of your services to the cloud.

## Prerequisites {#section_cww_qz1_kfb .section}

Access to the target source servers is established by using either the [physical connection](https://www.alibabacloud.com/help/doc-detail/54210.html) feature of Express Connect, or [VPN gateways](https://www.alibabacloud.com/help/doc-detail/54211.html) that correspond to the target VPC.

**Note:** Fees are incurred for the usage of Express Connect and VPN Gateway. For more information, see [Billing of physical connections](../../../../intl.en-US/Pricing/Billing of physical connections.md#) and [VPN Gateway billing method](../../SP_74/DNVPN11883127/EN-US_TP_13496.dita#concept_iyc_hwx_wdb).

## Client\_data description {#section_eww_qz1_kfb .section}

**Warning:** Only modify the client\_data configuration file if you want to migrate services by using Alibaba Cloud VPC. Do not modify the file otherwise, because any modification may affect normal cloud migration and running processes.

If you want to migrate to the cloud by using Alibaba Cloud VPC, you must modify the values of parameters that correspond to the following items in the client\_data file:

-   The source system: System platform architecture.
-   VPC: VPC ID, VSwitch ID, and security group ID.
-   The intermediate instance: Instance ID, instance type, IP address, and intermediate disk.
-   The target image: Target image ID.
-   Migration tool configuration: Data transfer parameter configuration, network configuration, and API service configuration.

The following table details the specific parameters in the client\_data file that you need to configure to achieve migration to the cloud through Alibaba Cloud VPC.

|Name|Type|Required?|Description|
|:---|:---|:--------|:----------|
|extra.net.net\_mode|Integer|No|Sets data transmission mode. Valid values: -   0 \(default\): Data is transmitted through the Internet. The source server must be able to access the Internet.
-   1: Data is transmitted through Alibaba Cloud VPC. The source server must be able to access the target VPC.
-   2: Data is transmitted through Alibaba Cloud VPC. The source server must be able to access both the Internet and target VPC.

 To achieve cloud migration through VPC, you must set `net_mode` to 1 or 2.|
|transition.vpc.vpc\_id|String|No|Specifies the ID of the VPC that is configured with the Express Connect service or VPN Gateway service. The parameter is required in the case of `net_mode=1` or `net_mode=2`.|
|transition.vswitch.vswitch\_id|String|No|Specifies the ID of the VSwitch in the specified VPC. The parameter is required in the case of `net_mode=1` or `net_mode=2`.|
|transition.security\_group.security\_group\_id|String|No|Specifies the ID of the security group within the VPC.|
|extra.net.proxy.ip\_port|String|No|Specifies the IP address and port of the proxy service, in the format of IP:Port \(for example "10.0.0.100:1080"\).|
|extra.net.proxy.user\_pwd|String|No|Specifies the username and password of the proxy service, in the format of User:Password \(for example "admin:123456"\).|

For more information, [download the migration tool](http://p2v-tools.oss-cn-hangzhou.aliyuncs.com/Alibaba_Cloud_Migration_Tool.zip?spm=a2c4g.11186623.2.8.6B6W0i&file=Alibaba_Cloud_Migration_Tool.zip) to view the client\_data file.

## Procedure for migrating the source server that cannot access the Internet {#section_nww_qz1_kfb .section}

The following procedure is applicable when `net_mode=1`. The cloud migration is divided into three stages. `Stage 1` and `Stage 3` are completed on a backup server that must be able to access the Internet, whereas data transmission at `Stage 2` is completed on the source server.

1.  Log on to the backup server and complete the following steps:

    1.  Download and install the Cloud Migration tool. For more information, see [Migrate your server to Alibaba Cloud by using the Cloud Migration tool](intl.en-US/Migration Service/Cloud Migration tool for P2V and V2V/Migrate your server to Alibaba Cloud by using the Cloud Migration tool.md#section_twq_sxz_jfb).

    2.  Edit the client\_data file of the Cloud Migration tool. Specifically, set `net_mode=1`, set `vpc_id` to the ID of the VPC that is configured with the Express Connect service or the VPN Gateway, and set the `vswitch_id` parameter.

    3.  \(Optional\) Configure the parameter `security_group_id` in the client\_data file. Note that the security group must be configured with a rule that permits inbound traffic through ports 8080 and 8703. For more information, see [Add security group rules](../../../../intl.en-US/Security/Security groups/Add security group rules.md#).

    4.  Run the Cloud Migration tool on the backup server as described in [Migrate your server to Alibaba Cloud by using the Cloud Migration tool](intl.en-US/Migration Service/Cloud Migration tool for P2V and V2V/Migrate your server to Alibaba Cloud by using the Cloud Migration tool.md#) until the notification `Stage 1 Is Done!` is displayed.

        [![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733783688/Stage1.png)](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733783688/Stage1.png)

2.  Log on to the source server and complete the following steps:

    1.  Copy the user\_config.json, Rsync, and client\_data configuration files of the Cloud Migration tool from the backup server to the source server.

    2.  Run the Cloud Migration tool on the source server as described in [Migrate your server to Alibaba Cloud by using the Cloud Migration tool](intl.en-US/Migration Service/Cloud Migration tool for P2V and V2V/Migrate your server to Alibaba Cloud by using the Cloud Migration tool.md#) until the notification `Stage 2 Is Done!` is displayed.

        [![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733805431/Stage2.png)](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733805431/Stage2.png)

3.  Log on to the backup server and complete the following steps:

    1.  Copy the user\_config.json, rsync, and client\_data configuration files of the Cloud Migration tool from the source server to the backup server.

    2.  Run the Cloud Migration tool on the source server as described in [Migrate your server to Alibaba Cloud by using the Cloud Migration tool](intl.en-US/Migration Service/Cloud Migration tool for P2V and V2V/Migrate your server to Alibaba Cloud by using the Cloud Migration tool.md#) until the notification `Stage 3 Is Done!` is displayed.

        [![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733837163/Stage3.png)](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733837163/Stage3.png)


## Procedure for migrating a source server that can access the Internet {#section_www_qz1_kfb .section}

The following procedure is applicable when `net_mode=2` and the steps are the same as cloud migration through the Internet \(when `net_mode=0`\). When `net_mode=2`, data is automatically migrated to Alibaba Cloud through VPC and the rest of the process is completed through the Internet.

1.  Log on to the source server.

2.  Download and install the Cloud Migration tool. For more information, see [Migrate your server to Alibaba Cloud by using the Cloud Migration tool](intl.en-US/Migration Service/Cloud Migration tool for P2V and V2V/Migrate your server to Alibaba Cloud by using the Cloud Migration tool.md#section_twq_sxz_jfb).

3.  Edit the client\_data file of the Cloud Migration tool. Specifically, set `net_mode=2`, set `vpc_id` to the ID of the VPC that is configured with the Express Connect service or the VPN Gateway, and set the `vswitch_id` parameter.

4.  \(Optional\) Configure the parameter `security_group_id` in the client\_data file. However, you must permit inbound traffic through proxy ports 8080 and 8703 in the security group. For more information, see [Add security group rules](../../../../intl.en-US/Security/Security groups/Add security group rules.md#).

5.  Run the Cloud Migration tool as described in [Migrate your server to Alibaba Cloud by using the Cloud Migration tool](intl.en-US/Migration Service/Cloud Migration tool for P2V and V2V/Migrate your server to Alibaba Cloud by using the Cloud Migration tool.md#).


## Procedure for migrating a source server that can access the proxy {#section_c1f_ah3_mrn .section}

The following procedure is applicable when `net_mode=2` and the steps are the same as cloud migration through the Internet \(when `net_mode=0`\). When `net_mode=2`, data is automatically migrated to Alibaba Cloud through VPC and the rest of the process is completed by accessing the Internet through the LAN proxy.

1.  Log on to the source server.

2.  Download and install the Cloud Migration tool. For more information, see [Migrate your server to Alibaba Cloud by using the Cloud Migration tool](intl.en-US/Migration Service/Cloud Migration tool for P2V and V2V/Migrate your server to Alibaba Cloud by using the Cloud Migration tool.md#section_twq_sxz_jfb).

3.  Edit the client\_data file of the Cloud Migration tool as follows:

    1.  Set `net_mode=2`, set `vpc_id` to the ID of the VPC that has configured the Express Connect service or the VPN Gateway, and set `vswitch_id`.

    2.  Configure the network proxy service. Prepare the network proxy server in the LAN of the source server and fill in the following configuration information:

        1.  Enter the IP address and port of the network proxy server in `extra.net.proxy.ip_port`.
        2.  Enter the username and password \(if they are configured\) in `extra.net.proxy.user_pwd`.
        **Note:** For more information about `extra.net.proxy.ip_port` and `extra.net.proxy.user_pwd`, see the above table.

4.  \(Optional\) Configure the parameter `security_group_id` in the client\_data file. However, you must permit inbound traffic through proxy ports 8080 and 8703 in the security group. For more information, see [Add security group rules](../../../../intl.en-US/Security/Security groups/Add security group rules.md#).

5.  Run the Cloud Migration tool as described in [Migrate your server to Alibaba Cloud by using the Cloud Migration tool](intl.en-US/Migration Service/Cloud Migration tool for P2V and V2V/Migrate your server to Alibaba Cloud by using the Cloud Migration tool.md#).


## Troubleshooting {#section_dgl_spy_whb .section}

If you experience an issue during the cloud migration, we recommend that you check the [Cloud Migration tool FAQ](intl.en-US/Migration Service/Cloud Migration tool for P2V and V2V/Cloud Migration tool FAQ.md#) for common troubleshooting issues, or [join the Cloud Migration tool DingTalk group](https://h5.dingtalk.com/invite-page/index.html?spm=a2c4g.11186623.2.31.FEg99s&code=ca190154ff) for technical support.

