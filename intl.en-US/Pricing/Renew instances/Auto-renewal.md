# Auto-renewal {#autoRenew_china .concept}

Auto-renewal is a function that helps conveniently renew a monthly or annually billed Subscription instance.

## Background information {#section_pvl_5nk_zdb .section}

After you activate the auto-renewal function, Alibaba Cloud deducts the Subscription fee directly from the credit card or PayPal account associated with your Alibaba Cloud account on the date of instance expiration.

**Note:** 

-   The auto-renewal function cannot be activated after a Subscription instance expires.

-   The auto-renewal function does not support switching between monthly and annually billed Subscriptions. If you want to change the service duration of an instance, see [Manual renewal](reseller.en-US/Pricing/Renew instances/Manual renewal.md#).


After you activate the auto-renewal function:

-   Alibaba Cloud notifies you about the expiration date of an instance seven days prior to its expiration.

-   The fee for the instance is deducted from your Alibaba Cloud account three days before its expiration date. If Alibaba Cloud cannot deduct fees from your account on that day, Alibaba Cloud attempts to deduct fees one day prior to expiration, the day of expiration, six days after and fourteen days after expiration in succession, and sends a notification about each attempt. If all five deduction attempts fail, the instance is suspended 15 days after expiration \(you cannot log on remotely to the instance, but data is retained\). To resolve the issue, you can perform a [manual renewal](reseller.en-US/Pricing/Renew instances/Manual renewal.md#). If the instance is not renewed manually within the 30 days after the expiration date, the instance is released and data is irretrievably lost.

    -   If the payment for the subscription is successful, your instance is no longer in an Expired status and the next billing cycle starts from the expiration day.

        For example, if your monthly subscription instance expired at 00:00:00 on April 25, 2016, but it was successfully renewed automatically on May 9, 2016, the billing cycle for this renewal is from 00:00:01 on April 25, 2016 to 00:00:00 on May 25, 2016.

    -   If you manually renew the instance before auto-renewal is attempted, your instance is renewed and no auto-renewal is attempted for the current billing cycle. The instance will then be renewed when the current billing cycle ends.
-   The time at which the fee is deducted from an Alibaba Cloud account through the auto-renewal method is between 08:00:00 \(UTC+8\) and 18:00:00 \(UTC+8\).


## Activate auto-renewal {#section_tvl_5nk_zdb .section}

To activate the auto-renewal function, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  At the top of the page, choose **Billing Management** \> **Renew**.
3.  In the left-side navigation pane, click **Elastic Compute Service**.
4.  On the Renew page, select the **Manually Renew** tab.
5.  Find the target instance, and in the **Actions** column, click **Enable Auto-Renew**.
6.  On the Enable Auto-Renew dialog box, click **Enable Auto-Renew**.

The instance is then displayed under the **Auto-Renew** tab area.

## Deactivate auto-renewal {#section_xvl_5nk_zdb .section}

To deactivate the auto-renewal function for a target instance, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  At the top of the page, choose **Billing Management** \> **Renew**.
3.  In the left-side navigation pane, click **Elastic Compute Service**.
4.  On the Renew page, select the **Auto-Renew** tab.
5.  Find the target instance, and in the **Actions** column, click **Modify Auto-Renew**.
6.  On the Modify Auto-Renew dialog box, select **Disable Auto-Renew** and click **OK**.

The instance is then displayed under the **Manually Renew** tab area.

