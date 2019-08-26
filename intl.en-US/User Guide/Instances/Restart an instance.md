# Restart an instance {#concept_fm2_sxm_xdb .concept}

After paying the overdue bill of a Pay-As-You-Go instance, you must restart the instance. Otherwise, the instance will be released.

For a Pay-As-You-Go instance, if fee deduction fails within 15 days \(T+15\) after payment becomes overdue \(day T\), the instance stops and enters the **Expired** status. You must open a ticket to pay the bill and restart the instance within 30 days \(T+30\) after payment becomes overdue \(day T\). Otherwise, the instance is released and all the data cannot be restored.

**Note:** If you fail to restart the instance within 30 days \(T+30\) after payment becomes overdue \(day T\), the instance is automatically released 30 days after payment becomes overdue and the data cannot be restored.

## Prerequisites {#section_pll_q1n_xdb .section}

The Pay-As-You-Go instance is in the **Expired** or **Expired and Being Recycled** status.

Open a ticket to pay the bill.

## Procedure {#section_qll_q1n_xdb .section}

To restart an instance on the ECS console, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select a region.
4.  Select the target instance. In the Actions column, select **More** \> **Instance Status** \> **Restart**.
5.  Select immediate restart or set a restart time.

If you select immediate restart, the selected instance returns to normal operation in about 10 minutes.

You can also call the ECS API [Reactivateinstances](../../../../../reseller.en-US/API Reference/Instances/ ReactivateInstances.md#) to restart an instance.

