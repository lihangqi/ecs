# Renew for configuration downgrade {#concept_pjr_l2d_5db .concept}

This topic describes how to downgrade the configuration of a Subscription instance when you renew the instance.

After a Subscription instance expires, if renewal has not been completed in the required time, the instance is released automatically. In this case, data is lost permanently and cannot be recovered. To view status changes that occur after Subscription resources expire, see [Subscription](intl.en-US/Pricing/Subscription.md#).

You can use the **Renew for Configuration Downgrade** feature to downgrade the specifications of a Subscription instance before you update its renewal to help lower costs incurred in the next billing cycle.

You can also change the billing method of your data disks from Subscription to Pay-As-You-Go.

## Limits {#section_fv5_s4k_zdb .section}

When you use the Renew for Configuration Downgrade feature, the following limits apply:

-   The feature allows you to scale down instance specifications at the time of renewal.
-   Renew for Configuration Downgrade can only be used for Subscription instances.
-   You can downgrade the configuration of an instance 15 days prior to its expiration date, or 15 days from its expiration date, but before the instance is released.

    For example, if you have a Subscription instance that expires on April 30, you can downgrade the specifications of the instance and renew it between the dates of April 16 to April 30. If you do not renew the instance at this time, the instance enters the **Recycling Upon Expiration** state. If the instance enters this state, you can still renew the instance from May 1 to May 15. If you do not renew the instance, it is automatically released on May 16.

-   After you renew an instance, the new package is effective from the next billing cycle. The current package continues until the end of the current billing cycle.
-   If instance configurations are changed during renewal, you must [restart the instance](../intl.en-US/Instances/Manage instances/Restart an instance.md#) within the first seven days of the new billing cycle for the new configurations to be effective. If you restart the instance on the seventh day of the new billing cycle, the instance is considered to have used the original package for the first six days, and uses the downgraded package only after it is restarted.
-   Once the renewal for configuration downgrade is complete, you cannot [upgrade configurations](../intl.en-US/Instances/Change configurations/Upgrade configurations/Upgrade configurations of Subscription instances.md#), [increase the system disk size](../intl.en-US/Block Storage/Block storage/Resize cloud disks/Resize cloud disks offline.md#), or increase the size of a Subscription data disk, which is attached to a [Linux instance](../intl.en-US/Block Storage/Block storage/Resize cloud disks/Resize partitions and file systems of Linux data disks.md#) or a [Windows instance](../intl.en-US/Block Storage/Block storage/Resize cloud disks/Extend a Windows file system.md#), during the rest of the current billing cycle.
-   You cannot cancel the renewal orders once the payment is processed.

## Procedure {#section_eql_h4k_zdb .section}

To downgrade the configuration of a Subscription instance during renewal, follow these steps:

1.  Find the Subscription instance. In the **Actions** column, click **Change Configuration**.
2.  In the Configuration Change Guide dialog box, select **Renew for Configuration Downgrade** and click **Continue**.
3.  On the Renew for Configuration Downgrade page, complete the following operations as necessary:
    -   Downgrade **Instance Type**. If you want to downgrade specifications for an instance, you must also set the **Restart Time** for that instance.

        **Note:** 

        -   Instance specifications that can be changed are displayed on the page. For more information about instance specifications, see [Instance type families](../intl.en-US/Instances/Instance type families.md#).
        -   Restarting an instance suspends your business operations on that instance. Please restart the instance during off-peak hours to reduce service impact. The restart must be completed within the first seven days of the next billing cycle.
    -   If a data disk was created while creating a Subscription instance, you can change the billing method of the data disk to **Pay-As-You-Go**. If the billing method is not changed, the data disk has the same billing cycle as the Subscription instance.
    -   Set the bandwidth value.
    -   Set the renewal duration.
4.  Click **Pay**, and follow the prompts to complete the process.
5.  If you have changed instance specifications, or changed the public network bandwidth of an instance in a classic network from 0 Mbit/s to a non-zero value for the first time, you must restart the instance in the console or by using the RebootInstance API within the first seven days of the next billing cycle for the new configurations to be effective.

    **Note:** For a VPC-connected instance, the instance does not need to be restarted.


