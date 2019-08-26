# Create a security group {#concept_ocl_bvz_xdb .concept}

A security group is a virtual firewall for an ECS instance. This topic describes how to create a security group in the ECS console.

## Background {#section_rry_yb1_hgb .section}

An ECS instance must belong to one or more security groups. If no security group is created when you create an ECS instance, a default security group will be created. The default security group only has inbound rules configured for the ICMP protocol, SSH port 22, RDP port 3389, HTTP port 80, and HTTPS port 443. For more information, see [Security group overview](../intl.en-US/Security/Security groups/Security group overview.md#). If you do not want the ECS instance to be added to the default security group, you can create a security group as described in this topic.

## Prerequisites {#section_ctl_3vz_xdb .section}

If you want to create a VPC-type security group, confirm that a VPC and a VSwitch have been created. For more information, see [Create a VPC and a VSwitch](../../../../../intl.en-US/User Guide/VPC and subnets/Manage a VPC.md#section_ufw_rhv_rdb).

## Procedure {#section_nyb_kvz_xdb .section}

1.  Log on to the [ECS console](https://ecs.console.aliyun.com).
2.  In the left-side navigation pane, choose **Network & Security** \> **Security Groups**.
3.  Click **Create Security Group**.
4.  In the Create Security Group dialog box, configure the following parameters:
    -   **Template**: If the instances in the security group are for Web server deployment, select a suitable template to simplify security group rule configuration.

        |Template|Description|Scenario|
        |:-------|:----------|--------|
        |**Web Server Linux**|Inbound traffic to TCP port 80, TCP port 443, TCP port 22, and for the ICMP protocol is allowed by default.|A Web server must be deployed on the Linux instances in the security group.|
        |**Web Server Windows**|By default, inbound traffic to TCP port 80, TCP port 443, TCP port 3389, and for the ICMP protocol is allowed.|A Web server must be deployed on the Windows instances in the security group.|
        |**Customize**|After creating a security group, you need to [add security group rules](intl.en-US/Security/Security groups/Add security group rules.md#).|Not for Web server|

    -   **Security Group Name**: specify a valid security group name.
    -   **Description**: the description of the security group for later management.
    -   **Security Group Type**:

        -   Basic Security Group: can be used in scenarios that have higher requirements for refined network control, and prefer multiple ECS instance types and moderate network connections. For more information, see [Security group overview](intl.en-US/Security/Security groups/Security group overview.md#).
        -   Advanced Security Group: can be used in scenarios that have higher requirements for O&M efficiency, ECS instance specifications, and computing nodes. For more information, see [Advanced security group overview](intl.en-US/Security/Security groups/Advanced security group overview.md#).
        **Note:** An ECS instance cannot be added to both a basic security group and an advanced security group.

    -   **Network Type**:
        -   To create a classic network-type security group, select **Classic**.
        -   To create a VPC-type security group, select **VPC** and then a specific VPC.

            **Note:** You must select VPC for an advanced security group.

5.  Click **OK**.

## Results {#section_s8e_xyx_fby .section}

After the security group is created, a new security group is added to the security group list. If you select a custom template, we recommend that you configure security group rules as prompted on the page.

## Related APIs {#section_qj5_221_hgb .section}

You can call [CreateSecurityGroup](../intl.en-US/API Reference/Security groups/CreateSecurityGroup.md#) to create a security group.

## Next operations {#section_agj_cwz_xdb .section}

-   You can [add security group rules](intl.en-US/Security/Security groups/Add security group rules.md#) to allow or deny access to the public or internal networks from ECS instances in security groups.
-   An ECS instance must belong to one or more security groups. You can [add an instance to one or more security groups](intl.en-US/Security/Security groups/Add an ECS instances to a security group.md#) based on your business needs.

