# Use CloudMonitor to monitor ECS instances {#concept_52047_zh .concept}

Many businesses are moving to cloud computing because it is cost-effective, and saves customers of heavy lifting. This can be greatly attributed to the leverage of monitoring. Monitoring service provides real-time operation data for you to identify risks in advance, avoid potential loss, and troubleshoot as quickly as possible.

This article takes a website for example \(the website architecture is shown as follows\) to illustrate how to configure CloudMonitor. The example website uses Alibaba Cloud services such as ECS, RDS, OSS, and Server Load Balancer.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9813/153922821612496_en-US.png)

## Prerequisites {#section_ywm_km1_ffb .section}

Before you begin, you must complete the following operations:

-   Make sure that your ECS monitoring agents are functional to collect metric data. Otherwise, you must install the agent manually. For more information, see [How to install CloudMonitor agent](../../../../reseller.en-US/User Guide/Host monitoring/Install CloudMonitor agent.md).
-   [Add alarm contacts and contact groups](../../../../reseller.en-US/User Guide/Alarm Service/Manage alarm contact and alarm contact group.md). We recommend that you add at least two contacts to make sure real-time responses to monitoring alarms. For more information about metrics, see [Cloud service overview and alarm overview](../../../../reseller.en-US/Product Introduction/Features.md).
-   With CloudMonitor Dashboard, you can gain system-wide visibility into resource utilization and operational health. You can select a metrics dimension. You can choose per-instance metrics dimension if you only have several instances.

    Otherwise, you can choose ECS groups dimension or user dimension, and choose the average value.


## Setting alarm threshold { .section}

We recommend that you set the alarm threshold according to your business status. A much lower threshold may trigger alarm too often and render monitoring meaningless, while a much higher threshold may leave you with no time to respond to a major event.

## Set alarm rules { .section}

Take CPU utilization as an example. We have to reserve some processing capacity to guarantee the normal function, so you can set the threshold to 70% and to trigger an alarm when the threshold is exceeded by three times in a row, as shown in the following figure.

If you have to set alarm rules for other metrics, click **Add Alarm Rule**.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9813/153922821612500_en-US.png)

## Set process monitoring { .section}

For Web applications, you can [add monitoring for process](../../../../reseller.en-US/User Guide/Host monitoring/Process Monitoring.md) . For more information, see [Process monitoring](../../../../reseller.en-US/User Guide/Host monitoring/Process Monitoring.md).

**Set site monitoring**

Site monitoring is at the network access layer to test the availability.

**Set RDS monitoring**

We recommend that you set the RDS CPU utilization alarm threshold to 70% and to trigger an alarm when the threshold is exceeded by three times in a row. You can set the disk utilization , IOPS utilization, total connections and other [metrics](../../../../reseller.en-US/User Guide/Cloud service monitoring/RDS monitoring.md) as needed.

## Set Server Load Balancer monitoring { .section}

Before you begin, make sure that you have enabled health check for your Server Load Balancer instance.

You can use Custom monitoring metrics if the metrics you need are not covered.

