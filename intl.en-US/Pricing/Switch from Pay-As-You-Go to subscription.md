# Switch from Pay-As-You-Go to subscription {#PAYGtoSubs_china .concept}

You can switch your instance from Pay-As-You-Go to subscription in the ECS console.

## Limits {#section_vg2_s1f_zdb .section}

You can only switch up to 20 Pay-As-You-Go instances to subscription instances each time.

## Prerequisites {#section_wg2_s1f_zdb .section}

The ECS instance to be switched must meet the following requirements:

-   The instance type is not any one of [Generation I](https://www.alibabacloud.com/help/doc-detail/55263.htm).

-   The instance belongs to your account.

-   The instance is in the **running** or **stopped** status.

    If an order has been placed successfully when the ECS instance in the **running** or **stopped** status, but the instance status changes and does not meet the status requirement before the order is paid, the payment fails and the switch is discontinued. You can go to the billing center to pay the order when the instance is in the running or stopped status.

-   [No timed release is set for the instance](../../../../intl.en-US/User Guide/Instances/Release an instance.md#).

    If the release time has been set for an instance, you need disable the timed release configuration and then switch the billing method.

-   No unpaid switch order for the instance.

    If an unpaid switch order exists, you need cancel the order and then place another order to switch its billing method.


## Procedure {#section_s3c_51f_zdb .section}

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/).
2.  In the left-side navigation pane, click **Instances**.
3.  Select a region.
4.  Select one or more instances of Pay-As-You-Go mode, and under the instance list, click **Switch to Subscription**.
5.  On the Switch to Subscription page, click **Batch Change**.
6.  On the dialog box, set the **Subscription Plan**, including:
    -   Duration: You can set the length of service time for the subscription instance, 1 month or 1 year. Instances executed in batch must have the same length of service time.
    -   Data Disk: Optional. If some data disks, which may be of Pay-As-You-Go mode, are mounted or attached to the selected instances, you can determine to switch their billing method to Subscription.
7.  Click **OK** to place an order and go to the payment page.

    After you make the payment, the operation is complete.


## FAQ {#section_dh5_fjf_zdb .section}

**What can I do if I fail to place an order?**

Any of the following error messages may be prompted:

-   The current instance status is not supported to switch.
-   Switch is not allowed because the release time has been set for the instance.
-   Switch is not allowed because instance information has changed.
-   A switch order for the instance has not been paid.

If any of the preceding error message is prompted, adjust the instance accordingly.

**How long is the switch completed after I pay the order?**

After you pay the order, an asynchronous task is executed for the switch operation. Currently, one to four seconds are required for switching 1 to 20 instances. After switch, the billing method is changed to **Subscription** in the console.

**What can I do if the switch fails?**

[Open a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex).

**Does the bandwidth billing method change after the switch?**

No. Only the billing method of an instance and data disk can be switched.

**If I upgrade the configurations of my ECS instance that has an unpaid switch order, is the order still valid?**

The order is invalid. A new order is placed when the billing method of an instance switches from Pay-As-You-Go to subscription. This new order must be paid. If the instance is upgraded when the order is not paid, the payment is not allowed because the instance components change and the order amount does not meet the switch requirement. If you still want to change the billing method of the instance, you must cancel the unpaid order and place a new switch order.

