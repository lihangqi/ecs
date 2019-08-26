# ENI overview {#concept_xzg_mgt_xdb .concept}

An Elastic Network Interface \(ENI\) is a virtual network interface that can be attached to an ECS instance in a VPC. You can use an ENI to deploy a high-availability cluster, and perform low-cost failover and fine-grained network management in all Alibaba Cloud regions.

## Scenarios {#section_ac1_qnw_ydb .section}

ENIs are suitable for:

-   **Deploying a high-availability cluster**

    An ENI is suitable for high-availability architecture for multiple network interfaces on a single instance.

-   **Providing a low-cost failover solution**

    You can detach an ENI from a failed ECS instance and then attach it to another ECS instance to quickly redirect traffic from the failed instance to a backup instance, thereby quickly restoring your services.

-   **Managing the network with refined controls**

    You can configure multiple ENIs for an instance in any Alibaba Cloud region. For example, you can use some ENIs for internal management and other ENIs for Internet business access, so as to isolate confidential data from business data. You can also configure specific security group rules for each ENI based on the source IP address, protocols, ports, and more to achieve secured traffic control.


## ENI types {#section_cc1_qnw_ydb .section}

ENIs are classified into two types:

-   **Primary ENI**

    The ENI created by default upon the creation of an instance in a VPC. The life cycle of the primary ENI is the same as that of the instance, and you cannot remove the primary ENI from the instance.

-   **Secondary ENI**

    You can create a secondary ENI and attach it to an instance or detach it from the instance. The maximum number of ENIs that you can attach to one instance varies with the instance type. For more information, see [Instance type families](../../../../reseller.en-US/Instances/Instance type families.md#).


## ENI attributes {#section_ec1_qnw_ydb .section}

The following table describes ENI attributes.

|Attribute|Quantity|
|:--------|:-------|
|Private IP address|Varies with instance types|
|MAC address|1|
|Security group|1 to 5|
|ENI name|1|

## Limits {#section_ic1_qnw_ydb .section}

ENIs have the following limits:

-   There is an upper limit on the number of ENIs that can be created for one account in each region. For more information, see [Limits on ENIs](../../../../reseller.en-US/Product Introduction/Limits.md#section_gfq_v2x_wdb).
-   The ECS instance and its attached secondary ENI must be in the same zone, region, and VSwitch, but can be in different security groups.
-   The number of secondary ENIs that can be attached to an ECS instance depends on the instance type. For more information, see [Instance type families](../../../../reseller.en-US/Instances/Instance type families.md#).
-   Only I/O-optimized instance types support ENIs.
-   ECS instances in a classic network do not support ENIs.
-   The instance bandwidth varies with the instance type. You cannot increase the bandwidth of an ECS instance by attaching multiple ENIs to the instance.

## Related operations {#section_kc1_qnw_ydb .section}

For images that cannot identify secondary ENIs, log on to the instance to [configure the ENI](../../../../reseller.en-US/Network/Elastic Network Interfaces/Configure an ENI.md#).

## Console operations {#section_lc1_qnw_ydb .section}

In the ECS console, you can view information of an attached ENI. You can also perform the following actions with a secondary ENI only \(a primary ENI is not supported\):

-   [Attach an ENI](reseller.en-US/Network/Elastic Network Interfaces/Attach an ENI.md#).
-   [Create an ENI](reseller.en-US/Network/Elastic Network Interfaces/Create an ENI.md#).
-   [Delete an ENI](../../../../reseller.en-US/Network/Elastic Network Interfaces/Delete an ENI.md#).
-   [Detach an ENI from an instance](reseller.en-US/Network/Elastic Network Interfaces/Detach an ENI from an instance.md#).
-   [Modify an ENI](reseller.en-US/Network/Elastic Network Interfaces/Modify an ENI.md#).

## API operations {#section_oc1_qnw_ydb .section}

You can call [DescribeNetworkInterfaces](../../../../reseller.en-US/API Reference/Elastic network interfaces/DescribeNetworkInterfaces.md#) to query an ENI list, and call [DescribeInstances](../../../../reseller.en-US/API Reference/Instances/DescribeInstances.md#) to query the information of a specific ENI attached to an instance. Additionally, you can call the following API actions as needed for a secondary ENI only \(a primary ENI is not supported\):

-   [CreateNetworkInterface](../../../../reseller.en-US/API Reference/Elastic network interfaces/CreateNetworkInterface.md#)
-   [DeleteNetworkInterface](../../../../reseller.en-US/API Reference/Elastic network interfaces/DeleteNetworkInterface.md#)
-   [AttachNetworkInterface](../../../../reseller.en-US/API Reference/Elastic network interfaces/AttachNetworkInterface.md#)
-   [DetachNetworkInterface](../../../../reseller.en-US/API Reference/Elastic network interfaces/DetachNetworkInterface.md#)
-   [ModifyNetworkInterfaceAttribute](../../../../reseller.en-US/API Reference/Elastic network interfaces/ModifyNetworkInterfaceAttribute.md#)

