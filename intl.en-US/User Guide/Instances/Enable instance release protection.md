# Enable instance release protection {#concept_cxt_bpl_ggb .concept}

If your ECS instances provide critical services, you can enable release protection for these ECS instances to prevent irreversible data loss resulting from accidental or incorrect operations during a manual release. This topic describes how to enable and disable instance release protection and view the instance release protection status.

## Limits {#section_djl_xbr_ggb .section}

-   Instance release protection applies only to Pay-As-You-Go instances.
-   An automatic release of an instance due to normal circumstances take precedence. These circumstances include, but are not limited to:
    -   A payment under your account is overdue for more than 15 days.
    -   The automatic release time that you set for the instance is reached.
    -   The instance does not comply with the applicable security compliance policies.
    -   The instance was automatically created by Auto Scaling and consequently is removed from the scaling group when the scaling group scales in.

## Enable instance release protection when you create an instance {#section_mnn_wdr_ggb .section}

**Note:** This procedure describes the instance release protection settings. For information about other settings, see [Create an instance by using the wizard](reseller.en-US/User Guide/Instances/Create an instance/Create an instance by using the wizard.md#).

To enable instance release protection when you create an instance, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  On the Instances page, click **Create Instance**.
4.  On the Basic Configurations page, set the **Billing Method** to **Pay-As-You-Go**, set other parameters as needed, and then click **Next: Networking**.
5.  On the **Networking** page, set the parameters as needed, and then click **Next: System Configurations**.
6.  On the **System Configurations** page, select **Prevent users from releasing the instance inadvertently by using the console or API**, set the parameters as needed, and then click **Next: Grouping**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83469/154755689237279_en-US.png)

7.  On the Grouping page, set the parameters as needed, and then click **Next: Preview** and confirm your settings.

When you create an instance through [RunInstances](../reseller.en-US/API Reference/Instances/RunInstances.md#) or [CreateInstance](../reseller.en-US/API Reference/Instances/CreateInstance.md#), you can use the DeletionProtection parameter to enable or disable instance release protection.

## Enable or disable instance release protection by modifying instance information {#section_vqv_d2r_ggb .section}

To enable or disable instance release protection by modifying the information of an instance, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  On the Instances page, select **More** \> **Instance Settings** \> **Modify Information** in the **Actions** column of the instance to be modified.
4.  In the Modify Information dialog box, select**Enable instance release protection**.

    **Note:** To disable the instance release protection, clear **Enable instance release protection**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83469/154755689237280_en-US.png)

5.  Click **OK**.

When you modify instance information through [ModifyInstanceAttribute](../reseller.en-US/API Reference/Instances/ModifyInstanceAttribute.md#), you can use the DeletionProtection parameter to enable or disable instance release protection.

## View the instance release protection status {#section_ypk_g2r_ggb .section}

To view the release protection status of an instance, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  On the Instances page, click the target instance in the **Instance ID/Name** column, or click **Manage** in the **Actions** column of the instance.
4.  On the Instance Details page, view the status of **Enable release protection** in the **Payment Information** area.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83469/154755689237282_en-US.png)


## Example of protection effect {#section_jhk_dhs_ggb .section}

After you enable release protection for an instance, a warning message will be displayed if you try to manually release the instance. If you want to manually release the instance, you must [disable instance release protection](#section_vqv_d2r_ggb).

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/83469/154755689237284_en-US.png)

After you enable release protection for an instance, the error code `InvalidOperation.DeletionProtection` is returned if you try to use [DeleteInstance](../reseller.en-US/API Reference/Instances/DeleteInstance.md#)to delete the instance.

