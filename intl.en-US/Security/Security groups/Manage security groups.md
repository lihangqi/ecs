# Manage security groups {#concept_s25_pb1_ydb .concept}

This topic describes how to manage security groups. After you create security groups, you can query, modify, clone, remove, and delete them.

## Query security groups {#section_bg5_lwy_lgb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Network & Security** \> **Security Groups**.
3.  In the top navigation bar, select a region.
4.  Optional. Query the security groups as needed.
    -   To query a security group by using its name, enter the name in the **Security Group Name** text box.
    -   To query a security group by using its ID, enter the ID in the **Security Group ID** text box.
    -   To query all security groups in a VPC, enter its ID in the **VPC ID** text box.

You can also call the API [DescribeSecurityGroups](../reseller.en-US/API Reference/Security groups/DescribeSecurityGroups.md#) to query the basic information of security groups.

## Modify a security group {#section_zv4_twy_lgb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Network & Security** \> **Security Groups**.
3.  In the top navigation bar, select a region.
4.  Find the target security group, and then click **Modify** in the **Actions** column.
5.  Modify the **Security Group Name** and **Description**.
6.  Click **OK**.

You can also call the API [ModifySecurityGroupAttribute](../reseller.en-US/API Reference/Security groups/ModifySecurityGroupAttribute.md#) to modify the name and description of a security group.

## Clone a security group {#section_imc_xwy_lgb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Network & Security** \> **Security Groups**.
3.  In the top navigation bar, select a region.
4.  Find the target security group, and then click **Clone** in the **Actions** column.
5.  In the Clone Security Group dialog box, set the parameters of the new security group.
    -   **Target Region**: Select the specific region in which the new security group applies. Not all regions are supported. The supported regions are displayed in the console.
    -   **Security Group Name**: Specify a name for the new security group.
    -   **Network Type**: Select a network type that applies to the new security group. If you select **VPC**, you must select an available VPC in the target region.
6.  Click **OK**.

## Remove an instance from a security group {#section_usl_bxy_lgb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Network & Security** \> **Security Groups**.
3.  In the top navigation bar, select a region.
4.  On the **Instances** page, find the target instance, and then click **Manage** in the **Actions** column.
5.  Click **Security Groups**.
6.  Find the target security group, and then click **Remove** in the **Actions** column.
7.  Click **OK**.

You can also call the API [LeaveSecurityGroup](../reseller.en-US/API Reference/Security groups/LeaveSecurityGroup.md#) to remove an instance from a specified security group.

## Delete a security group {#section_qjb_lxy_lgb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Network & Security** \> **Security Groups**.
3.  In the top navigation bar, select a region.
4.  Select one or more security groups, and then click **Delete** in the lower-left corner of the list.
5.  In the Delete Security Group dialog box, click **OK**.

You can also call the API [DeleteSecurityGroup](../reseller.en-US/API Reference/Security groups/DeleteSecurityGroup.md#) to delete a security group.

