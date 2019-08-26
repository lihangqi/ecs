# Manage security group rules {#concept_xdb_x11_ydb .concept}

This topic describes how to manage security group rules. After you add security group rules, you can query, modify, restore, export, import, and delete them.

## Query security group rules {#section_elt_zxy_lgb .section}

 **Prerequisites** 

You have added rules to your security groups. For more information, see [Add security group rules](intl.en-US/Security/Security groups/Add security group rules.md#).

 **Procedure** 

1.  Find the target security group, and then click **Add Rules** in the **Actions** column.
2.  Click a rule direction to query the corresponding security group rules.
    -   If you need to query security group rules for a VPC, select **Ingress** or **Outbound**.
    -   If you need to query security group rules for a classic network, select **Internal Network Ingress**, **Internal Network Egress**, **Internet Ingress**, or **Internet Egress**.

You can also call [DescribeSecurityGroupAttribute](../intl.en-US/API Reference/Security groups/DescribeSecurityGroupAttribute.md#) to query security group rules.

## Modify security group rules {#section_icc_hyy_lgb .section}

 **Context** 

If security group rules do not limit access to certain ports, serious security risks may occur. You can modify inappropriate rules to ensure the security of your ECS instances.

 **Prerequisites** 

You have created a security group and added security group rules to the security group. For more information, see [Create a security group](intl.en-US/Security/Security groups/Create a security group.md#) and [Add security group rules](intl.en-US/Security/Security groups/Add security group rules.md#).

 **Procedure** 

1.  On the Security Groups page, find the target security group, and then click **Add Rules** in the **Actions** column.
2.  Click a rule direction of the security group.
    -   If you need to modify security group rules for a VPC, select **Ingress** or **Outbound**.
    -   If you need to modify the security group rules for a classic network, select **Internal Network Ingress**, **Internal Network Egress**, **Internet Ingress**, or **Internet Egress**.
3.  Find the target security group rule, and click **Modify** in the **Actions** column. For information about how to configure security group rules, see [Add security group rules](intl.en-US/Security/Security groups/Add security group rules.md#ul_vpc_qwz_xdb). For information about how to use security group rules, see [Typical applications of security group rules](intl.en-US//Typical applications of security group rules.md#).

## Restore security group rules {#section_l2z_jyy_lgb .section}

 **Context** 

Restoring security group rules means to restore all or some of the rules in a security group to those rules in the target security group.

-   **Complete restoration**: The system deletes the rules that are not in the target security group from the source security group and adds the rules that are only in the target security group to the source security group. After restoration is finished, the rules in the source security group are identical to those in the target security group.
-   **Partial restoration**: The system adds the rules that are only in the target security group to the source security group and ignores the rules that are only in the source security group.

 **Limits** 

-   The source security group and the target security group must be in the same region.
-   The source security group and the target security group must be of the same network type.
-   If there are system-level security group rules \(with a priority level of 110\) in the target security group, these rules cannot be restored. After restoration, the rules in the source security group may be different from expected. If you need the system-level security group rules, you can create similar rules with a priority level of 100.

 **Prerequisites** 

You must have at least one security group of the same network type in the same region.

 **Procedure** 

1.  Find the security group whose rules you want to restore \(this security group serves as the source security group\), and then click **Restore Rules** in the **Actions** column.
2.  In the Restore rules dialog box, perform the following operations as needed:

    1.  Select the **Target Security Group**, which must have different rules from the source security group.
    2.  Select a **Method**.
        -   If you want the source security group to have the same rules as the target security group, select **Completely Restore**.
        -   If you want to add the rules that only exist in the target security group to the source security group, select **Partially Restore**.
    3.  Preview the restoration result.
        -   The rules highlighted in green only exist in the target security group. These rules are added to the source security group regardless of whether you select **Completely Restore** or **Partially Restore**.
        -   The rules highlighted in red do not exist in the target security group. If you select **Completely Restore**, these rules are deleted from the source security group. If you select **Partially Restore**, these rules are retained in the source security group.
    4.  Click **OK**.
    After restoration, the Restore Rules dialog box is closed automatically. On the **Security Groups** page, find the source security group, and then click **Add Rules** in the **Actions** column to open the Security Group Rules page and view the updated security group rules.


## Export security group rules {#section_o1b_syy_lgb .section}

1.  On the Security Groups page, find the target security group, and then click **Add Rules** in the **Actions** column.
2.  Click **Export Rules** to download and save the security group rules to a local JSON file.

    **Note:** The JSON file name uses the following format:

    ecs\_$\{region\_id\}\_$\{groupID\}.json

    If regionID is cn-qingdao and groupID is sg-123, then the name of the exported JSON file is ecs\_cn-qingdao\_sg-123.json.


## Import security group rules {#section_udj_zyy_lgb .section}

1.  In the upper-left corner, select the target region.

    **Note:** You can import security group rules from different regions.

2.  On the Security Groups page, find the target security group, and then click **Add Rules** in the **Actions** column.
3.  Click Import Rules.
4.  Select the target JSON file. You can preview the rules in the file.

    The preview displays the following information:

    -   The number of rules to be imported.
    -   File check results. If any rule that may cause import failure exists in the JSON file, you can move the point over the warning icon for details.
    -   Details of the rules to be imported.
    **Note:** Up to 100 security group rules can be imported. The excessive rules cannot be imported. The newly imported rules do not overwrite the existing rules.

5.  Click **Start**.
6.  View the import result, and then click **Finish and close**.

## Delete security group rules {#section_rmr_tzy_lgb .section}

1.  Find the target security group, and then click the **Add Rules** in the **Actions** column.
2.  Click a rule direction of the security group.
    -   If you need to delete security group rules for a VPC, select **Ingress** or **Outbound**.
    -   If you need to delete the security group rules for a classic network, select **Internal Network Ingress**, **Internal Network Egress**, **Internet Ingress**, or **Internet Egress**.
3.  Find the target security group rule, and then click **Delete** in the **Actions** column.
4.  In the Delete Security Group Rule dialog box, click **OK**.

You can also call [RevokeSecurityGroup](../intl.en-US/API Reference/Security groups/RevokeSecurityGroup.md#) to delete an ingress security group rule or call [RevokeSecurityGroupEgress](../intl.en-US/API Reference/Security groups/RevokeSecurityGroupEgress.md#) to delete an outbound security group rule.

