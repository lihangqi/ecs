# Reactivate an instance {#concept_fm2_sxm_xdb .concept}

This topic describes how to reactivate an instance. After paying the overdue bill of a Pay-As-You-Go instance, you must reactivate the instance. Otherwise, the instance will be released.

## Precautions {#section_q1g_3f0_wam .section}

For a Pay-As-You-Go instance, if the due date of an overdue payment \(T\) is not settled within 15 days after the due date \(T+15\), the instance is stopped due to overdue payment and its status changes to **Expired**. You must submit a ticket to settle the payment and reactivate your instance within 30 days after the due date \(T+30\). Otherwise, the instance is released and the data cannot be recovered.

**Note:** If you fail to reactivate the ECS instance within 30 days after the due date \(T+30\), the instance is automatically released 30 days after the due date and the data cannot be recovered.

## Prerequisites {#section_ntt_1fz_xdb .section}

The Pay-As-You-Go instance is in the **Expired** or **Expired and Being Recycled** state.

You have settled the payment by opening a ticket.

## Procedure {#section_qll_q1n_xdb .section}

To reactivate an instance in the ECS console, follow these steps:

1.  Select the instance to be reactivated, and then choose **More** \> **Reactivate** at the bottom of the instance list.
2.  Choose whether to reactivate the instance immediately or later at a specified time.

If you choose to reactivate immediately, the selected instance returns to the **Running** state after about 10 minutes.

Alternatively, you can complete this task by calling the [ReactivateInstances](../reseller.en-US/API Reference/Instances/ReactivateInstances.md#) API action through the Alibaba Cloud CLI, OpenAPI Explorer, or SDK.

