# Switch from Pay-As-You-Go to Subscription billing {#PAYGtoSubs_china .concept}

This topic describes how to switch the billing method of your instance from Pay-As-You-Go to Subscription in the ECS console.

## Limits {#section_vg2_s1f_zdb .section}

You can switch up to 20 Pay-As-You-Go instances to Subscription instances at a time.

## Prerequisites {#section_wg2_s1f_zdb .section}

The ECS instance you want to switch the billing method for must meet the following requirements:

-   The instance type is not a [Generation I](https://www.alibabacloud.com/help/doc-detail/55263.htm) type or a [Generation n1, n2, or e3 type](../reseller.en-US/Instances/Instance type families/Phased-out instance types.md#section_z2t_5ch_4gb).
-   The instance cannot be a [preemptible instance](../reseller.en-US/Instances/Instance purchasing options/Preemptible instances/Preemptible instances.md#).
-   The instance belongs to your account.
-   The instance is in a **Running** or **Stopped** state.

    If an order to switch the billing method has been placed successfully when the ECS instance is in a **Running** or **Stopped** state, but the instance status changes so it no longer meets the preceding requirement when payment is attempted for the order, the order fails and the billing method is unchanged. You can go to the billing center and pay for the order when the instance is in a running or stopped state again.

-   [No timed release is set for the instance](../reseller.en-US/Instances/Manage instances/Release an instance.md#).

    If the release time has been set for an instance, you need to disable the timed release configuration and then switch the billing method.

-   There is no unpaid switch order for the instance.

    If an unpaid switch order exists, you must cancel the unpaid order and then place another order to switch the billing method.


## Procedure {#section_s3c_51f_zdb .section}

1.  Select one or more Pay-As-You-Go instances, and under the instance list, click **Switch to Subscription**.
2.  On the Switch to Subscription page, click **Batch Change**.
3.  In the dialog box, set the **Subscription Plan**, including:
    -   **Duration**: You can set the length of service time for the Subscription instance as 1 month or 1 year. Instances executed in batch must have the same length of service time.
    -   **Data Disk** \(optional\): If Pay-As-You-Go data disks are mounted or attached to the selected instances, you can set whether to also switch their billing method to Subscription.
4.  Click **OK** to place an order and go to the payment page.

    After you make the payment, the operation is complete.


## FAQ {#section_dh5_fjf_zdb .section}

-   What can I do if placing an order fails?

    Adjust the instance accordingly if you are prompted with any of the following error messages:

    -   The current instance status is not supported to switch.
    -   Switch is not allowed because the release time has been set for the instance.
    -   Switch is not allowed because instance information has changed.
    -   A switch order for the instance has not been paid.
-   How long does it take to switch the billing method after I pay for the order?

    Currently, one to four seconds are required to switch the billing method of 1 to 20 instances. After the switch, the billing method is changed to **Subscription** in the console.

-   What can I do if the switch fails?

    [Open a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex).

-   Does the billing method for bandwidth change after the switch?

    No, only the billing method of an instance and data disk can be switched.

-   If I upgrade the configurations of my ECS instance that has an unpaid switch order, is the order still valid?

    The order is invalid. A new order is placed when you switch the billing method of an instance from Pay-As-You-Go to Subscription. This new order must be paid. If the instance is upgraded when the order remains unpaid, the order payment cannot then be made because the instance components change and the order does not meet the requirements to switch the billing method. If you still want to change the billing method of the instance, you must cancel the unpaid order and place a new switch order.


