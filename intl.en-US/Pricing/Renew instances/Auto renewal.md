# Auto renewal {#autoRenew_china .concept}

Auto renewal is only applicable to subscription instances. If subscription instances and disks are not renewed within the specified time period, they will be released automatically and all of their data will be permanently lost. You can enable auto renewal for instances to reduce renewal management costs and prevent instances from being released.

## Application scope {#section_70s_l52_dgr .section}

-   Auto renewal can only be enabled on subscription instances.
-   Auto renewal cannot be enabled on instances in the expired state.

## Auto renewal periods {#section_ogq_3gn_a4p .section}

You can enable auto renewal on the Create Instance page when you create a subscription instance, or on the Renew page for an existing subscription instance. The renewal period options are as follows:

-   If you create a new instance and you enable auto renewal on the Create Instance page, the renewal process is as follows:
    -   If the subscription period of an instance is one month, two months, three months, or six months, the instance will continue to automatically renew on a monthly basis after the subscription period ends until you cancel auto renewal. You are billed for each monthly renewal.
    -   If the subscription period of an instance is one year, the instance will continue to renew on a yearly basis after the subscription period ends until you cancel auto renewal. You are billed for each yearly renewal.
-   If you enable auto renewal for an existing instance on the Renew page, you can set the auto renewal period as one month, two months, three months, six months, one year, two years, or three years. When the subscription period ends, the instance will renew for the period you select and you are billed for the new cycle. The instance will then continue to automatically renew for the period you select until you cancel auto renewal. For example, if you select three months, the instance will renew every three months until you cancel auto renewal.

    **Note:** You can modify the auto renewal period for an existing instance at any time on the Renew page.


## Auto renewal rules {#section_1i0_zov_g7d .section}

After auto renewal is enabled, the instance will be automatically renewed before it expires. Specifically,

-   Alibaba Cloud sends an email reminder on the 7th day before the instance expires \(T-7\).
-   Alibaba Cloud collects payment for the next billing cycle from your credit card or PayPal account on the 3rd day before the instance expires \(T-3\). If the payment collection fails, Alibaba Cloud will attempt to collect automatic payment again up to five times until collection is successful, on the following days: the 1st day before the instance expires \(T-1\), the expiration day \(T\), the 7th day after the instance expires \(T+6\), and the 15th day after the instance expires \(T+14\).
    -   At 08:00:00 \(UTC+8\) on the collection day, Alibaba Cloud performs auto-renewal in turn on all the ECS instances that is set to expire. The actual renewal time may be later than 08:00:00 \(UTC+8\), but earlier than 18:00:00 \(UTC+8\).
    -   If payment is collected before T+14, the instance will start the billing cycle from the day the instance was set to expire.
    -   Otherwise, the instance will be in the expired state from T+15. Instances in the expired state cannot be logged on or remotely connected to. If the instance has expired, you must use [manual renewal](reseller.en-US/Pricing/Renew instances/Manual renewal.md#). If the instance is not manually renewed within 15 days after it enters the expired state, the instance will be released and its data will be permanently lost.
    -   If the auto renewal payment fails, Alibaba Cloud will send you an email reminder. Check whether you have received any reminder to avoid expiration of instances.
    -   If manual renewal has been completed before auto renewal, auto renewal will take effect in the next billing cycle.

Assume that you purchased an instance at 10:00:00 November 8, 2017, with a subscription period of one month and auto renewal enabled. The instance is set to expire at 00:00:00 December 9, 2017. The following figure describes actions involved in the first auto renewal round. For more information about the states of a subscription resource after it expires, see [Subscription](reseller.en-US/Pricing/Subscription.md#).

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9592/156394572947363_en-US.png)

## Enable auto renewal {#section_tvl_5nk_zdb .section}

Before enabling auto renewal, make sure you have read and understood [Limits](#section_70s_l52_dgr).

You can enable auto renewal on the Create Instance page. For more information about how to create an instance, see [Create an instance by using the wizard](../reseller.en-US/Instances/Create an instance/Create an instance by using the wizard.md#).

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9592/156394572947299_en-US.png)

On the Renew page, you can enable auto renewal for one or more instances or change the renewal period.

1.  In the top navigation bar, choose **Billing Management** \> **Renew**.
2.  In the left-side navigation pane, click **Elastic Compute Service**.
3.  Click the **Manually Renew** tab.
4.  Find the instance and click **Enable Auto Renewal** in the **Actions** column.

    To enable auto renewal for multiple instances, select multiple instances that have not expired and click **Enable Auto Renewal** at the bottom of the page.

5.  Confirm the instance information and renewal period, and then click **Enable Auto Renewal**.

    Click the **Auto-Renew** tab. The previously selected instances are displayed on the page, indicating that auto renewal has been enabled.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9592/156394572948712_en-US.png)


## Disable auto renewal {#section_xvl_5nk_zdb .section}

1.  In the top navigation bar, choose **Billing Management** \> **Renew**.
2.  In the left-side navigation pane, click **Elastic Compute Service**.
3.  Click the **Auto-Renew** tab.
4.  Find the instance and click **Modify Auto Renewal** in the **Actions** column.

    To enable auto renewal for multiple instances, select multiple instances and click **Modify Auto Renewal** at the bottom of the page.

5.  Select **Disable Auto Renewal** and click **OK**.

    Click the **Manually Renew** tab. The previously selected instances are displayed on the page, indicating that auto renewal has been enabled.


