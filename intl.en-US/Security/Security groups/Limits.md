# Limits {#concept_kv4_w3s_ggb .concept}

This topic describes the limits of security groups and security group rules.

## Security group limits {#section_njr_v5m_v2b .section}

-   By default, each account can create up to 100 security groups in a region. You can create more if your membership level increases. To raise the limit, open a ticket.
-   By default, each Elastic Network Interface \(ENI\) of an instance can join up to five security groups. To raise the limit, open a ticket. If you do so, Alibaba Cloud assesses your service traffic to see if you need to add your ENI to more security groups. If you pass the assessment, you can add your ENI to 10 or 16 security groups.
-   Security groups are divided into two network types: classic networks and Virtual Private Clouds \(VPCs\).
    -   Classic network instances can join security groups of the classic network type in the same region.

        A single security group of the classic network type cannot contain more than 1,000 instances. If mutual access is required among more than 1,000 instances over the intranet, you can assign them to different security groups and allow mutual access through mutual authorization.

    -   VPC instances can join security groups in the same VPC.

        A single VPC security group can contain up to 2,000 private IP addresses \(shared by the primary and secondary ENIs\). If mutual access is required among more than 2,000 private IP addresses over the intranet, you can assign the relevant instances to different security groups and authorize mutual access.

-   If an outbound packet is permitted, inbound packets corresponding to this connection is also permitted.

For more information, see [Security group FAQ](reseller.en-US/Security/Security groups/Security group FAQ.md#).

## Security group rule limits {#section_mxm_qsb_vfb .section}

Maximum number of security group rules of each ENI of an instance = number of security groups that the instance can join × maximum number of rules of each security group.<span data-goldlog="/cat.main.addNote" class="next-icon next-icon-AddNote next-icon-medium add-note-icon"\> Each ENI of an instance can have up to 500 security group rules.

-   By default, an ENI can join up to five security groups. Each security group can have 100 rules, that is, the total number of inbound and outbound rules of each security group cannot exceed 100.
-   The number of rules in each security group varies according to the number of security groups that an ENI can join. However, the total number cannot exceed 100 \(that is, inbound and outbound rules are not counted separately\).
    -   If each ENI is allowed to join 10 security groups, each security group can have up to 50 rules.
    -   If each ENI is allowed to join 16 security groups, each security group can have up to 30 rules.

The following table shows how the number of rules varies according to the number of security groups.

|Number of security groups|Maximum number of security group rules \(inbound and outbound rules\)|
|:------------------------|:--------------------------------------------------------------------|
|5 \(default value\)|100|
|10 \(you need to open a ticket\)|50|
|16 \(you need to open a ticket\)|30|

