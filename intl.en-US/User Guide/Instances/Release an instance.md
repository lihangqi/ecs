# Release an instance {#concept_jfp_wbf_5db .concept}

You can release a Pay-As-You-Go instance when you no longer need it to avoid excess charges.

For a Pay-As-You-Go instance, if the [No fees for stopped VPC instances](../../../../reseller.en-US/Pricing/No fees for stopped VPC instances.md#) feature is not enabled, charges continue to incur until the instance is released.

For a Subscription instance, the instance is automatically released after the billing cycle expires.

To release a Pay-As-You-Go instance, you can choose either of the following options:

-   Release immediately, which releases the pay-per-order instance at once.
-   Scheduled Release, which customizes the releasetime of your Pay-As-You-Go instance. The time to release the instance must be at least 30 minutes from the current time. Applying new schedules overwrites the previous ones.

**Note:** After an instance is released, its data cannot be recovered. We recommend that you [create a snapshot](reseller.en-US/User Guide/Snapshots/Create a snapshot.md#) to back up data before releasing an instance.

## Release an instance immediately {#section_cqg_ccn_xdb .section}

To release an instance immediately, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the target region.
4.  Set release:
    -   If you want to release only one instance, find the instance that you want to release and then, in the **Actions** column, select **Manage** \> **Release**.
    -   If you want to release multiple instances, find the Pay-As-You-Go instances according to the **Billing Method**, select multiple instances to release, and click **Release Setting** at the bottom of the list.
5.  In the dialog box, select **Release Now**.
6.  Click **Next**, and then click **OK**.

## Enable automatic release {#section_gqg_ccn_xdb .section}

To enable automatic release, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the target region.
4.  Set the release:
    -   If you want to release only one instance, find the instance that you want to release, and in the **Actions** column, select **Manage** \> **Release**.
    -   If you want to release multiple instances, find the Pay-As-You-Go instances according to the **Billing Method**, select multiple instances to release, and click **Release Setting** at the bottom of the list.
5.  In the dialog box, select **Scheduled Release**.
6.  Turn on the Automatic Release switch, and specify the release date and time. The earliest setting can only be set to automatically release an instance after 30 minutes.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9651/154321126332962_en-US.png)

7.  Click **Next**, and then click **OK**.

## Disable automatic release {#section_mqg_ccn_xdb .section}

If you want to cancel the automatic release schedule of a Pay-As-You-Go instance, you can disable the feature.

To disable the automatic release feature, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the target region.
4.  Set the release:
    -   If you want to disable automatic release for an instance, find the instance and then, in the **Actions** column, select **Manage** \> **Release**.
    -   If you want to disable automatic release for multiple instances, find the Pay-As-You-Go instances according to the **Billing Method**, select the target instances, and click **Release Setting** at the bottom of the list.
5.  In the dialog box, select **Scheduled Release**.
6.  Turn off the Automatic Release switch.
7.  Click **Next**, and then click **OK**.

## Related API {#section_rqg_ccn_xdb .section}

[DeleteInstance](../../../../reseller.en-US/API Reference/Instances/DeleteInstance.md#)

