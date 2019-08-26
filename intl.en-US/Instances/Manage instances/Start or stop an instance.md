# Start or stop an instance {#concept_mnp_lsl_xdb .concept}

This topic describes how to start or stop an ECS instance in the ECS console. It also describes operations related to the **No fees for stopped instances \(VPC-Connected\)** feature.

## Prerequisites {#section_puw_s2e_c1e .section}

-   The instance you want to start must be in the **Stopped** state.
-   The instance you want to stop must be in the **Running** state.

## Start an instance {#section_bdq_nsl_xdb .section}

To start an instance, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.
3.  In the top navigation bar, select a region.
4.  Find the instance to be started and, in the **Actions** column, choose **More** \> **Instance Status** \> **Start**.

    **Note:** If you want to start multiple **Stopped** instances, select the required instances and then, under the instance list, click **Start**.

5.  Read and confirm you agree to the note displayed in the dialog box by clicking **OK**.

After the instance is started, it enters the **Running** state.

You can also start an instance by calling the [StartInstance](../reseller.en-US/API Reference/Instances/StartInstance.md#) API action through the Alibaba Cloud CLI, OpenAPI Explorer, or Alibaba Cloud SDK.

## Stop a Subscription instance {#section_fdq_nsl_xdb .section}

**Note:** Stopping an instance disrupts services. Exercise caution when performing this action.

To stop an instance, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.
3.  In the top navigation bar, select a region.
4.  Find the instance to be stopped and, in the **Actions** column, choose **More** \> **Instance Status** \> **Stop**.

    **Note:** If you want to stop multiple **Running** instances, select the required instances and then, under the instance list, click **Stop**.

5.  Read and confirm you agree to the note displayed in the dialog box by clicking **OK**.
6.  In the Stop Instance dialog box, set **Stop Mode** and click **OK**.

After the instance is stopped, it enters the **Stopped** state.

## Stop a Pay-As-You-Go instance {#section_nz3_l5r_pgb .section}

**Note:** Stopping an instance disrupts services. Exercise caution when performing this action. The procedure for stopping a preemptible instance is the same as that for a Pay-As-You-Go instance. For more information, see [Stop a preemptible instance](reseller.en-US/Instances/Instance purchasing options/Preemptible instances/Stop a preemptible instance.md#).

Stopping a Pay-As-You-Go instance may affect instance billing. The impact is determined by the network type and the **No Fees for Stopped Instances \(VPC-Connected\)** feature:

-   Classic network: A Pay-As-You-Go instance in the classic network does not support the **No Fees for Stopped Instances \(VPC-Connected\)** feature and the instance still incurs fees after it is stopped. The billing stops only after you [release](reseller.en-US/Instances/Manage instances/Release an instance.md#) the instance.
-   VPC: A Pay-As-You-Go instance in the VPC network supports the **No Fees for Stopped Instances \(VPC-Connected\)** feature:
    -   If this feature is not enabled, billing continues after the instance is stopped.
    -   If this feature is enabled, you can decide whether to keep the instance after you stop the instance by specifying **Keep Stopped Instances and Continue Billing**. If you do not want to keep the instance, resources such as vCPUs, memory, and Internet IP addresses stop incurring fees. However, you are still billed for other resources. For more information, see [No fees for stopped VPC instances](../reseller.en-US/Pricing/No fees for stopped VPC instances.md#).

To stop a Pay-As-You-Go instance, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.
3.  In the top navigation bar, select a region.
4.  Find the Pay-As-You-Go instance to be stopped and, in the **Actions** column, choose **More** \> **Instance Status** \> **Stop**.

    **Note:** If you want to stop multiple **Running** instances, select the required instances and then, under the instance list, click **Stop**.

5.  Complete required actions according to the network type of the instance and whether **No Fees for Stopped Instances \(VPC-Connected\)** is enabled:
    -   If the network type is classic or **No Fees for Stopped Instances \(VPC-Connected\)** is not enabled:
        1.  In the Stop Instance dialog box, set **Stop Mode**.
        2.  Click **OK**.
    -   If **No Fees for Stopped Instances \(VPC-Connected\)** is enabled:

        1.  Read the note displayed in the **Notes** dialog box.
        2.  Confirm the note by clicking **OK**.
        3.  In the Stop Instance dialog box, set **Stop Mode** and **Stopped By**.

            **Note:** If **Keep Stopped Instances and Continue Billing** is selected, the instance continues to incur fees after being stopped. If **Keep Stopped Instances and Continue Billing** is not selected, the instance will not be billed after being stopped.

        4.  Click **OK**.
        **Note:** To disable the **No Fees for Stopped Instances \(VPC-Connected\)** feature, see [No fees for stopped VPC instances](../reseller.en-US/Pricing/No fees for stopped VPC instances.md#).

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9648/15667780375448_en-US.png)


The instance is in the **Stopped** state after you stop it.

You can also stop a Pay-As-You-Go instance by calling the [StopInstance](../reseller.en-US/API Reference/Instances/StopInstance.md#) API action through the Alibaba Cloud CLI, OpenAPI Explorer, or Alibaba Cloud SDK.

