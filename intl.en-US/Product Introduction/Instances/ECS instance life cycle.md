# ECS instance life cycle {#concept_zg1_gv2_5db .concept}

The life cycle of an ECS instance begins when the instance is created and ends when the instance is released.

## Instance status {#section_p4f_dk5_ydb .section}

During its life cycle, an ECS instance may undergo several status changes, as described in the following table.

|Status|Status attribute|Description|API status|Visible in the console?|
|:-----|:---------------|:----------|:---------|:----------------------|
|Preparing|Intermediate|After an instance is created, it is in this status before it enters the **Running** status. If the instance is in this status for a long time, it means that an exception has occurred.|Pending|No|
|Starting|Intermediate|After an instance is started or restarted in the console or through an API, the instance is in this status before it enters the **Running** status. If the instance is in this status for a long time, it means that an exception has occurred.|Starting|Yes|
|Running|Stable|The instance is operating normally, and you can run your services.|Running|Yes|
|Expiring|Stable|A Subscription instance is in this status for 15 days before it expires. We recommend that you [Renew the instance](../../../../../reseller.en-US/Pricing/Renew instances/Renewal overview.md#).|Running|Yes|
|Stopping|Intermediate|After an instance is stopped in the console or through an API, the instance is in this status before it enters the **Stopped** status. If the instance is in this status for a long time, it means that an exception has occurred.|Stopping|Yes|
|Stopped|Stable|An instance is in this status after it has been created but has not been started yet, or when it has been stopped due to normal operations. An instance in this status cannot provide external services.|Stopped|Yes|
|Expired|Stable|A Subscription instance enters the **Expired** status when it expires. A Pay-As-You-Go instance enters this status if you have an overdue payment under your account. An instance in this status cannot provide external services. For information about resource status changes, see [Subscription](../../../../../reseller.en-US/Pricing/Subscription.md#) and [Pay-As-You-Go](../../../../../reseller.en-US/Pricing/Pay-As-You-Go.md#).|Stopped|Yes|
|Expired and Being Recycled|Stable|Within 15 days after a VPC Subscription instance expires or is stopped due to an overdue payment, the instance stays in the **Expired** status for a period of time, and then enters the **Expired and Being Recycled** status.-   You can renew the instance before it enters the **Expired and Being Recycled** status. If the renewal is successful, all resources will be retained without being affected.
-   After the instance enters the **Expired and Being Recycled** status, its computing resources \(vCPU + Memory\) will no longer be retained, but its cloud disks, local disks, and assigned Internet IP address will be retained. You can renew the instance. If the renewal is successful, the block storage \(including the local disks\) and the assigned Internet IP address will remain the same.

| | |
|Overdue and Being Recycled|Stable|Within 15 days after a VPC Pay-As-You-Go instance expires or is stopped due to an overdue payment, the instance stays in the **Expired** status for a period of time, and then enters the **Overdue and Being Recycled** status.-   You can add funds to your account and [Restart](../../../../../reseller.en-US/User Guide/Instances/Reactivate an instance.md#) the instance before the instance enters the **Overdue and Being Recycled** status. If the restart is successful, all resources will be retained without being affected.
-   After the instance enters the **Expired and Being Recycled** status, its computing resources \(vCPU + Memory\) will no longer be retained, but its cloud disks, local disks, and assigned Internet IP address will be retained. You can add funds to your account and restart the instance. If the instance fails to be restarted, try again later or open a ticket. When you restart the instance successfully, the block storage \(including local disks\) and the assigned Internet IP address of the instance are retained.

|Stopped|Yes|
|Locked|Stable|An instance is in this status if you have an overdue payment under your account or you account is insecure. You can open a ticket to unlock the instance.|Stopped|Yes|
|Release pending|Stable| A Subscription instance is in this status after you apply for a refund before the instance expires.

 |Stopped|Yes|

## API status {#section_apf_dk5_ydb .section}

You can call [Describeinstancestatus](../../../../../reseller.en-US/API Reference/Instances/DescribeInstanceStatus.md#) or [Description instances](../../../../../reseller.en-US/API Reference/Instances/DescribeInstances.md#) to view the API status of an instance. The following figure shows the status conversions described in this topic.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9551/15477071785105_en-US.png)

