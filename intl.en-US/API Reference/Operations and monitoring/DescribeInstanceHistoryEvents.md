# DescribeInstanceHistoryEvents {#DescribeInstanceHistoryEvents .reference}

Describes the history events of a specified instance. You can query the system events history within the last week.

## Request parameters {#RequestParameter .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: DescribeInstanceHistoryEvents.|
|RegionId|String|Yes|ID of the region where the instance is located. For more information, call [DescribeRegions](intl.en-US/API Reference/Regions/DescribeRegions.md#) to obtain the latest region list.|
|InstanceId|String|No|Instance ID. If you do not specify an instance ID, you will obtain event information for all instances in the specified region.|
|EventId.N|String|No|One or more event ID. Value range of N: \[1, 100\], the IDs must be displayed in the similar format of `EventId. 1="e-xhskHun1256xxxx"`, `EventId. 2="e-xhskHun1257xxxx"` ...|
|InstanceEventCycleStatus.N|String|No|Lifecycle status of one or more events. Value range of N: \[1, 100\], the status must be displayed in the similar format of  `InstanceEventCycleStatus. 1="Scheduled"`, `InstanceEventCycleStatus. 2="Canceled"`... Optional values:-   Scheduled: The event is waiting for processing.
-   Avoided: You have fixed the event before it is complete.
-   Executing: The event is in processing.
-   Executed: Event progress is complete.
-   Canceled: The event is canceled.
-   Failed: Event progress failed.

|
|EventCycleStatus|String|No|Lifecycle status of an event. `EventCycleStatus` is effective only when the `InstanceEventCycleStatus.N` is not specified. Optional values:-   Scheduled
-   Avoided
-   Executing
-   Executed
-   Canceled
-   Failed

|
|InstanceEventType.N|String|No|One or more instance event types. Value range of N: \[1, 30\], the events must be displayed in the similar format of  `InstanceEventType. 1="Reboot"`, `InstanceEventType. 2="SystemFailure.Reboot"`... Optional values:-   SystemMaintenance.Reboot: The instance restarts because of maintenance.
-   SystemFailure.Reboot: The instance restarts due to a system failure.
-   InstanceFailure.Reboot: The instance restarts due to instance failure.

|
|EventType|String|No|Instance event type. `EventType` is effective only when the  `InstanceEventType.N` is not specified. Optional values:-   SystemMaintenance.Reboot
-   SystemFailure.Reboot
-   InstanceFailure.Reboot

|
|NotBefore.Start|String|No|Queries the start time of the scheduled event execution time. The time format follows the [ISO8601](intl.en-US/API Reference/Appendix/ISO 8601 Time Format.md#) standard, and the UTC time is used. The format is YYYY-MM-DDTHH:mm:ssZ.|
|NotBefore.End|String|No|Queries the end time of the scheduled event execution time. The time format follows the ISO8601 standard, and the UTC time is used. The format is YYYY-MM-DDTHH:mm:ssZ.|
|EventPublishTime.Start|String|No|Queries the start time of the event release time. The time format follows the ISO8601 standard, and the UTC time is used. The format is YYYY-MM-DDTHH:mm:ssZ.|
|EventPublishTime.End|String|No|The end time of the query event release time. The time format follows the ISO8601 standard, and the UTC time is used. The format is YYYY-MM-DDTHH:mm:ssZ.|
|PageNumber|Integer|No|Page number of the query result. The value must be a positive integer.Default value: 1.

|
|PageSize|Integer|No|Page size of the query result. Value range: \[1, 100\].Default value: 10.

|

## Response parameters {#ResponseParameter .section}

|Name|Type|Description|
|:---|:---|:----------|
|TotalCount|Integer|Total number of the status of the instance.|
|PageNumber|Integer|Page number of the instance list.|
|PageSize|Integer|Number of entries per page set during input.|
|InstanceSystemEventSet|Array of [InstanceSystemEventType](#InstanceSystemEventType)|Array of the history events of the instance.|

**InstanceSystemEventType** 

|Name|Type|Description|
|:---|:---|:----------|
|InstanceId|String|Instance ID.|
|EventId|String|Event ID.|
|EventType.Code|Integer|Event type code.|
|EventType.Name|String|Event type name.|
|EventCycleStatus.Code|Integer|Event status code.|
|EventCycleStatus.Name|String|Event status name.|
|EventPublishTime|String|Event release time. The time format follows the ISO8601 standard, and the UTC time is used. The format is YYYY-MM-DDTHH:mm:ssZ.|
|NotBefore|String|Scheduled time of event execution. The time format follows the ISO8601 standard, and the UTC time is used. The format is YYYY-MM-DDTHH:mm:ssZ.|
|EventFinishTime|String|Event execution time. The time format follows the ISO8601 standard, and the UTC time is used. The format is YYYY-MM-DDTHH:mm:ssZ.|

## Examples { .section}

**Request examples** 

```
https://ecs.aliyuncs.com/?Action=DescribeInstanceHistoryEvents
&RegionId=cn-hangzhou
&InstanceId=i-2ze3tphuqvc93cixxxx3
&<Common Request Parameters>
```

**Success response example** 

**XML format**

```
<DescribeInstanceHistoryEventsResponse>
    <InstanceSystemEventSet>
        <InstanceSystemEventType>
            <InstanceId>i-2ze3tphuqvc93cixxxx3</InstanceId>
            <EventId>e-2ze9yxxxxwtqcvai68rl</EventId>
            <EventType>
                <Code>1</Code>
                <Name>SystemMaintenance.Reboot</Name>
            </EventType>
            <EventCycleStatus>
                <Code>0</Code>
                <Name>Executed</Name>
            </EventCycleStatus>
            <EventPublishTime>2017-11-30T06:32:31Z</EventPublishTime>
            <NotBefore>2017-12-01T06:32:31Z</NotBefore>
            <EventFinishTime>2017-12-01T06:35:31Z</EventFinishTime>
        </InstanceSystemEventType>
        <InstanceSystemEventType>
            <InstanceId>i-2ze3tphuqvc93cixxxx3</InstanceId>
            <EventId>e-2ze9yxxxxwtqcvai68r3</EventId>
            <EventType>
                <Code>34</Code>
                <Name>InstanceExpiration.Stop</Name>
            </EventType>
            <EventCycleStatus>
                <Code>8</Code>
                <Name>Avoided</Name>
            </EventCycleStatus>
            <EventPublishTime>2017-11-29T06:32:31Z</EventPublishTime>
            <NotBefore>2017-12-06T00:00:00Z</NotBefore>
            <EventFinishTime>2017-12-05T12:35:31Z</EventFinishTime>
        </InstanceSystemEventType>
    </InstanceSystemEventSet>
    <PageSize>10</PageSize>
    <PageNumber>1</PageNumber>
    <TotalCount>2</TotalCount>
    <RequestId>02EA76D3-5A2A-44EB-XXXX-8901881D8707</RequestId>
</DescribeInstanceHistoryEventsResponse>
```

 **JSON format** 

```
{
  "InstanceSystemEventSet": {
    "InstanceSystemEventType": [
      {
        "InstanceId": "i-2ze3tphuqvc93cixxxx3",
        "EventId": "e-2ze9yxxxxwtqcvai68rl",
        "EventType": {
          "Code": 1,
          "Name": "SystemMaintenance.Reboot"
        },
        "EventCycleStatus": {
          "Code": 0,
          "Name": "Executed"
        },
        "EventPublishTime": "2017-11-30T06:32:31Z",
        "NotBefore": "2017-12-01T06:32:31Z",
        "EventFinishTime": "2017-12-01T06:35:31Z"
      },
      {
        "InstanceId": "i-2ze3tphuqvc93cixxxx3",
        "EventId": "e-2ze9yxxxxwtqcvai68r3",
        "EventType": {
          "Code": 34,
          "Name": "InstanceExpiration.Stop"
        },
        "EventCycleStatus": {
          "Code": 8,
          "Name": "Avoided"
        },
        "EventPublishTime": "2017-11-29T06:32:31Z",
        "NotBefore": "2017-12-06T00:00:00Z",
        "EventFinishTime": "2017-12-05T12:35:31Z"
      }
    ]
  },
  "PageSize": 10,
  "PageNumber": 1,
  "TotalCount": 2,
  "RequestId": "02EA76D3-5A2A-44EB-XXXX-8901881D8707"
}
```

**Error response example** 

**XML format**

```
<Error>
    <RequestId>C38E0D94-C18B-44F3-8C05-6E35BE334087</RequestId>
    <HostId>ecs.aliyuncs.com</HostId>
    <Code> invalidparameter</code>
    <Message>The Parameter "EventCycleStatus" provided is not valid.</Message>
</Error>
```

 **JSON format** 

```
{
    "RequestId": "1A8B4B27-8B2D-XXXX-XXXX-0F64DBE4C212",
    "HostId": "ecs.aliyuncs.com"
    "Code": "InvalidParameter"
    "Message": "The Parameter "EventCycleStatus" provided is not valid."
}
```

## Error codes {#ErrorCode .section}

The following error codes are restricted to this interface. For more error codes, see [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

|Error code|Error message|HTTP status code|Meaning|
|:---------|:------------|:---------------|:------|
|InvalidParameter|The Parameter provided is not valid.|403|The specified parameter is invalid.|
|EventIdLimitExceeded|The amount of EventId specified exceeds limit 100.|403|The number of `EventId` cannot exceed 100.|
|MissingParameter|The input parameter that is mandatory for processing this request is not supplied.|403|You must specify the required parameter.|
|InternalError|The request processing has failed due to some unknown error, exception or failure.|500|Internal error. Please try again later.|

