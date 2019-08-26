# System events {#concept_gdc_tyz_xdb .concept}

System events are scheduled or unexpected events that affect the running status of an ECS instance. Specifically, system events refer to events that involve restarting, stopping, or releasing ECS ​​instances due to such actions as system update, system maintenance, an illegal operation, system failure, hardware/software failure, an expiring Subscription instance, or an overdue payment.

## Overview {#section_mnp_5yz_xdb .section}

After you purchase your required ECS instances, complete their initial configurations, and deploy your services, maintaining the health of your ECS instances is crucial to the running of your services. To guarantee system performance and the security of your assets, ECS regularly reviews the health of the physical servers where your ECS instances reside. If ECS detects any hardware/software faults or potential risks on the physical servers, your instances will be migrated to healthy servers in real time. During such maintenance tasks, your instances will not be affected and you will not receive any notifications.

If a system event occurs, ECS will send you a notification, information about the recommended handling actions, and the time at which ECS is scheduled to perform these actions. For scheduled system events, ECS will send a notification to you that includes information such as the impact of the system event on your instances and the expected execution time. To prevent any detrimental impacts to your services, we recommend that you back up your data and redistribute inbound traffic before handling system events. After a system event is handled, you can query the historical system events of the past seven days for further analysis and review.

## Limits {#section_nnp_5yz_xdb .section}

