# Manual renewal {#Manualrenew_china .concept}

This topic describes how to manually renew a Subscription instance before the instance is released.

## Introduction {#section_tl3_rmf_zdb .section}

Manual renewal only applies to instances that use the **Subscription** billing method.

You can manually renew your **Subscription** instances when they are in the **Expired** state or are shut down. You can manually renew your instance for a month or a year. Therefore, if you want to modify the service duration of your Subscription instances, you can choose manual renewal.

-   Your instance will still work normally when the instance is in the **Expired** state. If manual renewal is successfully completed within 15 days of the instance expiring, the start of the next billing cycle will be the day the instance expired.

    For example, if your instance expired at 00:00:00 on April 25, 2016, but you successfully renewed it for one month on May 9, 2016, the billing cycle for this renewal is from April 25, 2016 to 00:00:00 on May 25, 2016.

-   If the instance fails to be renewed within 15 days of expiration, the instance will be shut down.

-   After the instance is shut down:

    -   Your instance will stop providing services, but your data will be retained for a further 15 days.
    -   If the instance is renewed within 15 days of the instance being shut down \(within 30 days of the instance expiring\), your instance will enter the new billing cycle from the day of renewal, and your data will be retained for the new cycle.

        For example, if your instance was shut down at 00:00:00 on May 10, 2016, but you successfully renewed it for one month at 08:09:35 on May 23, 2016, the billing cycle for this renewal is from 08:09:35 on May 23, 2016 to 00:00:00 on June 24, 2016.

    -   If the instance is not renewed within 15 days of the instance being shut down \(within 30 days of the instance expiring\), your instance will be automatically released on the 15th day. Your data will be deleted and cannot be restored.

## Procedure {#section_wl3_rmf_zdb .section}

To manually renew your instance, follow these steps:

