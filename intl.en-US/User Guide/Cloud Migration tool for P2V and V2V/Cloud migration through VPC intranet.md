# Cloud migration through VPC intranet {#ExpressConnectMigration .concept}

If you can directly access a VPC in an Alibaba Cloud region from your Integrated Data Center \(IDC\), virtual machines, or cloud hosts, we recommend that you set up the cloud migration by connecting the source servers with the VPC intranet. Compared to cloud migration through public networks, cloud migration through VPC intranet makes data transmission faster and more stable, which improves the efficiency of cloud migration.

## Prerequisites {#section_cww_qz1_kfb .section}

Cloud migration through VPC intranet requires you to be able to access the target VPC from the IDC, virtual machines, or cloud hosts. You can choose either two methods for achieving this: Use the [physical connection](https://partners-intl.aliyun.com/help/doc-detail/54210.html) feature of the Express Connect service. Alternatively, [build VPN gateways](https://partners-intl.aliyun.com/help/doc-detail/54211.html) in the target VPC.

**Note:** Express Connect and VPN Gateway are charged services. For more information, see Express Connect billing method and VPN Gateway billing method.

## Client\_data description {#section_eww_qz1_kfb .section}

You are required to edit the client\_data file on your own for cloud migration through VPC intranet. You can edit the client\_data file to meet your needs for cloud migration through VPC intranet. The client\_data file contains the following data for the cloud migration process:

-   The attributes of the intermediate instance for cloud migration, such as instance ID, instance name, Internet bandwidth, and IP addresses.
-   The process information of data disk migration.
-   The generated custom image name.
-   The region you plan to migrate to, and the network type of the intermediate instance.
-   The VPC, VSwitch, and security group used by the intermediate instance.

    For more information about the client\_data, see the relevant JSON file after the Cloud Migration tool is downloaded.


**Warning:** Do not modify the client\_data configuration file unless you want to migrate to Alibaba Cloud through VPC intranet. Otherwise, the modification may affect cloud migration and running processes.

After the [Cloud Migration tool is downloaded](http://p2v-tools.oss-cn-hangzhou.aliyuncs.com/Alibaba_Cloud_Migration_Tool.zip?spm=a2c4g.11186623.2.8.6B6W0i&file=Alibaba_Cloud_Migration_Tool.zip), open the client\_data file. The following parameters are involved in the cloud migration through VPC intranet:

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|net\_mode|Integer|No|Sets data transmission mode. Optional values:-   0 \(default\): Data is transmitted through the public network. The source server must be able to access the public network.
-   1: Data is transmitted through the VPC intranet. The source server must be able to access the target VPC.
-   2: Data is transmitted through the VPC intranet. The source server must be able to access both the public network and target VPC.

For cloud migration through VPC intranet, `net_mode` needs to be set 1 or 2.|
|vpc|Array|No|Specifies the ID of the VPC that has the Express Connect service or VPN Gateway configured. The parameter is required when net\_mode is set to `1` or `2`. A JSON array is composed of three string parameters: `vpc_id` \(required\), `vpc_name` \(optional\), and `description` \(optional\), which refer to VPC ID, VPC name, and VPC description respectively.|
|vswitch|Array|No|Specifies the ID of the VSwitch in the VPC. The parameter is required when net\_mode is set to `1` or `2`. A JSON array is composed of three String parameters: `vswitch_id` \(required\), `vpc_name` \(optional\), and `description` \(optional\), which refer to VSwitch ID, VSwitch name, and VSwitch description respectively.|
|securegroupid|String|No|Specifies the ID of the security group within the VPC.|

## Access VPC from the source server {#section_nww_qz1_kfb .section}

The following steps are applicable when net\_mode is set to `1`. The cloud migration is divided into three stages. `Stage 1` and `Stage 3` are completed on a backup server. The backup server must be able to access the public network. Data transmission at `Stage 2` is completed on the source server to be migrated.

1.  Log on to the backup server that can access the public network.

2.  Edit the client\_data file of the Cloud Migration tool. Set net\_mode to `1`, set `vpc_id` to the ID of the VPC that has configured the Express Connect service or the VPN Gateway, and set `vswitch_id` and `zone_id` parameters.

3.  \(Optional\) Configure the parameter `security_group_id` in the client\_data file, however, you must permit inbound traffic through proxy ports 8080 and 8703 of the security group. For more information, see [add Security Group Rules](../reseller.en-US/User Guide/Security groups/Add security group rules.md#).

4.  Run the Cloud Migration tool on the backup server by following [the steps of cloud migration through public network](reseller.en-US/Best Practices/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#) until you receive the notice `Stage 1 Is Done!`.

    [![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733783688/Stage1.png)](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733783688/Stage1.png)

5.  Log on to the source server. Copy the user\_config.json, rsync, and client\_data configuration files of the Cloud Migration tool from the backup server to the source server, while keeping the contents unchanged.

6.  Run the Cloud Migration tool on the backup server by following [the steps of cloud migration through public network](reseller.en-US/Best Practices/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#) until you receive the notice `Stage 2 Is Done!`.

    [![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733805431/Stage2.png)](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733805431/Stage2.png)

7.  Log on to backup server. Copy the user\_config.json, rsync, and client\_data configuration files of the Cloud Migration tool from the source server to the backup server, while keeping the contents unchanged.

8.  Run the Cloud Migration tool on the backup server again by following [the steps of cloud migration through public network](reseller.en-US/Best Practices/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#) until you receive the notice `Stage 3 Is Done!`, which means the cloud migration through VPC intranet has been completed.

    [![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733837163/Stage3.png)](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733837163/Stage3.png)


## Access the public network and VPC from the source server {#section_www_qz1_kfb .section}

The following steps are applicable when `net_mode = 2` and the steps are the same as cloud migration through the public network \(when `net_mode = 0`\). When `net_mode = 2`, data is automatically migrated to Alibaba Cloud through VPC and the rest of the process is completed through the public network. The transmission speed is slightly slower compared to the method of cloud migration through VPC intranet \(when `net_mode = 1`\).

1.  Log on to the source server that can access the public network and run the Cloud Migration tool following [the steps of cloud migration through public network](reseller.en-US/Best Practices/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#).

2.  Edit the client\_data file of the Cloud Migration tool. Set net\_mode to `2`, set `vpc_id` as the ID of the VPC that has configured the Express Connect service or the VPN Gateway, and set `vswitch_id` and `zone_id` parameters.

3.  \(Optional\) Configure the parameter `security_group_id` in the client\_data file, however, you must permit inbound traffic through proxy ports 8080 and 8703 of the security group. For more information, see [add Security Group Rules](../reseller.en-US/User Guide/Security groups/Add security group rules.md#).

4.  Run the Cloud Migration tool following [the steps of cloud migration through public network](reseller.en-US/Best Practices/Cloud Migration tool for P2V and V2V/Migrate to Alibaba Cloud by using Cloud Migration tool.md#).


## FAQ {#section_zww_qz1_kfb .section}

If the cloud migration process is interrupted, you can check the [Cloud Migration tool troubleshooting](reseller.en-US/Best Practices/Cloud Migration tool for P2V and V2V/Cloud Migration tool FAQ.md#). Alternatively, you can [join the DingTalk customer feedback group](https://h5.dingtalk.com/invite-page/index.html?spm=a2c4g.11186623.2.31.FEg99s&code=ca190154ff) for the Cloud Migration tool to contact ECS cloud migration technical support.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9833/154088286413339_en-US.png)

