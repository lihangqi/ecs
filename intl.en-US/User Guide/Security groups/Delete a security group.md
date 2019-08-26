# Delete a security group {#concept_s25_pb1_ydb .concept}

You can delete security groups if you no longer need them. Deleting a security group also deletes all its rules.

**Note:** 

When you want to delete a security group, you must make sure:

-   There are no ECS instances in the security group. For more information on how to move and ECS instance out of a security group, see [add to or remove from a security group](reseller.en-US/User Guide/Instances/Add to or remove from a security group.md#).
-   It is not referenced in the rules of another security group. You can delete a security group directly by following the steps described in this document. If the security group is authorized by another security group, error message shown in the following figure appears. You must delete the corresponding authorization rule.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9723/15433132494661_en-US.png)


## Procedure {#section_pkt_tb1_ydb .section}

To delete a security group, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Networks and Security** \> **Security Groups**.
3.  Select a region to display the list of all security groups in this region.
4.  Select one or more security groups, and click **Delete**.
5.  In the displayed Delete Security Group dialog box, click **OK**.

## Related APIs {#section_eyc_yb1_ydb .section}

-   Delete a security group: [DeleteSecurityGroup](../../../../reseller.en-US/API Reference/Security groups/DeleteSecurityGroup.md#)
-   Query authorization relationships between a security group and another security group: [DescribeSecurityGroupReferences](../../../../reseller.en-US/API Reference/Security groups/DescribeSecurityGroupReferences.md#)
-   Move an ECS instance out of a security group: [LeaveSecurityGroup](../../../../reseller.en-US/API Reference/Security groups/LeaveSecurityGroup.md#)

