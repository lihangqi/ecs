# Subscription {#subs_china .concept}

Subscription is a billing method that allows you to use resources only after payment for them is received.

## Applicable resources {#section_ilw_jv2_zdb .section}

Currently, Subscription-based billing is applicable to the following ECS resources:

-   ECS instances, including CPU configuration and memory capacity
-   Images
-   System disks and data disks

If you want to create a Subscription ECS instance, the **Total** price shown in the lower left corner of the page includes the costs of the preceding resources.

## Billing cycle {#section_mlw_jv2_zdb .section}

Subscription resources are billed on a monthly basis. The billing cycle is based on UTC+8:00, starting at the time when the resources are activated, and ending at 00:00:00 on the second day after the month or the year \(depending on the billing cycle that is selected\).

For example, if you activated a monthly Subscription ECS instance at 13:23:56 on March 12, 2017, the first billing cycle ended at 00:00:00 on April 13, 2017.

The price unit varies depending on different resources. The following table lists the price units for available resources.

|Resource|Price unit|
|:-------|:---------|
|ECS instance|USD/month|
|Image|USD/month|
|System disk|USD/\(GiB x month\)|
|Data disk|USD/\(GiB x month\)|

After a billing cycle expires, you can renew your ECS instance to continue using the resources. For more information, see [Manual renewal](reseller.en-US/Pricing/Renew instances/Manual renewal.md#) or [Auto-renewal](reseller.en-US/Pricing/Renew instances/Auto-renewal.md#).

## Resource status changes after expiration {#section_qlw_jv2_zdb .section}

After a Subscription instance expires, the status of its corresponding resources changes depending on whether you have enabled [auto-renewal](reseller.en-US/Pricing/Renew instances/Auto-renewal.md#).

-   **If you have not enabled automatic renewal:**

    The Subscription instance will become unavailable at any time within 24 hours from 00:00:00 of the expiration day to 00:00:00 of the next day. If you do not renew the instance within 15 days after it expires, the status of relevant resources will change as follows.

    |Time period|ECS instance and image|System disk|Data disk|Internet IP address|Snapshot|
    |:----------|:---------------------|:----------|:--------|:------------------|:-------|
    |On the expiration day|The instance will become unavailable\* and the image will be disabled.|The system disk will become unavailable, but the data will be retained.|The data disk will become unavailable, but the data will be retained.| For a Classic network instance, the assigned Internet IP address will be retained.

 For a VPC instance, the assigned Internet IP address and the attached EIP address will be retained.

 |Snapshots will not be affected.|
    |More than 15 days after expiration|The ECS instance and the image will be automatically released.|The system disk will be released along with the instance. The data cannot be restored.| By default, the cloud disk will be released along with the instance. If you have set the cloud disk not to be released along with the instance, the disk will stop operating.

 The local disk will be released along with the instance.

 The shared block storage will be automatically detached.

 | For a Classic network instance, the assigned Internet IP address will be released.

 For a VPC instance, the assigned Internet IP address will be released and the attached EIP address will be detached.

 |Automatic snapshots will be automatically deleted, whereas snapshots created manually will not be affected.|

    \* After the instance is **unavailable**, you cannot connect to the instance remotely, and websites deployed on the instance cannot be accessed. Service errors will occur.

    **Note:** [Auto-renewal](reseller.en-US/Pricing/Renew instances/Auto-renewal.md#) cannot be enabled for expired instances.

-   **If you have enabled automatic renewal:**

    If you do not renew the instance within the specified time period, the status of resources corresponding to the instance will change as follows.

    |Time period|ECS instance and image|System disk|Data disk|Internet IP address|Snapshot|
    |:----------|:---------------------|:----------|:--------|:------------------|:-------|
    |Within 15 days after expiration|The ECS instance and the image will operate normally\*.|The system disk will operate normally.|The data disk will operate normally.|The Internet IP address will not be affected.|Snapshots will not be affected.|
    |More than 15 days after expiration|The instance will become unavailable\*\* at any time within 24 hours from 00:00:00 of the 15th day after expiration to 00:00:00 of the 16th day. After that, the image will be disabled.|The system disk will become unavailable, but the data will be retained.|The data disk will become unavailable, but the data will be retained.| For a Classic network instance, the assigned Internet IP address will be retained.

 For a VPC instance, the assigned Internet IP address and the attached EIP address will be retained.

 |Snapshots will not be affected.|
    |More than 30 days after expiration|The ECS instance and the image will be automatically released.|The system disk will be released along with the instance. The data cannot be restored.| By default, the cloud disk will be released along with the instance. If you have set the cloud disk not to be released along with the instance, they will stop operating.

 The local disk will be released along with the instance.

 The shared block storage will be automatically detached.

 | For a Classic network instance, the assigned Internet IP address will be released.

 For a VPC instance, the assigned Internet IP address will be released and the attached EIP address will be automatically detached.

 |Automatic snapshots will be automatically deleted, whereas snapshots created manually will not be affected.|

    \* When the instance **operates normally**, it means that you can start or stop the instance and connect to the instance by using the **management terminal** of the ECS console.

    \*\* After the instance **becomes unavailable**, you cannot connect to the instance remotely, and websites deployed on the instance cannot be accessed. Service errors will occur.


