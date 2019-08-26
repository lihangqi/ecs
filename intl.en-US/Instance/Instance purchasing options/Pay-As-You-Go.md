# Pay-As-You-Go {#Pay-As-You-Go .concept}

With the Pay-As-You-Go billing method, you are charged based on the amount of resources you actually use. Pay-As-You-Go allows you to activate and release resources at any time to meet your requirements. You can purchase resources on demand, and scale up as your business grows. Costs can be reduced by 30% to 80% compared to a traditional host investment, with which many resources may be wasted at times.

**Note:** All the charging rules described in this article is for reference purpose only. For more information, please contact your service provider.

## Applicable resources {#section_xmc_xbg_c2b .section}

Currently, the Pay-As-You-Go billing method is applicable to the following ECS resources:

-   ECS instances, including CPU configuration and memory capacity
-   Images
-   System disks and/or data disks

If you create an ECS instance that uses the Pay-As-You-Go billing method, the **Instance Cost** displayed in the bottom of the instance creation page is the total fee for the preceding three types of resources.

You can make following changes after activating Pay-As-You-Go resources:

-   Resource configuration change:

    You can change the instance types, including CPU configuration and memory capacity, after you create an instance. For more information, see [Change configurations of Pay-As-You-Go instances](../../../../../reseller.en-US/Instance/Change configurations/Change configurations of Pay-As-You-Go instances/Change configurations of Pay-As-You-Go instances.md#).

-   Billing method change:

    Instances, system disks, and data disks support switching from Pay-As-You-Go billing to Subscription billing. For more information, see [Switch from Pay-As-You-Go to Subscription billing](reseller.en-US/Pricing/Switch from Pay-As-You-Go to Subscription billing.md#).


## Payment methods {#section_kgq_1gm_42b .section}

Credits are used to pay for the resources of the Pay-As-You-Go billing method.

## Billing period {#section_rbk_ldg_c2b .section}

A Pay-As-You-Go resource is billed by the second after is it created, and billing stops after it is released.

For a VPC instance, you can enable the [no fees for stopped instances feature](reseller.en-US/Pricing/No fees for stopped VPC instances.md#). When the feature is enabled, a VPC instance is not billed when it is in a **Stopped** status. This feature is only available for instances, and not for other ECS resources.

The billing cycle varies depending on the resource types. The minimum charge for the lifecycle of an ECS instance \(from creation to release\) is USD 0.01.

|Item|Instances + Images|System disks|Data disks|
|:---|:-----------------|:-----------|:---------|
|Billing cycle|One second|One second|One second|
|Price unit|USD/hour|USD/\(GiB \* hours\)|USD/\(GiB \* hours\)|

## Settlement cycle {#section_ipb_4x2_zdb .section}

Pay-As-You-Go resources are billed by the second, but settled by the hour. Note the following:

-   Payments for Pay-As-You-Go resources are settled together with other products under your account that are billed after you use them.

-   Generally, if the cumulative monthly consumption amount of your account is less than 1,000 USD, fees are deducted on the first day of the following month.

-   If you have a quota agreement with Alibaba Cloud, fees are deducted when the cumulative consumption amount of your account exceeds the quota.


## Instructions for settlement {#section_mwz_qx2_zdb .section}

-   **Settlement period**

    -   For ECS instances: The active duration is the time during which the ECS instance runs properly, starting from when the ECS instance is activated to when it is released or expires. If the instance is out of service during the active duration due to an overdue payment, billing stops until the payment is cleared.
    -   For system disks and/or data disks: The active duration is the time during which the disks run properly, starting from when the disks are activated to when they are released.
-   **Release rules**

    -   If payment for an ECS instance is overdue, usage of Pay-As-You-Go cloud disks is restricted, and the cloud disks cannot process I/O read and write requests properly, affecting the normal running of the ECS instance. The impact includes but is not limited to the reduced performance of application read/write, serious time-out of some operations, and power-off or restart failure for some operating system versions.
    -   ECS instances configured with the automatic release time are automatically released at a specified time.
    -   Notification of release: In the event of service expiration or overdue payment, the system notifies you by email.

## Resource status when an instance is out of service {#section_rpb_4x2_zdb .section}

If you fail to pay for the Pay-As-You-Go resources fees three times in one settlement period, the instance is out of service on the day T+15. When your instance is out of service, you cannot use the resources normally until you clear the overdue payment. Once the payment is cleared, you must [reactivate the instance](../../../../../reseller.en-US/Instance/ECS instance life cycle/Restart an instance.md#) within the specified period. The following table lists the status of the related resources once the instance is out of service.

|Period|ECS instance and image|System disk + data disks|Internet IP address|Snapshots|
|:-----|:---------------------|:-----------------------|:------------------|:--------|
|Within 15 days of the instance going out of service \(T+15 to T+30\)|Both stop working.|When the instance is out of service\*, the capability of the cloud disks and the local disks is limited. But the data on them is retained.| -   For instances of the Classic network type: The assigned Internet IP address is retained.
-   For VPC instances: If an Internet IP address is assigned, it is retained. If an elastic IP \(EIP\) address is bound to the instance, it is retained.

 |Retained.|
|15 days after the instance goes out of service \(T+30\)|Released automatically. You are notified in advance by emails when the resources will be released.| All cloud disks, including system disks and data disks that are created separately or together with the instance, or that are attached to the instance or not, are released automatically. The data cannot be recovered.

 The local disks are released automatically, and the data on them cannot be recovered.

 If shared block storage is attached to the instance, it is detached automatically, and the data on it is retained.

 | For instances of the Classic network type: The assigned Internet IP address is released.

 For VPC instances: If an Internet IP address is assigned, it is released. If an EIP address is bound to the instance, it is unbound automatically.

 |The automatic snapshots are deleted automatically. The snapshots that are manually created are retained.|

\* When a Pay-As-You-Go instance is **out of service**, the instance is in an **Expired**status. During the period it is out of service, no fees are incurred.

## FAQs {#section_utf_tx2_zdb .section}

**If a Pay-As-You-Go ECS instance is out of service or has stopped running, are fees still incurred?**

An instance stops working and is rendered out-of-service when a payment is overdue. When a Pay-As-You-Go instance is out of service, it is in an **Expired** status, and no fees are incurred.

A stopped instance is in a Stopped status and has been stopped [in the ECS console](../../../../../reseller.en-US/Instance/ECS instance life cycle/Start or stop an instance.md#) or by using the [StopInstance](../../../../../reseller.en-US/API Reference/Instances/StopInstance.md#) interface. Billing of a stopped instance varies according to the network type of the instance:

-   VPC: You can enable the [No fees for stopped instances \(VPC-Connected\)](reseller.en-US/Pricing/No fees for stopped VPC instances.md#) feature. When this feature is enabled, an instance is not billed when it is in a **Stopped** status. This feature is only available for instances, and not for other resources.

-   Classic: An instance continues to be billed even after it is in a **Stopped** status.


