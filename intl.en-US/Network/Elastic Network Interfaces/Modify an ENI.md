# Modify an ENI {#concept_wn3_c3k_zdb .concept}

This topic describes how to modify primary and secondary Elastic Network Interfaces \(ENIs\). You can only modify the primary ENI by configuring its associated instance with a different security group as needed, and you can modify a secondary ENI by changing its attributes \(such as the name, associated security group, and description\).

## Limits {#section_ysd_9t4_u7z .section}

Before you can modify the security group to which an ENI belongs, the ENI and its associated ECS instance must meet the following limits:

-   An ECS instance cannot be added to a basic security group and an advanced security group at the same time.
-   An ENI cannot be added to a basic security group and an advanced security group at the same time.
-   An ENI can be attached to an ECS instance only if they belong to the same type of security group.

For more information, see [Security group overview](../reseller.en-US/Security/Security groups/Security group overview.md#).

## Modify a primary ENI {#section_j0k_ece_enn .section}

To modify a primary ENI, follow these steps:

**Note:** The primary ENI and the secondary ENIs of an ECS instance can belong to different security groups. This means that if you associate the ECS instance with another security group, the primary ENI will also be associated with this security group, but the secondary ENIs will remain in the previous security group.

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Network & Security** \> **Security Groups**.
3.  In the top navigation bar, select a region.
4.  Find the target security group, and then click **Manage Instances** in the **Actions** column.
5.  On the **Instances in Security Group** page, modify the security group with which the primary ENI is associated.
    -   To add the primary ENI to a new security group, follow these steps:
        1.  In the upper-right corner of the **Instances in Security Group** page, click **Add Instance**.
        2.  In the displayed dialog box, select an instance ID to which the primary ENI is attached, and then click **OK**.

            The primary ENI is added to the new security group along with the corresponding ECS instance.

    -   To remove the primary ENI from the current security group, follow these steps:
        1.  On the **Instances in Security Group** page, select one or more instances, and then click **Remove from Security Group**.
        2.  In the displayed dialog box, click **OK**.

            The primary ENI is removed from the current security group along with the corresponding ECS instance. Note that the primary ENI and the ECS instance must belong to at least one security group.

6.  Go back to the **Security Groups** page and find the target primary ENI to verify that the settings have taken effect.

Related APIs:

-   [JoinSecurityGroup](../reseller.en-US/API Reference/Security groups/JoinSecurityGroup.md#)
-   [LeaveSecurityGroup](../reseller.en-US/API Reference/Security groups/LeaveSecurityGroup.md#)

## Modify a secondary ENI {#section_mwo_vea_r94 .section}

To modify a secondary ENI, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Network & Security** \> **ENI**.
3.  In the top navigation bar, select a region.
4.  Find the target secondary ENI, and then click **Modify** in the **Actions** column.
5.  In the displayed dialog box, modify the ENI attributes as follows:
    -   **Network Interface Name**: Set a new ENI name according to the rules displayed under this field.
    -   **Security Group**: Select a new security group for the ENI, or remove the ENI from a security group. Note that the ENI must be associated with at least one security group.
    -   **Description**: Modify the description according to the rules displayed under this field.
6.  Click **OK**.

Related API: [ModifyNetworkInterfaceAttribute](../reseller.en-US/API Reference/Elastic network interfaces/ModifyNetworkInterfaceAttribute.md#)

