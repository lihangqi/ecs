# API FAQ {#concept_761256 .concept}

-   [What is ECS API?](#section_2mf_wov_wfu)
-   [Error code InvalidDataDiskCategory.NotSupported is returned when I try to create an ECS instance. What can I do?](#section_rqe_51b_fkf)
-   [How can I create an ECS instance that is assigned a public IP address?](#section_iop_1gx_4ub)
-   [I have created an ECS instance by using an ECS API operation. Why can't the public IP address of the instance be pinged?](#section_2pr_bjo_kqj)
-   [The error message "The specified IP is already in use." is returned when I use an ECS API operation to bind a public IP address to my instance. What can I do?](#section_qxl_ubh_cso)
-   [When I modify the public bandwidth configurations of my instance by using an ECS API operation, can I specify an effective period of time for the new bandwidth configurations?](#section_opz_hdk_3ab)
-   [Why can't all the security group rules in a security group be displayed when I use an ECS API operation or ECS SDK to query the details of the security group?](#section_0gg_gvb_36g)
-   [Why does a query made by using the ECS API, ECS SDK, or Alibaba Cloud CLI return only ten entries?](#section_vto_62a_f45)

## What is ECS API? {#section_2mf_wov_wfu .section}

ECS API is an open-source remote procedure call \(RPC\) API that provides API services to Alibaba Cloud users. You can use this API to manage and use ECS instances. The following figure shows the path along which a request is forwarded to call an API. For more information about how to use the ECS API, see [Quick start for ECS APIs](reseller.en-US/API Reference/Quick start for ECS APIs.md#).

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/614896/156695916649776_en-US.png)

## Error code InvalidDataDiskCategory.NotSupported is returned when I try to create an ECS instance. What can I do? {#section_rqe_51b_fkf .section}

-   Problem description: After you call the [EN-US\_TP\_9856.md\#](reseller.en-US/API Reference/Instances/RunInstances.md#) operation to create an ECS instance, the following error information is returned:

    ``` {#codeblock_dgs_3nb_dh9}
    {
        "Code": "InvalidDataDiskCategory.NotSupported",
        "Message": "Specified disk category is not supported."
    }
    ```

-   Cause: The error occurred because disks of the specified category cannot be created in the specified zone.
-   Solution: We recommend that you call the [DescribeAvailableResource](reseller.en-US/API Reference/Regions/DescribeAvailableResource.md#) operation to view the resources available in the zone where you want to create the ECS instance and ensure that there are sufficient resources in that zone. You can also change the value of ZoneId and try again.

    ``` {#codeblock_70q_r18_4zf}
    aliyun ecs RunInstances --ImageId win2008_64_ent_r2_cn_40G_alibase_20150429.vhd --InstanceType ecs.g5.large --SecurityGroupId <TheSecuriytyGroupId> --SystemDiskCategory cloud_efficiency --ZoneId cn-hangzhou-c
    ```


## How can I create an ECS instance that is assigned a public IP address? {#section_iop_1gx_4ub .section}

-   Method 1: Call the [EN-US\_TP\_9856.md\#](reseller.en-US/API Reference/Instances/RunInstances.md#) operation with InternetMaxBandwidthOut set to a value greater than 0 to create an ECS instance. The new ECS instance is automatically assigned a public IP address.
-   Method 2: Call the [EN-US\_TP\_9857.md\#](reseller.en-US/API Reference/Instances/CreateInstance.md#) operation to create an ECS instance. Then call the [EN-US\_TP\_9931.md\#](reseller.en-US/API Reference/Networks/AllocatePublicIpAddress.md#) operation to assign a public IP address to the instance.

## I have created an ECS instance by using an ECS API operation. Why can't the public IP address of the instance be pinged? {#section_2pr_bjo_kqj .section}

-   Problem description: The new ECS instance that you created by using an ECS API operation cannot connect to the public network, and the public IP address of the instance cannot be pinged.
-   Cause: You have not added a security group rule to allow the public network to access the instance.
-   Solution: Call the [EN-US\_TP\_9917.md\#](reseller.en-US/API Reference/Security groups/AuthorizeSecurityGroup.md#) operation to add an inbound rule to the security group to which the instance belongs to allow the public network to access the instance. For example, you can send the following request where IpProtocol is set to ICMP to call the AuthorizeSecurityGroup operation and add an inbound rule that allows the public IP address of this instance to be pinged from any other IP addresses:

    ``` {#codeblock_x29_ll1_ix9}
    https://ecs.aliyuncs.com/?Action=AuthorizeSecurityGroup
    &SecurityGroupId=sg-bp15ed6xe1yxeycg7***
    &SourceCidrIp=0.0.0.0/0
    &IpProtocol=ICMP
    &PortRange=-1/-1
    &<Common request parameters>
    ```


## The error message "The specified IP is already in use." is returned when I use an ECS API operation to bind a public IP address to my instance. What can I do? {#section_qxl_ubh_cso .section}

-   Problem description: When you call the [EN-US\_TP\_9931.md\#](reseller.en-US/API Reference/Networks/AllocatePublicIpAddress.md#) operation to assign the public IP address specified by IpAddress to your ECS instance, the following error information is returned:

    ``` {#codeblock_kep_mrx_ifa}
    {
        "Code": "IpInUse",
        "Message": "The specified IP is already in use."
    }
    ```

-   Cause: The specified IP address is already in use.
-   Solution: Check whether the IP address is already in use. If yes, try another IP address.

## When I modify the public bandwidth configurations of my instance by using an ECS API operation, can I specify an effective period of time for the new bandwidth configurations? {#section_opz_hdk_3ab .section}

You can call the [EN-US\_TP\_9937.md\#](reseller.en-US/API Reference/Networks/ModifyInstanceNetworkSpec.md#) operation to modify the public bandwidth configurations of your ECS instance. The new bandwidth configurations take effect on the instance immediately after the modification is completed. If you only want to temporarily modify the bandwidth configurations of your instance, set StartTime and EndTime to define an effective period of time.

If you are using an Elastic IP Address, you can call the [ModifyEipAddressAttribute](../../../../reseller.en-US/API reference/EIP/ModifyEipAddressAttribute.md#) operation to make the modification but you cannot specify an effective period of time.

## Why can't all the security group rules in a security group be displayed when I use an ECS API operation or ECS SDK to query the details of the security group? {#section_0gg_gvb_36g .section}

Security group rules can be distinguished by their NIC types, public NIC \(internet\) and internal NIC \(intranet\). When you call the [DescribeSecurityGroupAttribute](reseller.en-US/API Reference/Security groups/DescribeSecurityGroupAttribute.md#) operation to query the details of a security group, the NIC parameter is not required. However, if this parameter is not specified, the default value internet is used. Therefore, when you run the following CLI command to call the DescribeSecurityGroupAttribute operation, only the public security group rules, not all security group rules, in the queried security group are displayed:

``` {#codeblock_tpl_qvr_rxl}
aliyun ecs DescribeSecurityGroupAttribute --SecurityGroupId <TheSecurityGroupId> --RegionId <TheRegionId>
```

If you want to view the internal security group rules in a security group \(such as internal security group rules that allow access across internal networks or that are configured for the VPN firewall of Finance Cloud\), run the following command with NicType set to intranet:

``` {#codeblock_na2_bjq_8yl}
aliyun ecs DescribeSecurityGroupAttribute --SecurityGroupId <TheSecurityGroupId> --RegionId <TheRegionId> --NicType intranet
```

## Why does a query made by using the ECS API, ECS SDK, or Alibaba Cloud CLI return only ten entries? {#section_vto_62a_f45 .section}

For details, see [Why only ten entries are returned for query request by using APIs or SDK](reseller.en-US/API Reference/Appendix/Why only ten entries are returned for query request by using APIs or SDK.md#).

