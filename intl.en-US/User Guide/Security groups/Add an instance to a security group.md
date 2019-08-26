# Add an instance to a security group {#concept_jhw_31n_xdb .concept}

You can add an ECS instance to one or more security groups according to your business needs. By default, an ECS instance can join up to five security groups.

## Context { .section}

Security groups are an important means for network security isolation. They are used to set network access control for one or more ECS instances. Each instance must belong to at least one security group.

## Prerequisites {#section_ljq_34c_3gb .section}

-   You have [created an ECS instance](reseller.en-US/User Guide/Instances/Create an instance/Create an instance by using the wizard.md#).
-   Classic network instances must join a security group of the classic network in the same region.
-   VPC instances must join a security group in the same VPC.

## Procedure {#section_g4z_32n_xdb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.

    ![Instance](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9652/155019717532359_en-US.png)

3.  Select a **region**.
4.  Select the target instance on the **Instances** page. Click **Manage** in the **Actions** column.
5.  Click **Security Groups**.

    ![Security Groups](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9652/155019717532366_en-US.png)

6.  Click **Add to Security Group**.

    ![Add an instance to a security group](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9652/155019717532367_en-US.png)

7.  Select the security group to which the instance will be added. If you need to add the instance to multiple security groups, select a security group and then click **Join multiple security groups**. A selection box appears that shows the selected security groups.

    ![Join multiple security groups](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9652/155019717532368_en-US.png)

8.  Click **OK**.

    ![Confirm to join the security group](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9652/155019717532369_en-US.png)


After the instance is added to a security group, the rules of that security group apply to the instance automatically.

## API operations {#section_jsc_fnc_3gb .section}

You can use the [JoinSecurityGroup](../../../../../reseller.en-US/API Reference/Security groups/JoinSecurityGroup.md#) interface to add an instance to a specified security group.

## What to do next {#section_izx_rnc_3gb .section}

-   If you want to view all the security groups that you have created under a region, you can [view the security group list](reseller.en-US/User Guide/Security groups/View the security group list.md#).
-   If you want to modify the name and description of a security group, you can [modify security group attributes](reseller.en-US/User Guide/Security groups/Modify security group attributes.md#).
-   If you want to remove an instance from one or more security groups, you can [remove an instance from a security group](reseller.en-US/User Guide/Security groups/Remove an instance from a security group.md#). If an instance is removed from a security group, it can no longer communicate with other instances in that group through the intranet. Therefore, we recommend that you test your running environment before removing the instance to ensure that your services can continue to run normally.
-   If you no longer need one or more security groups, you can [delete security groups](reseller.en-US/User Guide/Security groups/Delete a security group.md#). Deleting a security group will delete all its rules.

