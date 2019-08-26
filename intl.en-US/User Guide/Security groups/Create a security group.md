# Create a security group {#concept_ocl_bvz_xdb .concept}

In the default security group, the default rules only apply to the incoming ICMP traffic and the incoming access to SSH port 22, RDP port 3389, HTTP port 80, and HTTPS port 443. Moreover, the default rules vary according to the network type of the security group. If you do not want to add your instance to the default security group, you can create a custom security group.

## Context {#section_rry_yb1_hgb .section}

Each ECS instance must join at least one security group. For more information, see [Security groups](../../../../../reseller.en-US/Product Introduction/Network and security/Security groups.md#).

If you did not create a security group before creating an instance, you can use the default security group. For more information, see [Default security group rules](reseller.en-US/User Guide/Security groups/Default security group rules.md#).

## Prerequisites {#section_ctl_3vz_xdb .section}

If you want to create a security group for a VPC, you must first [create a VPC and a vSwitch](../../../../../reseller.en-US//Manage a VPC.md#section_ufw_rhv_rdb).

**Note:** If you create a security group in a VPC, you can use that security group together with different vSwitches in that VPC. However, you cannot use that security group in other VPCs.

## Procedure {#section_nyb_kvz_xdb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Network and Security** \> **Security Groups**.
3.  Select a region.
4.  Click **Create Security Group**.
5.  In the displayed Create Security Group dialog box, complete the following configurations:
    -   **Template**: Select a template according to the services deployed in the instances inside the security group. Templates are designed to simplify the configuration of security group rules. The following table describes how templates can be applied to various scenarios.

        |Scenario|Template|Description|
        |Web services need to be deployed in Linux instances in the security group.|**Web Server Linux**|By default, incoming access to TCP ports 80/443/22 and incoming ICMP traffic are allowed.|
        |Web services need to be deployed in Windows instances in the security group.|**Web Server Windows**|By default, incoming access to TCP ports 80/443/3389 and incoming ICMP traffic are allowed.|
        |No special requirements|**Custom**|After the security group is created, you can add security group rules according to your business needs. [Add security group rules](reseller.en-US/User Guide/Security groups/Add security group rules.md#)|

    -   **Security Group Name**: Enter a name for the security group.
    -   **Description**: Enter a description of the security group.
    -   **Network Type**:
        -   To create a security group for a VPC, select **VPC**, and then select the target VPC.
        -   To create a security group for the classic network, select **Classic**.

            ![Create a security group](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9717/15490093594657_en-US.png)

6.  Click **OK**.

If you create a new security group without adding any rules, the default rules for both the Internet and intranet apply. Specifically, outbound access is allowed while inbound access is denied.

## API operations {#section_qj5_221_hgb .section}

You can call [CreateSecurityGroup](../../../../../reseller.en-US/API Reference/Security groups/CreateSecurityGroup.md#) to create a security group.

## What to do next {#section_agj_cwz_xdb .section}

-   You can [add security group rules](reseller.en-US/User Guide/Security groups/Add security group rules.md#) to control the Internet- or intranet-based access of your ECS instances. For information about the ports commonly involved in security group rules, see [Introduction to common ECS instance ports](reseller.en-US/User Guide/Security groups/Introduction to common ECS instance ports.md#). For details about typical use cases, see [Typical applications of security group rules](reseller.en-US/User Guide/Security groups/Typical applications of security group rules.md#).

