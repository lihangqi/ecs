# Auto-renewal {#autoRenew_china .concept}

Auto-renewal service only applies to instances that use the Subscription billing method.

## Introduction {#section_pvl_5nk_zdb .section}

If you have activated the auto-renewal service, Alibaba Cloud charges the subscription fee to your linked credit card or PayPal account when the instance expires.

The auto-renewal service can be activated after the ECS instance is purchased and before it expires. It cannot be activated after a Subscription instance expires. Auto-renewal has the following features:

-   The monthly subscription service automatically renews the instance on a monthly basis when a monthly subscription instance expires.
-   The annual subscription service automatically renews the instance on a yearly basis when a yearly subscription instance expires.


**Note:** The auto-renewal service does not support switching between monthly subscription and annual subscription. If you want to change the service duration of an instance, you can choose the [Manual renewal](reseller.en-US/Pricing/Renew instances/Manual renewal.md#) service.

After you activate the auto-renewal service:

-   You are notified of the imminent expiration of your Subscription instances seven days, three days, and one day before the expiration day \(T\).

-   Alibaba Cloud charges the subscription fee to your linked credit card or PayPal account on the expiration day \(T\). If payment fails, Alibaba Cloud will try to take payment again on Day 7 \(T+6\) and Day 15 \(T+14\). If all the three payment attempts fail, the instance is shut down.

    -   If the payment for the subscription is successful, your instance is no longer in an Expired status and the next billing cycle starts from the expiration day.

        For example, if your monthly subscription instance expired at 00:00:00 on April 25, 2016, but it was successfully renewed automatically on May 9, 2016, the billing cycle for this renewal is from 00:00:01 on April 25, 2016 to 00:00:00 on May 25, 2016.

    -   If all the three payment attempts fail, the instance shuts down 15 days after its expiration day. If the instance shuts down, it stops providing services and you cannot log on or remotely connect to the instance. At this point, you can only choose [Manual renewal](reseller.en-US/Pricing/Renew instances/Manual renewal.md#). If the instance is not renewed within the 15 days after the expiration day, the instance is released and the data stored is lost.
    -   If you manually renew the instance before auto-renewal is attempted, your instance is renewed and no auto-renewal is attempted for the current billing cycle. The instance will then be renewed when the current billing cycle ends.
    -   Alibaba Cloud sends a notification email to your linked email address for each failed auto-renewal attempt. Therefore, we recommend that you check your inbox frequently so you can keep up to date with the status of your instance and take necessary actions to avoid further business impact.
-   Alibaba Cloud takes payment for the auto-renewal of instances between 08:00:00 \(UTC+8\) and 18:00:00 \(UTC+8\).


## Activate auto-renewal {#section_tvl_5nk_zdb .section}

To activate the auto-renewal service, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  At the top of the page, choose **Billing Management** \> **Renew**.
3.  In the left-side navigation pane, click **Elastic Compute Service**.
4.  On the Renew page, select the **Manually Renew** tab.
5.  Find an instance, and in the **Actions** column, click **Enable Auto-Renew**.
6.  On the Enable Auto-Renew dialog box, click **Enable Auto-Renew**.

You can then find the instance by selecting the **Auto-Renew** tab.

## Deactivate auto-renewal {#section_xvl_5nk_zdb .section}

To deactivate the auto-renewal service for an instance, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  At the top of the page, choose **Billing Management** \> **Renew**.
3.  In the left-side navigation pane, click **Elastic Compute Service**.
4.  On the Renew page, select the **Auto-Renew** tab.
5.  Find the instance, and in the **Actions** column, click **Modify Auto-Renew**.
6.  On the Modify Auto-Renew dialog box, select **Disable Auto-Renew** and click **OK**.

You can then find the instance by selecting the **Manually Renew** tab.

