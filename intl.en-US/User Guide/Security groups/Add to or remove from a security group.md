# Add to or remove from a security group {#concept_jhw_31n_xdb .concept}

## Add an instance to a security group {#section_g4z_32n_xdb .section}

You can add an instance to a security group through the console. Up to five security groups can be added to an instance.

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the region.
4.  Select the target instance by clicking the instance name or clicking its corresponding **Manage** button.
5.  Click **Security Groups** in the left-side navigation pane.
6.  Click **Add Security Group** and then select the required security group.
7.  Click **OK**.

After you add an instance to the security group, the rules apply to the instance automatically. 

## Remove an instance from a security group {#section_j4z_32n_xdb .section}

You can remove instances from security groups.

**Note:** 

-   An instance must be in at least two security groups for this action to be performed.
-   Do enough test before this operation to avoid any intranet communication error between instances.

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the target region.
4.  Select the target instance by click the instance name or clicking its corresponding **Manage** button.
5.  In the left-side navigation pane, click **Security Groups**. 
6.  Select the security group to remove from the instance and then click **Remove**.
7.  Click **OK**.

For use cases of security groups, see [scenarios](reseller.en-US/User Guide/Security groups/Scenarios.md#).

