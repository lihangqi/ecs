# Security group overview {#concept_o2y_mqw_ydb .concept}

This topic provides an overview of security groups.

## What is a security group? {#section_tz3_3ta_fcu .section}

Security groups are logically isolated groups of instances that are located within the same region and share the same security requirements while also being mutually accessible. They act as virtual firewalls that provide Stateful Packet Inspection \(SPI\), also known as dynamic packet filtering. In a security group, security group rules can be used to grant or limit the access of ECS instances to the Internet or local private networks.

## Limits {#section_onb_uqa_qsc .section}

Security groups have the following limits:

-   Each instance must belong to at least one security group. When you create an instance, you must specify the security group to which the instance will belong.
-   By default, instances in different security groups cannot communicate with each other. However, you can set security group rules to authorize mutual access between two security groups.
-   The maximum session timeout for a security group is 910s.

    **Note:** Security groups are stateful, and states can be kept through sessions. If outbound data packets are allowed for a connection, inbound data packets are also allowed for this connection. When you send a request from your instance, the security group accepts the response in the same session.


## Security group types {#section_m4b_bdb_3gb .section}

Security groups can be divided into basic security group and advanced security group. The following table provides information about these two security group types. For more information, see [Overview of advanced security group](intl.en-US/Security/Security groups/Advanced security group overview.md#).

**Note:** The advanced security group type is in the beta testing phase in China North 5 \(Hohhot\) and US West 1 \(Silicon Valley\). You can [open a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to apply for a free trial.

|Security group type|Security group rule type|Security group rule priority|Inbound rule|Outbound rule|Scenario|
|:------------------|:-----------------------|:---------------------------|:-----------|:------------|:-------|
|Basic security group|Default rules of the basic security group|Depends on the security group template[\*](#)|Depends on the security group template[\*](#)|Allow all access requests.|Scenarios with high network control requirements, multiple ECS instance types, and moderate network connections|
|Custom rules of the basic security group|Custom. Value range: 1 to 100|Supports the allow and deny policies. Add inbound rules as needed.[\*\*](#)|Add outbound rules as needed.[\*\*](#)|
|Advanced security group|Default rules of the advanced security group|1. This value cannot be modified.|Depends on the security group template[\*](#)|Allow all access requests.|Scenarios with high requirements on O&M efficiency, ECS instance types, and computing nodes|
|Custom rules of the advanced security group|Supports the allow policy. Add inbound rules as needed.[\*\*](#)|Allow all access requests.|

\*When you create a security group in the ECS console, you can select Web Server Linux, Web Server Windows, and a custom security group template.

\*\*For more information, see [Add security group rules](intl.en-US/Security/Security groups/Add security group rules.md#) and [Scenarios](intl.en-US/Security/Security groups/Scenarios.md#).

## Default security group {#section_8iv_qrx_d6c .section}

After you create an ECS instance in a region, a default security group is created if no security group has been created under the current account in this region. The default security group is a basic security group.

The default rules of the default security group are as follows:

-   Inbound: ICMP, SSH port 22, and RDP port 3389 are opened. You can also open HTTP port 80 and HTTPS port 443. The rule priority is 110.
-   Outbound: Allow all access requests.

## Security group rule priority {#section_mgh_wv1_wgb .section}

When you add a security group rule, you can set its priority to a value ranging from 1 to 100. A smaller value indicates a higher priority. The priority of a default security group rule is 110, lower than that of any manually created security group.

In a security group or between different security groups, if two security group rules have the same protocol type, port range, authorization type, and authorization object, the rule that takes effect depends on the priority and authorization policy settings of each rule.

-   If both security group rules have the same priority, the deny policy takes effect, but the allow policy does not take effect.
-   If both security group rules have different priorities, the rule with a higher priority takes effect, regardless of the policy settings of both rules.

**Note:** Advanced security groups do not support rule priority settings.

## Network types {#section_7h7_hfv_k8p .section}

For basic security groups, the ENI settings of security group rules vary depending on network types.

-   In a classic network, you must select a private ENI or public ENI before you can set security group rules.
-   In a VPC, you do not need to select a private ENI or public ENI before you set security group rules.

    **Note:** ECS instances in a VPC access the Internet through private ENI mapping. Therefore, you cannot find public ENIs in these ECS instances. You can only set private security group rules, but these rules apply to the Internet and the intranet at the same time.


**Note:** Advanced security groups only support VPCs.

## Workflow {#section_vkd_4kv_vgb .section}

The following figure shows the workflow of basic security groups. For information about the workflow of advanced security groups, see [Overview of advanced security group](intl.en-US/Security/Security groups/Advanced security group overview.md#).

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9569/156290232242063_en-US.png)

## Usage notes {#section_f2k_nmf_4gb .section}

When you use security groups, we recommend that you:

-   Use them as a whitelist.
-   Set the rule policy of all security groups to deny access requests first, and then set the rule policy of these security groups one by one to allow access requests.
-   Observe the principle of least privilege when you configure inbound or outbound rules for applications.
-   Set a specific port \(instead of a port range\) to be opened, for example, port 80/80.
-   Do not grant the access permission to objects whose CIDR block is 0.0.0.0/0 unless necessary when you add security group rules.
-   Do not use one security group to manage all applications because isolation requirements are different at different layers.
-   Add instances with the same security requirements to the same security group. Do not set a separate security group for each instance.
-   Set simple security group rules. If you add an ECS instance to multiple security groups, hundreds of rules may apply to the instance. Any changes to these rules may cause connection errors.
-   Clone an active security group and modify the cloned copy. Modifying the cloned copy allows you to avoid interruptions to your application. After you modify the copy, you can delete the original security group and activate the new copy. For more information, see [Manage security groups](intl.en-US/Security/Security groups/Manage security groups.md#).

