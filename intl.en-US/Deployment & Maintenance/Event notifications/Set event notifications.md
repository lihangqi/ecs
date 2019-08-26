# Set event notifications {#concept_188655 .concept}

This topic describes how to set notifications for Elastic Compute Service \(ECS\) system events by using CloudMonitor.

## Benefits {#section_f3t_fxo_by8 .section}

CloudMonitor supports a wide range of cloud service events. For more information, see [Cloud service events](../../../../reseller.en-US/User Guide/Event monitoring/Cloud product events/Cloud service events.md#).

ECS system events include O&M events, fault detection, instance status changes, and configuration changes. For more information, see [System events](reseller.en-US/Deployment & Maintenance/System events/System events.md#).

You can subscribe to one or more specific events to receive the corresponding event notifications. Based on the notifications, you can review the resource changes and determine the appropriate next steps to ensure your services run normally.

You can also configure message-oriented middleware to automate O&M and call API actions and SDKs.

## Procedure {#section_cfg_mh1_36k .section}

After your ECS instance reports events to CloudMonitor, you can set event notifications by completing the following steps on the CloudMonitor console:

1.  Log on to the [CloudMonitor console](https://partners-intl.console.aliyun.com/#/cloudmonitor).
2.  In the left-side navigation pane, click **Event Monitoring**.
3.  On the **Event Monitoring** page, click the **Alarm Rules** tab.
4.  On the **Alarm Rules** tab page, click the **System Event** tab, and then click **Create Event Alerts**.
5.  In the Create / Modify Event Alerts dialog box, set parameters as follows:

    -   Set event filter criteria.
        -   **Event Type**: Select **System Event**.
        -   **Product Type**: Select **ECS**.
        -   **Event Level**: Select one or more levels of event severity to which you want to subscribe. Values: CRITICAL | WARN | INFO.
        -   **Event Name**: Select the names of the events to which you want to subscribe. For more information, see [Overview of event notifications](reseller.en-US/Deployment & Maintenance/Event notifications/Overview of event notifications.md#).

            **Note:** We recommend that you do not select **All Events**. Instead, we recommend that you create different levels of event notifications based on the impacts of events on services.

        -   **Resource Range**: When you select **All Resources**, notifications are sent for all resource-related events.
    -   Set the notification method and message-oriented middleware.
        -   **Notification Method** 

            We recommend that you select email as the method for receiving notifications. We also recommend that you do not select INFO as a security level for which to receive notifications to reduce the number of notifications sent to your account.

        -   Message-oriented middleware

            You can enable **MNS queue**, **Function service** \(Function Compute\), **URL callback**, or **Log service** as the message-oriented middleware so that the system handles events automatically.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/162637/155929555745532_en-US.png)

6.  Click **OK**.

## Result {#section_dl0_n4m_7e6 .section}

After you set event notifications, the configured ECS instance sends notifications by using the specified method once events are detected. The following is a default notification in JSON format that is sent when the system detects a change regarding the status of your ECS instance:

``` {#codeblock_xnl_uzs_890}
{
    "eventTime": "20181226T220114.058+0800",
    "id": "9435EAD6-3CF6-4494-8F7A-3A********77",
    "level": "INFO",
    "name": "Instance:StateChange",
    "product": "ECS",
    "regionId": "cn-hangzhou",
    "resourceId": "acs:ecs:cn-hangzhou:169070********30:instance/i-bp1ecr********5go2go",
    "userId": "169070********30",
    "ver": "1.0",
    "content": {
        "resourceId": "i-bp1ecr********5go2go",
        "resourceType": "ALIYUN::ECS::Instance",
        "state": "Stopping"
    }
}
```

This notification contains the following top-level fields:

-   `id`: the ID of the event.
-   `eventTime`: the time when the event occurred. The valid time format is UTC+8.
-   `level`: the level of the event. Values: INFO | WARN | CRITICAL.
-   `name`: the name of the event. For more information, see [Overview of event notifications](reseller.en-US/Deployment & Maintenance/Event notifications/Overview of event notifications.md#).
-   `product`: the name of the involved product. Value: ECS.
-   `regionId`: the ID of the involved region. For more information, see [Regions and zones](../../../../reseller.en-US/General Reference/Regions and zones.md#).
-   `resourceId`: the Aliyun Resource Name \(ARN\) of the involved resource.
-   `userId`: the ID of your account.
-   `content`: the details about the event. For more information, see [Overview of event notifications](reseller.en-US/Deployment & Maintenance/Event notifications/Overview of event notifications.md#).

