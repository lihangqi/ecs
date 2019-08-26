# Start or stop an instance {#concept_mnp_lsl_xdb .concept}

This article describes how to start or stop an ECS instance.

## Start an instance {#section_bdq_nsl_xdb .section}

You can start an instance in the ECS console. When an instance starts successfully, it is in the **Running** status.

**Prerequisite**

The instance must be in the **Stopped** status.

**Procedure**

To start an instance, follow these steps:

1.  Log on to the [ECS Management console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the target region.
4.  Find the instance to be started and, in the **Actions** column, select **More** \> **Instance Status** \> **Start**. If you want to start multiple **Stopped** instances, select the required instances and then, under the instance list, click **Start**.
5.  Read and confirm you agree to the note displayed in the dialog box by clicking **OK**.

The instance is in the **Running** status after it is started.

## Stop an instance {#section_fdq_nsl_xdb .section}

To stop an instance is to shut it down. You can stop an ECS instance in the ECS console. When an instance stops successfully, it is in the **Stopped** status.

**Note:** Stopping an instance disrupts services. Exercise caution when performing this action.

If you stop a \(Subscription\) instance before its billing cycle is completed, the bill for that cycle is not affected. If the auto-renewal service is activated, you are still billed for the stopped instance at the start of each new billing period.

For a Pay-As-You-Go instance, its network type and the No Fees for Stopped Instances \(VPC-Connected\) feature determine billing:

-   VPC: If the **No Fees for Stopped Instances \(VPC-Connected\)** feature is enabled, you can decide whether to continue being billed for the instance. However, you are still billed for other ECS-related resources. For more information, see [no fees for stopped instances \(VPC-Connected\)](../../../../../reseller.en-US/Pricing/No fees for stopped VPC instances.md#). If this feature is not enabled, billing continues after the instance is stopped.
-   Classic network: A stopped instance still incurs fees. Billing stops only after you [release the instance](reseller.en-US/Instance/ECS instance life cycle/Release an instance.md#).

**Prerequisite**

The instance is in the **Running** status.

**Procedure**

To stop an instance, follow these steps:

1.  Log on to the [ECS Management console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the target region.
4.  Find the instance to be stopped and, in the **Actions** column, select **More** \> **Instance Status** \> **Stop**. If you want to stop multiple **Running** instances, select the required instances and then, under the instance list, click **Stop**.
5.  According to the billing method and network type of the instance, complete the required actions:
    -   Subscription instance or classic network pay per volume instance: In the Stop Instance dialog box, select **Stop** or **Force Stop**, and then click **OK**.
    -   A VPC-Connected Subscription instance:

        -   If the **No Fees for Stopped Instances \(VPC-Connected\)** feature is enabled, read the Notice, select **Stop** or **Force Stop** in the Stop Instance dialog box, select a mode \(whether to keep the instance after stopping and continue charging\), and then click **OK**.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9648/15510233715448_en-US.png)

        -   If the **No Fees for Stopped Instances \(VPC-Connected\)** feature is disabled, in the Stop Instance dialog box, select **Stop** or **Force Stop**.

            **Note:** To disable the **No Fees for Stopped Instances \(VPC-Connected\)** feature, see [no fees for stopped instances](../../../../../reseller.en-US/Pricing/No fees for stopped VPC instances.md#disable).


Once the instance is successfully stopped, the instance enters the **Stopped** status. For a VPC-Connected Pay-As-You-Go instance, if you select not to keep the instance, **Stop Instance, No Fees** is shown in the instance list. Otherwise, **Keep Instance, Fees Apply** is shown. For other ECS instances, no information is shown.

## Related APIs {#section_pdq_nsl_xdb .section}

Start instance: [StartInstance](../../../../../reseller.en-US/API Reference/Instances/StartInstance.md#)

Stop instance: [StopInstance](../../../../../reseller.en-US/API Reference/Instances/StopInstance.md#)

