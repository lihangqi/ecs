# Elastic network interfaces {#concept_xzg_mgt_xdb .concept}

An Elastic Network Interface \(ENI\) is a virtual network interface that can be attached to an ECS instance in a VPC. By using ENIs, you can build high-availability clusters, implement failover at a lower cost, and achieve refined network management. The ENI feature is available in all regions.

## Scenarios {#section_ac1_qnw_ydb .section}

ENIs can be used in the following scenarios:

-   **Deploying a high-availability cluster**

    An ENI can meet the demands of a high-availability architecture for multiple network interfaces on a single instance.

-   **Providing a low-cost failover solution**

    You can detach an ENI from a failed ECS instance and then attach it to another ECS instance to quickly redirect the failed instance’s traffic to a backup instance. This action recovers the service immediately.

-   **Managing the network with refined controls**

    You can configure multiple ENIs for an instance. For example, you can use some ENIs for internal management and other ENIs for Internet business access, so as to isolate managerial data from business data. You can also configure precisely-targeted security group rules for each ENI based on the source IP address, protocols, ports, and more to achieve secured traffic control.


## ENI types {#section_cc1_qnw_ydb .section}

ENIs are classified into two types:

-   **Primary ENI**

    The ENI created by default upon the creation of an instance in a VPC is called the primary ENI. The life cycle of the primary ENI is the same as that of the instance and you are not allowed to remove the primary ENI from the instance.

-   **Secondary ENI**

    You can create a secondary ENI and attach it to an instance or detach it from the instance. Multiple private IPs are supported for each secondary ENI. The maximum number of ENIs that you can attach to one instance varies with the instance type. For more information, see [Instance type families](reseller.en-US/Product Introduction/Instance type families.md#).


## ENI attributes {#section_ec1_qnw_ydb .section}

The following table displays ENI attributes.

|Attribute|Quantity|
|:--------|:-------|
|Primary private IP addresses|1|
|MAC address|1|
|Security group|Min. 1, and Max. 5|
|Description|1|
|ENI name|1|

## Limitations {#section_ic1_qnw_ydb .section}

ENIs have the following limitations:

-   By default, one account can own up to 100 ENIs in one region. The quota increases with the membership level. If you require a higher quota, open a ticket.

-   The ECS instance must be in the same zone of the same region as the ENI, but they do not have to be in the same VSwitch.

-   The number of ENIs that can be attached to an ECS instance is determined by the instance type. For more information, see [Instance type families](reseller.en-US/Product Introduction/Instance type families.md#).

-   Only I/O optimized instance types support ENIs.

-   Attaching multiple ENIs does not increase the instance bandwidth.

    **Note:** The instance bandwidth capability varies with the instance type.


## Related operations {#section_kc1_qnw_ydb .section}

For images that cannot identify ENIs, you can log on to the instance to [configure the ENI](../../../../reseller.en-US/User Guide/Elastic Network Interfaces/Configure an ENI.md#).

## Console operations {#section_lc1_qnw_ydb .section}

You can complete the following operations in the ECS console:

-   [Attach an ENI when creating an instance](../../../../reseller.en-US/User Guide/Elastic Network Interfaces/Attach an ENI when creating an instance.md#)
-   [Create an ENI](../../../../reseller.en-US/User Guide/Elastic Network Interfaces/Create an ENI.md#)
-   [Delete an ENI](../../../../reseller.en-US/User Guide/Elastic Network Interfaces/Delete an ENI.md#)
-   [Attach an ENI to an instance](../../../../reseller.en-US/User Guide/Elastic Network Interfaces/Attach an ENI to an instance.md#): The instance must be in a **Stopped** or **Running** status.
-   [Detach an ENI from an instance](../../../../reseller.en-US/User Guide/Elastic Network Interfaces/Detach an ENI from an instance.md#): The instance must be in a **Stopped** or **Running** status.
-   [Modify attributes of an ENI](../../../../reseller.en-US/User Guide/Elastic Network Interfaces/Modify attributes of an ENI.md#): You can modify attributes of an ENI, including its name, security group, and description.
-   When an ENI is attached to an instance, you can view the information of the ENI on the instance details page and the network interfaces page.

## API operations {#section_oc1_qnw_ydb .section}

You can complete the following operations by using APIs:

-   [Create an ENI](../../../../reseller.en-US/API Reference/Elastic network interfaces/CreateNetworkInterface.md#)
-   [Delete an ENI](../../../../reseller.en-US/API Reference/Elastic network interfaces/DeleteNetworkInterface.md#)
-   [Query ENI list](../../../../reseller.en-US/API Reference/Elastic network interfaces/DescribeNetworkInterfaces.md#)
-   [Attach an ENI to an instance](../../../../reseller.en-US/API Reference/Elastic network interfaces/AttachNetworkInterface .md#): The instance must be in a **Stopped** or **Running** status.
-   [Detach an ENI from an instance](../../../../reseller.en-US/API Reference/Elastic network interfaces/DetachNetworkInterface.md#): The instance must be in a **Stopped** or **Running** status.
-   [Modify attributes of an ENI](../../../../reseller.en-US/API Reference/Elastic network interfaces/ModifyNetworkInterfaceAttribute.md#): You can modify attributes of an ENI, including its name, its security group, and its description.
-   You can use the [DescribeInstances](../../../../reseller.en-US/API Reference/Instances/DescribeInstances.md#) interface to query the information of an ENI when the ENI is attached to an instance.

