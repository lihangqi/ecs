# Pay-As-You-Go {#Pay-As-You-Go .concept}

With the Pay-As-You-Go billing method, you are charged based on the amount of resources you actually use. Pay-As-You-Go allows you to activate and release resources at any time to meet your requirements. You can purchase resources on demand, and scale up as your business grows. Costs can be reduced by 30% to 80% compared with the investment on a traditional host, with which many resources may be wasted at times.

## Applicable resources {#section_2s1_uri_cet .section}

Currently, the Pay-As-You-Go billing method is applicable to the following ECS resources:

-   ECS instances, including CPU configuration and memory capacity
-   Images
-   System disks and data disks

If you create an ECS instance that uses the Pay-As-You-Go billing method, the **Instance Cost** displayed at the bottom of the instance creation page is the total fee for the preceding three types of resources.

You can make the following changes after activating Pay-As-You-Go resources:

-   **Resource configuration change** 

    You can change the instance types, including CPU configuration and memory capacity, after you create an instance. For more information, see [Change configurations of Pay-As-You-Go instances](../../../../reseller.en-US/Instances/Change configurations/Change configurations of Pay-As-You-Go instances/Change configurations of Pay-As-You-Go instances.md#).

-   **Billing method change** 

    You can change the billing method of instances, system disks, and data disks from Pay-As-You-Go to Subscription. For more information, see [Switch from Pay-As-You-Go to Subscription billing](reseller.en-US/Pricing/Switch from Pay-As-You-Go to Subscription billing.md#).


## Billing cycle {#section_sp4_7am_4k6 .section}

A Pay-As-You-Go resource is billed by second after it is created, and billing stops after it is released. For a VPC instance, you can enable the [No fees for stopped VPC instances](reseller.en-US/Pricing/No fees for stopped VPC instances.md#) feature to ensure that the VPC instance is not billed when it is in the **Stopped** status. This feature is available only for instances.

The minimum charge for the life cycle of an ECS instance \(from creation to release\) is USD 0.01.

|Item|Instance + Image|System disk|Data disk|
|:---|:---------------|:----------|:--------|
|Billing cycle|One second|One second|One second|
|Price unit|USD/hour|USD/\(GiB \* hour\)|USD/\(GiB \* hour\)|

## Settlement period {#section_7yw_afz_d31 .section}

Pay-As-You-Go resources are billed by second, but settled by hour. Note the following:

-   Payments for Pay-As-You-Go resources are settled together with other products under your account that are billed after you use them.

-   Generally, if the cumulative monthly consumption amount of your account is less than 1,000 USD, fees are deducted on the first day of the following month.

-   If you have a quota agreement with Alibaba Cloud, fees are deducted when the cumulative consumption amount of your account exceeds the quota.

|Cumulative consumption amount|Due date \(T\)|Fee deduction day|Description|
|-----------------------------|--------------|-----------------|-----------|
|Cumulative monthly consumption amount less than 1,000 USD.|The first day of the following month.|T, T+7, and T+14| -   In the event of deduction failure on the due date \(T\), the system attempts to deduct fees again on the day T+7 and the day T+14.
-   If fee deduction fails three times, the instance goes out of service on the day T+15. In this case, the instance stops running but data is retained. Billing stops when the instance is out of service.
-   When your instance is out of service, you must open a ticket to clear the overdue payment. After the overdue payment is cleared, you must reactivate the instance before the day T+30. Otherwise, the instance is released automatically.
-   If the overdue payment fails to be cleared before the day T+30, the instance is released and data cannot be recovered.
 |
|Agreed quota|On the day when the quota is exceeded|


## Instructions for settlement {#section_n1m_c53_1nk .section}

-   **Settlement period**

    -   For ECS instances: The active duration is the time during which the ECS instance runs properly, starting from when the ECS instance is activated to when it is released or expires. If the instance is out of service during the active duration due to an overdue payment, billing stops until the payment is cleared.
    -   For system disks and data disks: The active duration is the time during which the disks run properly, starting from when the disks are activated to when they are released. Fees are charged by hour.
-   **Release rules**

    -   If payment for an ECS instance is overdue, usage of Pay-As-You-Go cloud disks is restricted, and the cloud disks cannot process I/O read and write requests properly, affecting the normal running of the ECS instance. The impact includes but is not limited to reduced performance of application read/write, serious time-out of some operations, and power-off or restart failure for some operating system versions.
    -   ECS instances configured with the automatic release time are automatically released at a specified time.
    -   Notification of release: In the event of service expiration or overdue payment, the system notifies you by email.

## Resource status when an instance is out of service {#section_v7p_yu0_p4g .section}

If you fail to pay for Pay-As-You-Go resource fees three times in one settlement period, the instance is out of service on the day T+15. When your instance is out of service, you cannot use the resources normally until you clear the overdue payment. Once the payment is cleared, you must reactivate the instance within the specified period. The following table lists the status of the related resources once the instance is out of service.

|Period|ECS instance and image|System disk and data disk|Internet IP address|Snapshot|
|:-----|:---------------------|:------------------------|:------------------|:-------|
|Within 15 days after the instance goes out of service \(T+15 to T+30\)|Both stop working.|When the instance is out of service\*, the capability of related cloud disks and local disks is limited. But the data on them is retained.| -   For instances of the classic network type: The assigned Internet IP address is retained.
-   For VPC instances: If an Internet IP address is assigned, it is retained. If an elastic IP \(EIP\) address is bound to the instance, it is retained.

 |Retained.|
|15 days after the instance goes out of service \(T+30\)|Released automatically. You are notified in advance by emails if your resources will be released.| -   All cloud disks, including system disks and data disks are released automatically regardless of whether they are attached to the instance and whether they are created separately or at the same time as the instance. Data on the cloud disks cannot be recovered.
-   Local disks are released automatically, and data on them cannot be recovered.
-   If Shared Block Storage is attached to the instance, it is detached automatically, and data on it is retained.

 | -   For instances of the classic network type: The assigned Internet IP address is released.
-   For VPC instances: If an Internet IP address is assigned, it is released. If an EIP address is bound to the instance, it is unbound automatically.

 |Automatic snapshots are deleted automatically. Snapshots that are manually created are retained.|

\* When a Pay-As-You-Go instance is out of service, you cannot remotely connect to the instance or access websites hosted on the instance.

## FAQ {#section_tyq_kj8_4ou .section}

**If a Pay-As-You-Go ECS instance is out of service or has stopped running, are fees still incurred?**

An instance stops working and is rendered out-of-service when a payment is overdue. When a Pay-As-You-Go instance is out of service, it is in the **Expired** status, and no fees are incurred.

A stopped instance is stopped through the ECS console or by calling StopInstance. Billing of a stopped instance varies according to the network type of the instance:

-   VPC: You can enable the [no fees for stopped instances](EN-US_TP_9595.dita#concept_js1_1fd_5db) feature. If this feature is enabled, the instance is not billed when it is in the **Stopped** status. This feature is available only for instances.
-   Classic: An instance continues to be billed even after it is in the **Stopped** status.

