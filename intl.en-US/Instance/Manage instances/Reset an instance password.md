# Reset an instance password {#concept_qct_gfl_xdb .concept}

This article describes how to use the Reset Password feature to specify a new logon password for an instance.

**Note:** You must restart an instance after its password is reset, which may disrupt services. Exercise caution when performing this action.

## Prerequisite {#section_mg1_3fl_xdb .section}

The instance must be in a stable status, such as **Stopped** and **Running**. For more information, see [ECS instance life cycle](../../../../../reseller.en-US/Instance/ECS instance life cycle/ECS instance life cycle.md#).

## Procedure {#section_ng1_3fl_xdb .section}

To reset a password for one or multiple ECS instances, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the target region.
4.  According to the number of instances to be operated, do the following:
    -   To reset the password for one instance, find the target instance and, in the **Actions** column, select **More** \> **Password/Key Pair** \> **Reset Password**.

    -   To reset the passwords for multiple instances, select the target instances and, under the instance list, click **Reset Password**.

5.  Specify a new valid password, and click **Submit**.
6.  To make the password change take effect, change the instance status to one of the following:
    -   **Running**: [Restart an instance](reseller.en-US/Instance/ECS instance life cycle/Restart an instance.md#) in the console.
    -   **Stopped**: Start the instance in the console.

## Related operations {#section_sg1_3fl_xdb .section}

To modify the password: follow [Step 3: Connect to an instance](../../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 3: Connect to an instance.md#), then [change the password in the ECS instance](https://partners-intl.aliyun.com/help/faq-detail/40647.htm).

