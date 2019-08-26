# Automatic recovery of instances {#concept_nr2_2ly_pgb .concept}

This topic describes how automatic recovery and failover functions of Alibaba Cloud ECS instances.

## Background information {#section_sp1_dlc_wgb .section}

The automatic recovery and failover functions are triggered by a [system event](intl.en-US/Deployment & Maintenance/System events/System events.md#) whose code is SystemFailure.Reboot. If an irreparable failure occurs to the underlying hardware on which your instances are hosted, these instances automatically restart and the corresponding [metadata](../intl.en-US/Instances/Manage instances/User-defined data and metadata/Metadata.md#) \(including the instance ID and the private and public IP addresses\) remain unchanged after the restart. The following table compares different types of system events and what troubleshooting actions are supported.

|System event type|Can the system event schedule be queried?|Can I manually intervene?|
|:----------------|:----------------------------------------|:------------------------|
|Automatic recovery|No|No|
|Non-critical failure system events|Yes|Yes|

## Limits {#section_y2w_dlc_wgb .section}

-   You cannot restart an instance when automatic recovery is in progress.
-   Instances with local disks can automatically restart and recover from an unexpected instance host failure, and data in the local disks can be retained, only if the host can restart and recover. Otherwise, these instances are deployed to another healthy host for continuous availability, and data in the local disks are cleared. If a system event occurs to your local disk, you can [open a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) to check the status of the data disk.

## View instance automatic recovery events {#section_u5q_2lc_wgb .section}

The following example uses the Alibaba Cloud CLI to call [DescribeInstanceHistoryEvents](../intl.en-US/API Reference/System event/DescribeInstanceHistoryEvents.md#) to check whether an instance has active or historical system events. For more information, see [Quick start for ECS APIs](../intl.en-US/API Reference/Quick start for ECS APIs.md#).

``` {#codeblock_ghl_yfc_3gh}
aliyun ecs DescribeInstanceHistoryEvents --RegionId TheRegionId --InstanceId YourInstanceId --InstanceEventCycleStatus.1=Executing --InstanceEventCycleStatus.2=Executed --InstanceEventType.1=SystemFailure.Reboot
```

For information about how to view automatic recovery events through the ECS console, see [System events](intl.en-US/Deployment & Maintenance/System events/System events.md#).

## Best practices for increased fault tolerance {#section_qhr_clc_wgb .section}

To increase the fault tolerance of your ECS instances for when the automatic recovery and failover functions are triggered, we recommend that you implement the following actions:

-   Add critical applications \(for example, SAP HANA\) to the startup item list to avoid any service disruptions.
-   Enable the automatic reconnection function for your applications. For example, enable your applications to automatically connect to MySQL, SQL Server, or Apache Tomcat.
-   If you use [Server Load Balancer](../../../../../intl.en-US/Product Introduction/What is Server Load Balancer?.md#), we recommend that you deploy multiple ECS instances in a cluster. In this way, even if one ECS instance is undergoing an automatic recovery, the other ECS instances can continue to provide access to your services.
-   Periodically back up data on the local disks.

