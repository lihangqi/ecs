# Security FAQ {#concept_mhp_prm_lgb .concept}

-   Security groups
    -   [What is a security group?](#)
    -   [Why do I need to select a security group when I create an ECS instance?](#)
    -   [What can I do if I create an ECS instance before I create a security group?](#)
    -   [Why am I prompted that the number of rules has exceeded the limit when I add an ECS instance to a security group?](#)
    -   [If I adjust the maximum number of ECS instances that each security group in VPCs can contain, does this adjustment take effect only on the security groups that I create after the time of adjustment?](#)
-   Security group rules
    -   [Why can't I configure public security group rules for my ECS instance in a VPC?](#)
    -   [Why can't I access TCP port 25?](#)
    -   [Why can't I access port 80?](#)
    -   [Why have several internal security group rules been automatically added to my security group?](#)
    -   [Why is the priority of some security group rules 110?](#)
    -   [What happens when a security group rule is configured incorrectly?](#)
    -   [Are the inbound and outbound rules in a security group counted separately?](#)
    -   [Can I adjust the maximum number of rules that can be added to a security group?](#)

## What is a security group? {#section_kvb_jxz_lgb .section}

A security group is a virtual firewall that implements access control for one or more ECS instances. As an important means of security isolation, security groups logically isolate security domains in the cloud.

Each ECS instance must belong to at least one security group. When you create an ECS instance, you must specify a security group for it. Instances in the same security group can communicate with each other, but instances in different security groups are isolated from each other by default. You can configure a security group rule to authorize mutual access between two security groups. For more information, see [Security group overview](intl.en-US/Security/Security groups/Security group overview.md#).

## Why do I need to select a security group when I create an ECS instance? {#section_jym_lxz_lgb .section}

When you create ECS instances, you must select security groups to divide the security domains within your application environment and configure security group rules for proper network security isolation.

If you create an ECS instance in the ECS console in a region where you have not created any security groups, the instance is automatically assigned to the default security group. We recommend that you remove the instance from the default security group and add it to a new security group.

## What can I do if I create an ECS instance before I create a security group? {#section_mkc_wxz_lgb .section}

If you have not created any security groups before you create an ECS instance, you can use the default security group. The default security group allows access to common ports such as TCP port 22 and port 3389. For more information, see the Default security group section in [Security group overview](../../../../intl.en-US//Default security group rules.md#).

## Why am I prompted that the number of rules has exceeded the limit when I add an instance to a security group? {#section_vgd_1zz_lgb .section}

Maximum number of security group rules that can be associated with an ECS instance \(primary ENI\) = Maximum number of security groups that the instance can be added to × Maximum number of rules in each security group

If you are prompted that **the number of rules has exceeded the limit**, the number of security group rules that are associated with the instance has exceeded the upper limit. We recommend that you select another security group.

## If I adjust the maximum number of ECS instances that each security group in VPCs can contain, does this adjustment take effect only on the security groups that I create after the time of adjustment? {#section_ftt_wyz_lgb .section}

No, the adjustment takes effect on all the security groups that you create in VPCs before and after the time of adjustment.

## Why can't I configure public security group rules for my ECS instance in a VPC? {#section_rff_5xz_lgb .section}

It is because instances in VPCs can access the public network only through internal NIC mapping, which makes public NICs invisible in the instances. As a result, you can configure only internal rules in the security groups that your instance belongs to. The security group rules you configure apply to both the internal network and public network.

## Why can't I access TCP port 25? {#section_kmc_yxz_lgb .section}

TCP port 25 is the default email service port. For security reasons, port 25 of ECS instances is disabled by default. We recommend that you use port 465 to send emails. For more application scenarios, see [Scenarios](intl.en-US/Security/Security groups/Scenarios.md#).

## Why can't I access port 80? {#section_avg_cyz_lgb .section}

See [Check whether TCP port 80 is working properly](https://www.alibabacloud.com/help/faq-detail/59367.htm).

## Why have several internal security group rules been automatically added to my security group? {#section_fxk_zxz_lgb .section}

Rules may be automatically added to your security group in either of the following situations:

-   You have accessed Data Management Service \(DMS\). .
-   You have migrated data by using Alibaba Cloud Data Transmission Service \(DTS\). The rules associated with the DTS IP address are automatically added to your security group.

## Why is the priority of some security group rules 110? {#section_ohr_1yz_lgb .section}

The security group rules whose priority is 110 are the default rules created by the system. The priority of the default rules is always lower than that of manually added security group rules. When you manually add security group rules, you can set the priority to a value ranging from 1 to 100.

## What happens when a security group rule is configured incorrectly? {#section_qrf_nxz_lgb .section}

If a security group rule is configured incorrectly, the ECS instances associated with this rule cannot communicate with other devices through the internal network. For example:

-   You cannot access Linux ECS instances remotely by using SSH or access Windows ECS instances by using the Remote Desktop Protocol \(RDP\).
-   The public IP addresses of ECS instances cannot be `pinged`.
-   The Web services provided by the ECS instances cannot be accessed through HTTP or HTTPS.
-   The ECS instances associated with this rule cannot communicate with other ECS instances through the internal network.

## Are the inbound and outbound rules in a security group counted separately? {#section_bll_vyz_lgb .section}

No, the inbound rules and outbound rules of a security group are counted together. The total number of inbound rules and outbound rules for each security group cannot exceed 100. For more information, see [Limits](../../../../intl.en-US/Product Introduction/Limits.md#).

## Can I adjust the maximum number of rules that can be added to a security group? {#section_qnp_ryz_lgb .section}

No, each security group can contain a maximum of 100 security group rules. Each ENI of an ECS instance can be added to a maximum of five security groups by default. Therefore, each ENI of an ECS instance can be associated with a maximum of 500 security group rules, which meets the needs of most scenarios.

If the maximum number of rules in each security group has been reached but you need to add more security group rules, perform the following steps:

1.  Check whether redundant rules exist. You can also [submit a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to ask Alibaba Cloud technical support personnel to check for you.
2.  If any redundant rules exist, delete them and then add new security group rules. If no redundant rules exist, create more security groups and add new security group rules.

