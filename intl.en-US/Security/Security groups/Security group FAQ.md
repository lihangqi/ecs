# Security group FAQ {#concept_mhp_prm_lgb .concept}

-   [What is a security group?](#)
-   [Why do I need to select a security group when I create an ECS instance?](#)
-   [Why am I unable to set Internet security group rules for a VPC instance?](#)
-   [Why am I unable to access TCP port 25?](#)
-   [Why am I unable to access port 80?](#)
-   [Why have several rules been added to a security group automatically?](#)
-   [Why is the priority of some security group rules 110?](#)
-   [Why am I prompted that the number of rules has exceeded the limit when I add an instance to a security group?](#)
-   [What should I do if I create an ECS instance before I create a security group?](#)
-   [What happens when a security group is configured incorrectly?](#)
-   [Are the inbound and outbound rules of a security group counted separately?](#)
-   [Am I able to adjust the maximum number of security group rules allowed?](#)
-   [If I adjust the maximum number of security groups for a VPC instance, does the adjustment apply only to the security groups that I add after the adjustment date?](#)

## What is a security group? {#section_kvb_jxz_lgb .section}

A security group is a virtual firewall that is used to set the network access control for one or more ECS instances. More specifically, security groups logically isolate security domains in the cloud.

Each instance must belong to at least one security group, which is specified when you create an instance. Instances in the same security group can communicate through the intranet. In contrast, instances in different security groups are isolated from each other. However, you can set security group rules to authorize mutual access between two security groups. For more information, see [Security group overview](reseller.en-US/Security/Security groups/Security group overview.md#).

## Why do I need to select a security group when I create an ECS instance? {#section_jym_lxz_lgb .section}

When you purchase an ECS instance, you must select a security group to divide the security domains of the application environment and set security group rules for proper network security isolation.

If you do not select a security group, all the ECS instances that you have created are assigned to the default security group. As a result, you will need to remove instances from the default security group and add them to a new security group.

## Why am I unable to set Internet security group rules for a VPC instance? {#section_rff_5xz_lgb .section}

You are unable to set Internet security group rules for a instance in a VPC because VPC instances can only access the Internet through intranet NIC mapping, which makes the Internet NIC invisible to your instance. As a result, you can only set intranet rules in the security group. The security group rules apply to the intranet and the Internet.

## Why am I unable to access TCP port 25? {#section_kmc_yxz_lgb .section}

TCP port 25 is the default email service port. For security purposes, port 25 of ECS is disabled by default. We recommend that you use port 465 instead to send emails. For more information, see [Scenarios](reseller.en-US/Security/Security groups/Scenarios.md#).

## Why am I unable to access port 80? {#section_avg_cyz_lgb .section}

See [Verify if TCP port 80 works properly](https://partners-intl.aliyun.com/help/faq-detail/59367.htm).

## Why have several rules been added to my security group automatically? {#section_fxk_zxz_lgb .section}

Several rules were added to your security group automatically likely due to one of the following two scenarios:

-   If you have accessed DMS, the relevant rules are automatically added to the security group. .
-   If you have migrated data by using Alibaba Cloud Data Transmission Service \(DTS\), the security group will automatically add the rules relating to the IP address of the DTS service.

## Why is the priority of some security group rules 110? {#section_ohr_1yz_lgb .section}

The security group rules whose priority is 110 are the default rules created by the system. The priority of such default rules is always lower than that of any manually added security group rules. When you manually add security group rules, you can only set the priority to a value ranging from 1 to 100.

## Why am I prompted that the number of rules has exceeded the limit when I add an instance to a security group? {#section_vgd_1zz_lgb .section}

Maximum number of security group rules of an instance \(primary ENI\) = number of security groups that the instance can join × maximum number of rules of each security group.

If you are prompted that the number of rules has exceeded the limit, it means that the number of security group rules applied to the instance has exceeded the upper limit.

## What should I do if I create an ECS instance before I create a security group? {#section_mkc_wxz_lgb .section}

If you have not created a security group before you create an ECS instance, you can select the default security group. The default security group allows commonly used ports, such as TCP port 22 and port 3389. For more information, see [Default security group rules](../../../../../reseller.en-US//Default security group rules.md#).

## What happens when a security group is configured incorrectly? {#section_qrf_nxz_lgb .section}

If a security group is configured incorrectly, mutual access between the ECS instance and other devices through the private network or the Internet will fail. For example:

-   Linux instances cannot be accessed remotely through SSH, or Windows instances cannot be accessed through the remote desktop.
-   The Internet IP address of the ECS instance cannot be pinged.
-   The Web service provided by the ECS instance cannot be accessed through HTTP or HTTPS.
-   Other ECS instances cannot be accessed through the intranet.

## Are the inbound and outbound rules of a security group counted separately? {#section_bll_vyz_lgb .section}

No, inbound rules and outbound rules of a security group are counted together. The total number of inbound rules and outbound rules for each security group cannot exceed 100.

## Am I able to adjust the maximum number of security group rules allowed? {#section_qnp_ryz_lgb .section}

No, the maximum number of security group rules cannot be changed. Each security group can contain only a maximum of 100 security group rules. If the maximum number of instances cannot meet your needs, follow these steps:

1.  Check whether redundant rules exist. You can also open a ticket for Alibaba Cloud technical support.
2.  If any redundant rules exist, clear the redundant rules. If no redundant rules exist, you can create multiple security groups.

**Note:** By default, each ENI of an instance can be added to up to five security groups. Therefore, each ENI of an instance can contain up to 500 security group rules. This is sufficient for most scenarios.

## If I adjust the maximum number of security groups for a VPC instance, does the adjustment apply only to the security groups that I add after the adjustment date? {#section_ftt_wyz_lgb .section}

No, the adjustment applies to the security groups of all VPC instances created before and after the adjustment date.

