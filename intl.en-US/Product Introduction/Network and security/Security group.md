# Security group {#concept_o2y_mqw_ydb .concept}

A security group is a virtual firewall that provides Stateful Packet Inspection \(SPI\). Security groups are used to set network access control for one or more ECS instances. As an important means of security isolation, security groups are used to divide security domains on the cloud.

A security group is a logical group that contains instances in the same region with the same security requirements and mutual trust. Each instance belongs to at least one security group, which must be specified at the time of creation. Instances in the same security group can communicate through the intranet network, but instances in different security groups cannot communicate by default. However, mutual access between two security groups can be authorized.

## Security group restrictions {#section_njr_v5m_v2b .section}

-   There is a maximum limit for the number of security groups you can have for a region. The limit depends on your level of experience with Alibaba Cloud. For new users, the limit is 100 security groups. For more experienced users, the limit is higher. To raise the upper limit, you can open a ticket.
-   Each Elastic Network Interface \(ENI\) of an instance can join to up to five security groups by default. You can open a ticket to raise the upper limit to a maximum of 16.
-   Security groups have two network types: classic network and Virtual Private Cloud \(VPC\).
    -   Classic network instances can join security groups on classic networks in the same region.

        A single security group on a classic network cannot contain more than 1,000 instances. If you require mutual intranet access between more than 1,000 instances, you can allocate them to different security groups and authorize mutual access.

    -   VPC instances can join security groups on the same VPC.

        A single security group on a VPC cannot contain more than 2,000 private IP addresses \(shared by the primary and secondary ENIs\). If you require mutual intranet access between more than 2,000 private IP addresses, you can allocate the relevant instances to different security groups and authorize mutual access.

-   Adjusting security groups will not affect the continuity of user service.
-   Security groups are stateful. If an outbound packet is permitted, inbound packets corresponding to this connection will also be permitted.

## Security group rules {#section_vsf_nqw_ydb .section}

Security group rules can be set that permit or forbid ECS instances in a security group from accessing a public network or intranet in the inbound and outbound directions.

You can create or delete security group rules at any time. Once changes are made, the updated security group rules are automatically applied to ECS instances in the security group.

When setting security group rules, make sure they are concise. If you add an ECS instance to multiple security groups, hundreds of rules may apply to the instance, which may cause connection errors when you access the instance.

Security group rule restrictions :

-   Each security group can have a maximum of 100 security group rules in total, including both inbound and outbound rules.
-   Each ENI of an instance can have a maximum of 500 security group rules.

