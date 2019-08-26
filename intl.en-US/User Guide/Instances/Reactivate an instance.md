# Reactivate an instance {#concept_fm2_sxm_xdb .concept}

For a Pay-As-You-Go instance, if the due date of an overdue payment \(T\) is not settled within 15 days after the due date \(T+15\), the instance is stopped due to overdue payment and its status changes to **Expired**. You must submit a ticket to settle the payment and reactivate your instance within 30 days after the due date \(T+30\). Otherwise, the instance is released and the data cannot be recovered.

**Note:** If you fail to reactivate the ECS instance within 30 days after the due date \(T+30\), the instance is automatically released 30 days after the due date and the data cannot be recovered.

## Prerequisites {#section_ntt_1fz_xdb .section}

The Pay-As-You-Go instance is in the **Expired** status.

You have settled the payment by opening a ticket.

## Procedure {#section_qll_q1n_xdb .section}

To reactivate an instance in the ECS console, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the target region.
4.  Select the instance to be reactivated, and then select **More** \> **Reactivate** at the bottom of the instance list.
5.  Choose whether to reactivate the instance immediately or later at a specified time.

If you choose to reactivate immediately, the selected instance returns to the **Running** status after about 10 minutes.

Alternatively, you can also complete the task by calling the ECS API [ReactivateInstances](../../../../reseller.en-US/API Reference/Instances/ ReactivateInstances.md#).

