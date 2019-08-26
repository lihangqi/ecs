# Attach Elastic Network Interfaces {#task_wng_dlc_ggb .task}

In this topic, you will attach secondary network interfaces to the bare-metal servers.

You must have created a specified quantity of ENIs in the ECS console. In this topic, nine ENIs should be created and secured by the VSwitches that you launched in the [Prepare network](intl.en-US/Hide/Build VMC on Alibaba Cloud bare-metal server/Preparation/Prepare network.md#) topic.

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/?spm=a2c4g.11186623.2.9.FNEORG#/home).
2.  In the left-side navigation pane, select **Networks and Security** \> **ENI**.
3.  Select a region.

    **Note:** The region must be identical to where the bare-metal servers belong.

4.  Click **Create ENI**.
5.  Refer to the document [Create an ENI](../../../../../intl.en-US/User Guide/Elastic Network Interfaces/Create an ENI.md#) for configuration details. To keep the configuration consistent in this tutorial, particular configurations are specified as follows:

    |Attribute|Setting|
    |:--------|:------|
    |VPC|The VPC "vmware-on-xdragon" you created in the [Prepare network](intl.en-US/Hide/Build VMC on Alibaba Cloud bare-metal server/Preparation/Prepare network.md#) topic.|
    |VSwitch|The VSwitch you created in the [Prepare network](intl.en-US/Hide/Build VMC on Alibaba Cloud bare-metal server/Preparation/Prepare network.md#) topic.**Note:** For more information about the number of ENIs and the name of VSwitches, see the following [Background information](intl.en-US/Hide/Build VMC on Alibaba Cloud bare-metal server/Preparation/Attach Elastic Network Interfaces.md#context_mbn_szx_ggb).

|
    |Security Group|The security group you selected during the [Prepare network](intl.en-US/Hide/Build VMC on Alibaba Cloud bare-metal server/Preparation/Prepare network.md#) topic.|

    After you complete the operation, 9 ENIs are created with the following **ID/Name**. And they are all controlled by the same VPC \(**vmware-on-xdragon**\).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83055/154705615335504_en-US.png)


The following table describe how the ENIs are used:

|Name of the VSwitch|Purpose|How many created in this topic|ENI requirement in total|Assigned network segment|
|:------------------|:------|:-----------------------------|:-----------------------|:-----------------------|
|management| -   Working as the passthrough network interface for the three NSX components.
-   Three primary ENIs has been created in the [Create bare-metal servers and ECS instance](intl.en-US/Hide/Build VMC on Alibaba Cloud bare-metal server/Preparation/Create bare-metal servers and ECS instance.md#) topic.

 |3|6|192.168.10.0/24|
|Vtep|Two ENIs for every ESXi host, and one ENI for the NSX-edge component. It controls the east-west traffic flows of the VMC VM.|3|3|192.168.40.0/24|
|Vmotion|Two ENIs for every ESXi host. It provides live migration capability for the VMC VM.|2|2|192.168.20.0/24|
|EXT|One for the NSX-edge component. It controls the south-north traffic flow for the VMC VM.|1|1|192.168.50.0/24|

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/?spm=a2c4g.11186623.2.9.FNEORG#/home). 
2.  In the left-side navigation pane, select **Networks and Security** \> **ENI**. 
3.  Locate the previously created ENI, in the **Action** column, click **Bind to Instance**. 
4.  At the **Select Instance** entry, choose the ESXi host, and click **OK**. 

    The following table lists how the nine network interfaces are allocated:

    |ESXi host|VSwitch name in this tutorial|ENI quantity|
    |:--------|:----------------------------|:-----------|
    |Network node and compute node \(vmc\_management\)|management|3|
    |vtep|2|
    |vmotion|1|
    |ext|1|
    |Compute node \(esxi-nsx-vm1\)|vtep|1|
    |vmotion|1|


To assign private IP addresses for the EXT ENI, follows these steps:

1.  Navigate to the [Alibaba Cloud API Explorer DescribeRegions](https://api.aliyun.com/#product=Ecs&api=DescribeRegions) page. Click **Submit Request** to retrieve the region ID of the ENIs from the responded Alibaba Cloud region ID list.
2.  Assign nine private IP addresses for the EXT ENI:

    1.  Open the [AssignPrivateIpAddresses](https://api.aliyun.com/#product=Ecs&api=AssignPrivateIpAddresses) page.
    2.  Specify the RegionId with cn-shanghai, and NetworkPrivateAddress with the actual ID of the EXT ENI.
    3.  Submit the request.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83055/154705615335507_en-US.png)

3.  Record the IP address list of the EXT ENI:
    1.  Open the [DescribeNetworkInterfaces](https://api.aliyun.com/#product=Ecs&api=DescribeNetworkInterfaces) page.
    2.  Specify the RegionId with cn-shanghai, and NetworkPrivateAddress with the actual ID of the EXT ENI.
4.  Submit the request.
5.  Copy the response body and keep it for further use.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83055/154705615335508_en-US.png)


The next topic is [Install VMware vCenter Server](intl.en-US/Hide/Build VMC on Alibaba Cloud bare-metal server/Installation Guide/Install VMware vCenter Server.md#).

