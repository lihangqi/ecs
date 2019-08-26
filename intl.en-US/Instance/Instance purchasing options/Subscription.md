# Subscription {#subs_china .concept}

For the Subscription billing method, you can use resources only after you have paid for them.

**Note:** All the charging rules described in this article is for reference purpose only. For more information, please contact your service provider.

## Applicable resources {#section_ilw_jv2_zdb .section}

Currently, Subscription billing is used for the following ECS resources:

-   ECS instances, including CPU configuration and memory capacity
-   Images
-   System disks and/or data disks

If you create an ECS instance that uses Subscription billing, the **Instance Cost** displayed in the lower right of the instance creation page is the total cost of the three resources listed.

## Payment methods {#section_kx5_l2m_42b .section}

Credits are used to pay for the resources of the Subscription billing method.

## Billing period {#section_mlw_jv2_zdb .section}

Resources in Subscription mode are billed on a monthly basis. The billing period is based on the UTC+8 time zone. It starts from the resource activation time and ends at 00:00:00 on the second day after one month or one year.

For example, if you activate an ECS instance in Monthly Subscription mode at 13:23:56 March 12, 2017, the first billing cycle for the instance ends at 00:00:00 April 13, 2017.

The price unit varies depending on the resource. The following table lists the price units for various resources.

|Resource|Price unit|
|:-------|:---------|
|ECS instance|USD/month|
|Image|USD/month|
|System disk|USD/\(GiB\*month\)|
|Data disk|USD/\(GiB\*month\)|

To continue using a resource after the billing period has ended, you can renew your ECS instance at the end of a billing period. For more information about the renewal procedure, see [Manual renewal](reseller.en-US/Pricing/Renew instances/Manual renewal.md#) or [Auto-renewal](reseller.en-US/Pricing/Renew instances/Auto-renewal.md#).

## Status changes after expiration {#section_qlw_jv2_zdb .section}

The status of a Subscription instance after it expires will change depending on whether the auto-renewal feature is enabled.

-   **Auto-renewal disabled**

    If auto-renewal is disabled, and a Subscription instance is not renewed at the end of the billing period, it goes out of service within the 24 hours from 00:00:00 on the expiration day to 00:00:00 the next day. The status changes of related resources are shown in the following table.

    |Period|ECS instances and images|System disks|Data disks|Internet IP addresses|Snapshots|
    |:-----|:-----------------------|:-----------|:---------|:--------------------|:--------|
    |On the expiration day|Out of service\*, and images are disabled.|Out of service, but data is retained.|Out of service, but data on cloud disks, local disks, or shared block storage devices is retained.| For an instance of the Classic network type: If an Internet IP address is assigned, it is retained.

 For a VPC-Connected ECS instance: If an Internet IP address is assigned, it is retained. If an EIP address is bound, it is retained.

 |Retained.|
    |15 days after expiration|Released automatically|Released along with the instance, and data cannot be recovered.| By default, cloud disks are released along with the instance and data on them cannot be recovered. If you have set the cloud disks not to be released along with the instance, the disks stop working.

 Local disks are released along with the instance and data on them cannot be recovered.

 Shared block storage is detached automatically from the instance.

 | For an instance of the Classic network type: If an Internet IP address is assigned, it is released.

 For a VPC-Connected ECS instance: If an Internet IP address is assigned, it is retained. If an EIP address is bound, it is unbound from the instance.

 |Automatic snapshots are automatically deleted, but those manually created are retained. Manual snapshots are not affected.|

    \* When an instance is **Out of service**, you cannot connect to it, the website deployed on the instance cannot be accessed, and your business operations may be affected.

    **Note:** You cannot enable the auto-renewal feature for an instance after it expires.

-   **Auto-renewal enabled**

    If auto-renewal is enabled for an instance, but it fails to be renewed in the specified period, the status changes of the related resources are shown in the following table.

    |Period| ECS instances and images|System disks|Data disks|Internet IP addresses|Snapshots|
    |:-----|:------------------------|:-----------|:---------|:--------------------|:--------|
    |Within 15 days of expiration|Running properly\*.|Running properly.|Running properly.|Retained.|Retained.|
    |15 days after expiration|The instance goes out of service\*\* at any time within the 24 hours from 00:00:00 on the 15th day after expiration to 00:00:00 the next day.|Out of service, but data is retained.|Out of service, but data is retained.| For an instance of the Classic network type: If an Internet IP address is assigned, it is released.

 For a VPC-Connected ECS instance: If an Internet IP address is assigned, it is retained. If an EIP address is bound, it is retained.

 |Retained.|
    |30 days after expiration|Automatically released.|Released along with the instance, and data cannot be recovered.| By default, the cloud disks are released along with the instance. If you set them not to be released along with the instance, they stop working.

 Local disks are released along with the instance.

 Shared block storage is automatically detached.

 | For an instance of the Classic network type: If an Internet IP address is assigned, it is released.

 For a VPC-Connected ECS instance: If an Internet IP address is assigned, it is released. If an EIP address is bound, it is unbound from the instance.

 |Automatic snapshots are automatically deleted, but those that are manually created are retained.|

    \* **Running properly** means you can start and stop the instance properly and connect to the instance by using the **Management Terminal** in the console or other remote connection methods.

    \*\* When an instance is **Out of service**, you cannot connect to it, the website deployed on the instance cannot be accessed, and your business operations may be affected.


