# Query and subscribe to system events {#SystemMaintenance.PerformanceImpact .concept}

This topic describes how to query and subscribe to system events that occur when the performance of an instance is impacted. By subscribing to system events, you can quickly assess the running status of the instance and determine whether your services will be impacted.

## Background information {#Introduction .section}

System events are events that affect the running status of an ECS instance. They can be scheduled events, such as a system update or system maintenance, or unexpected events, such as an instance failure. For more information, see [System events](../../../../../reseller.en-US/User Guide/Monitoring/System events.md#).

The following procedure uses CloudMonitor to describe how to query and subscribe to system events that impact instance performance \(using `SystemMaintenance.PerformanceImpact`\). These events have the following two lifecycle states:

-   `Executing`: The events have started and are in progress.
-   `Executed`: The events have ended.

## View system events through CloudMonitor {#QueryCloudMonitor .section}

1.  Log on to the [CloudMonitor console](https://cloudmonitor.console.aliyun.com/).
2.  In the left-side navigation pane, click **Event Monitoring**.
3.  On the **Query Event** tab page, choose **System Event** \> **ECS** \> **All Events**, or select **PerformanceImpact Executing \(System Maintenance\)** or **PerformanceImpact Executed \(System Maintenance\)** from **All Events**. System events that are about to occur or have occurred are displayed.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21669/155055594538788_en-US.png)


## Add an alarm contact {#AddContact .section}

If you have already set an alarm contact, you can skip the following steps.

1.  Log on to the [CloudMonitor console](https://cloudmonitor.console.aliyun.com/).
2.  In the left-side navigation pane, choose **Alarms** \> **Alarm Contacts**.
3.  Click **Create Alarm Contact**, and then set the alarm contact information.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21669/155055594538789_en-US.png)

    **Note:** For information on how to add a **DingTalk chatbot**, see [Receive alarm notifications in a DingTalk group](../../../../../reseller.en-US/Best Practices/Receive alarm notifications in a DingTalk group.md#).


## Subscribe to event notifications through CloudMonitor {#SucscribeCloudMonitor .section}

1.  Log on to the [CloudMonitor console](https://cloudmonitor.console.aliyun.com/).
2.  In the left-side navigation pane, click **Event Monitoring**.
3.  On the **Alarm Rules** tab, select **System Event** \> **Create Event Alerts**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21669/155055594512397_en-US.png)

4.  On the Create/Modify Event Alerts page, set the alarm notification, and then click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21669/155055594538792_en-US.png)


## Query system events through an API {#APIQuery .section}

If you have multiple ECS instances, we recommend that you use APIs to automate the querying and handling of system events. This example uses the API [DescribeInstanceHistoryEvents](../../../../../reseller.en-US/API Reference/System event/DescribeInstanceHistoryEvents.md#) as an example. You can query system events and historical events of the past seven days through OpenAPI Explorer.

1.  Log on to the [OpenAPI Explorer console](https://api.aliyun.com/).
2.  In the left-side navigation pane, click **Elastic Compute Service**, and then enter DescribeInstanceHistoryEvents in the search box.
3.  Set the request parameters, and then click **Submit Request**.

    -   **Request parameters**: RegionId, InstanceId, and EventId.N.
    -   **Response parameters**: InstanceId, EventId, EventType \(`SystemMaintenance.PerformanceImpact`\), EventCycle, PublishTime \(the time in UTC when the event is initially released\), NotBeforeTime \(the time in UTC when the event is executed\), and FinishTime \(the time in UTC when the event is ended\).
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21669/155055594538795_en-US.png)


