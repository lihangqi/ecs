# Advanced security group overview {#concept_388533 .concept}

Compared with basic security groups, advanced security groups can contain more ECS instances and ENIs, and can manage unlimited private IP addresses. Advanced security groups are applicable to VPC networks, and have a simplified rule adding mechanism. Advanced security groups can be used in scenarios that have higher requirements for O&M efficiency, ECS instance specifications, and computing nodes.

## Feature comparison {#section_ffp_qw1_dqz .section}

Because you cannot add ECS instances or ENIs to both basic and advanced security groups, we recommend that you learn about the functional differences between the two security group types before planning your network environment. For more information about basic security groups, see [Security group overview](reseller.en-US/Security/Security groups/Security group overview.md#).

|Item|Basic security group|Advanced security group|
|----|--------------------|-----------------------|
|Supports all instance types?|Yes|No. Only supports instances that support IPv6.|
|Supports VPCs?|Yes|Yes|
|Supports classic networks?|Yes|No|
|Rule priority available?|Yes|No|
|Access permissions granted to other security groups?|Yes|No|
|Manual setting of allow security group rules?|Yes|Yes|
|Manual setting of deny security group rules?|Yes|No. All access requests are denied for advanced security groups by default.|
|Number of ENIs supported|Limited by the number of ECS instances in the security group|50,000|
|ENIs bound to any instance type?|Yes. The instance network type must be VPC.|No. ENIs can only be bound to instance types that support IPv6.|
|Number of private IP addresses|2,000|No limit|

## Limits {#section_xlw_3c1_uwi .section}

-   You cannot add ECS instances created before May 30, 2019 to advanced security groups.
-   You can add only instance types that support IPv6 to advanced security groups. For more information, see [Instance type families](../../../../reseller.en-US/Instances/Instance type families.md#).
-   ECS instances and ENIs have the following requirements on security group types:
    -   An ECS instance cannot be added to both a basic security group and an advanced security group.
    -   An ENI cannot be added to both a basic security group and an advanced security group.
    -   When an ENI is bound to an ECS instance, they must belong to the same security group type.

## Console operations {#section_mc4_m5l_zua .section}

In the ECS console, you can use advanced security groups as follows:

1.  [Create an advanced security group](reseller.en-US/Security/Security groups/Create a security group.md#). Set **Security Group Type** to **Advanced Security Group**.
2.  [Add an allow rule to the advanced security group](reseller.en-US/Security/Security groups/Add security group rules.md#).

    An advanced security group is equivalent to a communication whitelist. Only allow rules can be created and no priority values can be set for rules. Authorization objects must be CIDR blocks instead of security groups.

3.  [Add an ECS instance that supports IPv6 to an advanced security group](reseller.en-US/Security/Security groups/Add an ECS instances to a security group.md#). An ECS instance cannot be added to both a basic security group and an advanced security group.
4.  Perform the following steps to use an ENI in an advanced security group:
    1.  If an ENI is already in a basic security group, you can [Modify an ENI](../../../../reseller.en-US/Network/Elastic Network Interfaces/Modify an ENI.md#) to add the ENI to an advanced security group.
    2.  [Bind the ENI to an ECS instance](../../../../reseller.en-US/Network/Elastic Network Interfaces/Attach an ENI.md#).
5.  \(Optional\) [Manage an advanced security group](reseller.en-US/Security/Security groups/Manage security groups.md#). For example, you can add a tag, modify the name and description, and manage ECS instances in the advanced security group.

## API operations {#section_mko_rpm_zop .section}

1.  Call [CreateSecurityGroup](../../../../reseller.en-US/API Reference/Security groups/CreateSecurityGroup.md#) and set SecurityGroupType to enterprise.

    Before creating a security group, confirm that a VPC and a VSwitch have been created.

2.  Call [AuthorizeSecurityGroup](../../../../reseller.en-US/API Reference/Security groups/AuthorizeSecurityGroup.md#) to add a rule which allows inbound traffic to the advanced security group. Authorization objects must be CIDR blocks instead of security groups.

    An advanced security group is equivalent to a communication whitelist. Policy is set to accept by default. You can leave Priority blank, but you must specify IpProtocol, PortRange, SourcePortRange \(optional\), SourceCidrIp, and DestCiderIp.

3.  Call [AuthorizeSecurityGroupEgress](../../../../reseller.en-US/API Reference/Security groups/AuthorizeSecurityGroupEgress.md#) to add an outbound rule to the advanced security group.
4.  Call [JoinSecurityGroup](../../../../reseller.en-US/API Reference/Security groups/JoinSecurityGroup.md#) to add a VPC-type ECS instance to the advanced security group.
5.  Perform the following steps to use an ENI in an advanced security group:
    1.  Call [ModifyNetworkInterfaceAttribute](../../../../reseller.en-US/API Reference/Elastic network interfaces/ModifyNetworkInterfaceAttribute.md#) to add an ENI to an advanced security group, if the ENI is already in a basic security group.
    2.  Call [AttachNetworkInterface](../../../../reseller.en-US/API Reference/Elastic network interfaces/AttachNetworkInterface.md#) to attach an ENI that has been added to an advanced security group to an ECS instance.
6.  \(Optional\) Call [DescribeSecurityGroups](../../../../reseller.en-US/API Reference/Security groups/DescribeSecurityGroups.md#) to view the list of security groups you have created in the current region.