Phased-out instance type families, such as sn1, sn2, t1, s1, s2, s3, m1, m2, c1, c2, c4, ce4, cm4, n1, n2, and e3, do not support system events. For more information, see [Instance type families](../reseller.en-US/Product Introduction/Instance type families.md#).

## System event types {#section_onp_5yz_xdb .section}

The following table describes the types of ECS system events.

|Category|Event type|Parameter|
|:-------|:---------|:--------|
|Scheduled restart|An instance is restarted after a scheduled system maintenance.|`SystemMaintenance.Reboot`|
|Unexpected restart|An instance is restarted after an unexpected system failure.|`SystemFailure.Reboot`|
|An instance is restarted after an unexpected instance failure.|`InstanceFailure.Reboot`|
|Instance stop|A Subscription instance is stopped due to expiration.|`InstanceExpiration.Stop`|
|A Pay-As-You-Go instance is stopped due to overdue payment.|`AccountUnbalanced.Stop`|
|Instance release|A Subscription instance is released after expiration.|`InstanceExpiration.Delete`|
|A Pay-As-You-Go instance is released due to overdue payment.|`AccountUnbalanced.Delete`|

## Event statuses {#section_snp_5yz_xdb .section}

The following table describes the statuses of a system event during its lifecycle.

|Status|Status attribute|Description|
|:-----|:---------------|:----------|
|Scheduled|Transitory status|The system event has been scheduled but not performed.|
|Avoided|Stable status|You have performed the recommended actions in advance within the [user operation period](#).|
|Executing|Transitory state|The system event is being executed.|
|Executed|Stable status|The system event has been executed.|
|Canceled|Stable status|ECS has canceled the scheduled system event.|
|Failed|Stable status|The system event failed.|

## System event periods {#section_xnp_5yz_xdb .section}

System events observe the following two periods:

-   **User operation period**: The period between the time when a system event is initiated and the time when the system event starts to be executed. For maintenance-related system events, the period is between 24 and 48 hours. For Subscription instances that are about to be stopped due to expiration, the period is 3 days. For Pay-As-You-Go instances that are about to be stopped due to overdue payment, the period is less than 1 hour. Instances in which a system event occurs due to billing issues will be immediately stopped, and will be released 15 days later if the issue is not resolved.

    During this period, you can use the recommended methods to handle system events in advance, or wait until the default actions are executed. If ECS fixes a system failure and triggers a system event, ECS will send you an event notification in advance based on the system maintenance schedule.

-   **System action period**: If you do not handle a system event in advance, the system event will be automatically fixed within 6 hours after the system action period begins at a scheduled time. After that, you will receive a system event report.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9748/15508037013942_en-US.png)

    **Note:** Only scheduled system events have a user operation period. Unexpected system events that are caused by emergency failures or invalid operations do not have a user operation period. If an unexpected system event occurs, you will receive a notification, but you cannot take any actions. You can only query the historical system events for fault diagnosis and data recovery.


## View system events {#SystemAlert .section}

**Procedure \(through the console\)**

If a system event is scheduled, the **Unsettled Events** button in the ECS console will display a notification badge with the current number of unsettled events.

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Overview**.
3.  In the **Common Operation** area, click **Unsettled Events**.
4.  Click the **Scheduled system event** button. A list of instance IDs, regions, statuses, event types, and recommended actions is displayed on the page. Alternatively, you can choose recommended actions from the **Actions** column to handle system events.

**Procedure \(through an API\)**

In this example, Alibaba Cloud CLI is used as the tool to call the API. For more information, see [Quick start for ECS APIs](../reseller.en-US/API Reference/Quick start for ECS APIs.md#).

1.  Obtain the instance ID.

    ```
    aliyun ecs DescribeInstances --RegionId <TheRegionId> --output cols=InstanceId,InstanceName
    ```

2.  Call [DescribeInstancesFullStatus](../reseller.en-US/API Reference/System event/DescribeInstancesFullStatus.md) to view the system events of the instance.

    ```
    aliyun ecs DescribeInstancesFullStatus --RegionId <TheRegionId> --InstanceId.1 <YourInstanceId> --output cols=EventId,EventTypeName
    ```


**Procedure \(through instance metadata\)**

For more information, see [Metadata](reseller.en-US/User Guide/Instances/User-defined data and metadata/Metadata.md#).

## View historical system events {#SystemAlertHistory .section}

You can query the historical system events of the past seven days for fault diagnosis and review.

**Procedure \(through the console\)**

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  On the left-side navigation pane, click **Overview**.
3.  In the **Common Operation** area, click **Unsettled Events**.
4.  In the left-side navigation pane, click **All events**, and then choose **Scheduled system events** \> **Instances**. A list of instance IDs, event types, and task statuses is displayed.

**Procedure \(through an API\)**

1.  Obtain the instance ID.

    ```
    aliyun ecs DescribeInstances --RegionId <TheRegionId> --output cols=InstanceId,InstanceName
    ```

2.  Call [DescribeInstanceHistoryEvents](../reseller.en-US/API Reference/System event/DescribeInstanceHistoryEvents.md#) to view the system events of the instance.

    ```
    aliyun ecs DescribeInstanceHistoryEvents --RegionId <TheRegionId> --InstanceId.1 <YourInstanceId> --output cols=EventId,EventTypeName
    ```


## Subscribe to event notifications {#Subscribe .section}

You can set alarm rules for all system events by using CloudMonitor so that you can receive notifications when a system event occurs. For more information, see [Cloud product system event monitoring](../../../../../../reseller.en-US/User Guide/Event monitoring/Cloud product system event monitoring.md#).

## Handling suggestions {#section_e2q_3zz_xdb .section}

You can handle system events by using the ECS console or using the corresponding APIs. You can also optimize instance performance based on system events. The following table describes the recommended actions to help you handle system events as needed.

|Event type|Impact on the instance|Recommended action|
|:---------|:---------------------|:-----------------|
|An instance is restarted due to system maintenance.|The instance will be restarted at the scheduled maintenance time.|Use either of the following methods within the user operation period:-   [Restart the instance](reseller.en-US/User Guide/Instances/Restart an instance.md#) in the ECS console.

-   Call the API [RebootInstance](../reseller.en-US/API Reference/Instances/RebootInstance.md).

**Note:** Restarting instances in the runtime environment cannot handle system events.

-   Redistribute traffic, or remove ECS instances that are scheduled for maintenance from [SLB instances](../../../../../../reseller.en-US/Product Introduction/What is Server Load Balancer?.md#).

To back up your data, we recommend that you [create a snapshot](reseller.en-US/User Guide/Snapshots/Create a snapshot.md#) \([CreateSnapshot](../reseller.en-US/API Reference/Snapshots/CreateSnapshot.md)\) for the disk where your instance is mounted.|
|An instance is restarted due to an unexpected system failure.|The instance will be restarted if an unexpected host failure occurs.|When you receive the event notification, your instance is being restarted or has been restarted. We recommend that you:-   Verify that the instance and applications are restored.
-   [Subscribe to event notifications](reseller.en-US/User Guide/Monitoring/System events.md#) through SMS or MNS to dynamically switch over the traffic to balance the load and replace the faulty instance.

|
|An instance is restarted due to an unexpected instance error.|The instance will be restarted if the OS fails.|When you receive the event notification, your instance is being restarted or has been restarted. We recommend that you:-   Check the [Console output and screenshot](reseller.en-US/User Guide/Monitoring/Console output and screenshot.md#) to determine the cause of OS failure.

-   Verify that the instance and applications are restored.


|
|A Subscription instance is stopped due to expiration.|The Subscription instance resources will be stopped.|[Renew the instance](../reseller.en-US/Pricing/Renew instances/Renewal overview.md#) or wait for the instance to be stopped.|
|A Pay-As-You-Go instance is stopped due to overdue payment.|The Pay-As-You-Go instance resources will be stopped.| Add funds to your account or wait for the instance to be stopped.

 |
|A Subscription instance is released due to expiration.|The Subscription instance resources will be released.|[Renew the instance](../reseller.en-US/Pricing/Renew instances/Renewal overview.md#) or wait for the instance to be released.|
|A Pay-As-You-Go instance is released due to overdue payment.|The Pay-As-You-Go instance resources will be released.| Add funds to your account or wait for the instance to be released.

 |

