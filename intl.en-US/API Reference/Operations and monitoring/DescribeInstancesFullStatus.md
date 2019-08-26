# DescribeInstancesFullStatus {#DescribeInstancesFullStatus .reference}

Describes the full status information of the specified instance. The full status information includes the instance status and the instance event status, while the instance status is the lifecycle status of the instance and the instance event is the health status of the maintenance event. For more details, see instance lifecycle, and instance system events.

## Description {#section_rcq_354_ydb .section}

After you call the interface, information including the status of the scheduled events \(Scheduled\) and the status of the specified instance is returned.

If a period is specified, all the events in the period are queried.

## Request parameters {#RequestParameter .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: DescribeInstancesFullStatus|
|RegionId|String|Yes|ID of the region where the instance belongs. For more information, see Regions and zones, or call [DescribeRegions](reseller.en-US/API Reference/Regions/DescribeRegions.md#) to obtain the latest region list.|
|InstanceId.N|String|No|Instance ID. Value range of N: \[1, 100\]. For example, `InstanceId. 1="i-instance1", 2="i-instance2"`......|
|EventId.N|String|No|Event ID. Value range of N: \[1, 100\]. For example, `EventId. 1="e-xhskHun1256xxxx"`, `EventId. 2="e-xhskHun1257xxxx"`......|
|Status|String|No|Lifecycle status of the instance. Optional values:-   Starting
-   Running
-   Stopped

|
|HealthStatus|String|No|Health status of the instance. Optional values:-   OK: The instance performance is normal.
-   Impaired: The instance performance is damaged.
-   Warning: The performance of instance may be degraded because of maintenance or technical issues.
-   Maintaining: The instance is in maintenance.
-   Initializing: The instance is in initialization.
-   InsufficientData: The event details cannot be determined because of insufficient data.
-   NotApplicable: Not applicable.

|
|InstanceEventType.N|String|No|One or more instance event types. Value range of N: \[1, 30\], the events must be displayed in the similar format of InstanceEventType.1="Reboot", InstanceEventType.2="SystemFailure.Reboot"... Optional values: SystemMaintenance.Reboot: The instance restarts because of maintenance. SystemFailure.Reboot: The instance restarts due to a system failure. InstanceFailure.Reboot: The instance restarts due to instance failure. `Instanceeventtype. 1="Reboot"`, `InstanceEventType. 2="SystemFailure.Reboot"`...... Scope of value:-   Systemmaintenance. Reboot: reboot due to system maintenance instance
-   Systemfailure. Reboot: restart due to system error instance
-   Maid. Reboot: instance restart due to instance error

|
|EventType|String|No|Instance event type. `EventType` is effective only when the InstanceEventType.N is not specified. Optional values:-   SystemMaintenance.Reboot
-   SystemFailure.Reboot
-   InstanceFailure.Reboot

|
|NotBefore.Start|String|No|Queries the start time of the scheduled event execution time. The time format follows the [ISO8601](../reseller.en-US/API Reference/Appendix/ISO 8601 Time Format.md#) standard, and the UTC time is used. The format is yyyy-MM-ddTHH:mm:ssZ.|
|NotBefore.End|String|No|Queries the end time of the scheduled event execution time. The time format follows the [ISO8601](../reseller.en-US/API Reference/Appendix/ISO 8601 Time Format.md#) standard, and the UTC time is used. The format is yyyy-MM-ddTHH:mm:ssZ.|
|EventPublishTime.Start|String|No|Queries the start time of the event release time. The time format follows the [ISO8601](../reseller.en-US/API Reference/Appendix/ISO 8601 Time Format.md#) standard, and the UTC time is used. The format is yyyy-MM-ddTHH:mm:ssZ.|
|EventPublishTime.End|String|No|Queries the end time of the event release time. The time format follows the [ISO8601](../reseller.en-US/API Reference/Appendix/ISO 8601 Time Format.md#) standard, and the UTC time is used. The format is yyyy-MM-ddTHH:mm:ssZ.|
|PageNumber|Integer|No|Page number of the query result. The value must be a positive integer.Default value: 1.

|
|PageSize|Integer|No|Page size of the query result. Value range: \[1, 100\]Default value: 10.

|

## Response parameters {#ResponseParameter .section}

|Name|Type|Description|
|:---|:---|:----------|
|TotalCount|Integer|Total number of the status of the instance.|
|Pagenumber|Integer|Page number of the status list of the instance.|
|Pagesize|Integer|Size of each page.|
|Instancefullstatusset|Array of [`InstanceFullStatusType`](#)|Array of full instance status.|

**InstanceFullStatusType** 

|Name|Type|Description|
|:---|:---|:----------|
|InstanceId|String|Instance ID.|
|Scheduledsystemeventset|Array of [`ScheduledSystemEventType`](#)|Array of scheduled events.|
|Status. Code|Integer|Code of the instance lifecycle status.|
|Status. Name|String|Name of the instance lifecycle status.|
|Healthstatus. Code|Integer|Code of the health status.|
|Healthstatus. Name|String|Name of the health status.|

**ScheduledSystemEventType** 

|Name|Type|Description|
|:---|:---|:----------|
|EventId|String|Instance event ID.|
|EventCycleStatus.Code|Integer|Code of event status.|
|EventCycleStatus.Name|String|Name of event status.|
|EventType.Code|Integer|Code of event type.|
|EventType.Name|String|Code of event type.|
|Eventpublishtime|String|Event release time. The time format follows the [ISO8601](../reseller.en-US/API Reference/Appendix/ISO 8601 Time Format.md#) standard, and the UTC time is used. The format is yyyy-MM-ddTHH:mm:ssZ.|
|NotBefore|String|Scheduled time of event execution. The time format follows the [ISO8601](../reseller.en-US/API Reference/Appendix/ISO 8601 Time Format.md#) standard, and the UTC time is used. The format is yyyy-MM-ddTHH:mm:ssZ.|

## Examples { .section}

**Request example** 

```
https://ecs.aliyuncs.com/?Action=DescribeInstancesFullStatus
&RegionId=cn-hangzhou
&<Common Request Parameters>
```

**Success response example** 

**XML format**

```
<DescribeInstancesFullStatusResponse>
    <? xml version="1.0" encoding="UTF-8" ? >
    <InstanceFullStatusSet>
        <InstanceFullStatusType>
            <InstanceId>i-instance1</InstanceId>
            <Status>
                <Code>1</Code>
                <Name>Running</Name>
            </Status>
            <HealthStatus>
                <Code>0</Code>
                Group1
            </HealthStatus>
            <ScheduledSystemEventSet>
                <ScheduledSystemEventType>
                    <EventId>e-event1</EventId>
                    <EventCycleStatus>
                        <Code>24</Code>
                        <Name>Scheduled</Name>
                    </EventCycleStatus>
                    <EventType>
                        <Code>1</Code>
                        <Name>SystemMaintenance.Reboot</Name>
                    </EventType>
                    <EventPublishTime>2017-11-30T06:32:31Z</EventPublishTime>
                    <NotBefore>2017-12-01T06:32:31Z</NotBefore>
                </ScheduledSystemEventType>
                <ScheduledSystemEventType>
                    <EventId>e-event2</EventId>
                    <EventCycleStatus>
                        <Code>24</Code>
                        <Name>Scheduled</Name>
                    </EventCycleStatus>
                    <EventType>
                        <Code>34</Code>
                        <Name>InstanceExpiration.Stop</Name>
                    </EventType>
                    <EventPublishTime>2017-11-30T00:00:00Z</EventPublishTime>
                    <NotBefore>2017-12-07T00:00:00Z</NotBefore>
                </ScheduledSystemEventType>
            </ScheduledSystemEventSet>
        </InstanceFullStatusType>
        <InstanceFullStatusType>
            <InstanceId>i-instance2</InstanceId>
            <Status>
                <Code>1</Code>
                <Name>Running</Name>
            </Status>
            <HealthStatus>
                <Code>64</Code>
                <Name>Warning</Name>
            </HealthStatus>
            <ScheduledSystemEventSet>
                <ScheduledSystemEventType>
                    <EventId>e-event3</EventId>
                    <EventCycleStatus>
                        <Code>24</Code>
                        <Name>Scheduled</Name>
                    </EventCycleStatus>
                    <EventType>
                        <Code>65</Code>
                        <Name>SystemFailure.Reboot</Name>
                    </EventType>
                    <EventPublishTime>2017-11-30T06:32:31Z</EventPublishTime>
                    <NotBefore>2017-12-01T06:32:31Z</NotBefore>
                </ScheduledSystemEventType>
            </ScheduledSystemEventSet>
        </InstanceFullStatusType>
    </InstanceFullStatusSet>
    <PageSize>10</PageSize>
    <PageNumber>1</PageNumber>
    <TotalCount>2</TotalCount>
    <RequestId>AAC49D3E-ED6F-4F00-XXXX-377C551B1DD4</RequestId>
</DescribeInstancesFullStatusResponse>
```

 **JSON format** 

```
{
  "InstanceFullStatusSet": {
    "InstanceFullStatusType": [
      {
        "InstanceId": "i-instance1",
        "Status": {
          "Code": 1,
          "Name": "Running"
        },
        "HealthStatus": {
          "Code": 0,
          "Name": "Ok"
        },
        "ScheduledSystemEventSet": {
          "ScheduledSystemEventType": [
            {
              "EventId": "e-event1",
              "EventCycleStatus": {
                "Code": 24,
                "Name": "Scheduled"
              },
              "EventType": {
                "Code": 1,
                "Name": "SystemMaintenance.Reboot"
              },
              "EventPublishTime": "2017-11-30T06:32:31Z",
              "NotBefore": "2017-12-01T06:32:31Z"
            },
            {
              "EventId": "e-event2",
              "EventCycleStatus": {
                "Code": 24,
                "Name": "Scheduled"
              },
              "EventType": {
                "Code": 34,
                "Name": "InstanceExpiration.Stop"
              },
              "EventPublishTime": "2017-11-30T00:00:00Z",
              "NotBefore": "2017-12-07T00:00:00Z"
            }
          ]
        }
      },
      {
        "InstanceId": "i-instance2",
        "Status": {
          "Code": 1,
          "Name": "Running"
        },
        "HealthStatus": {
          "Code": 64,
          "Name": "Warning"
        },
        "ScheduledSystemEventSet": {
          "ScheduledSystemEventType": [
            {
              "EventId": "e-event3",
              "EventCycleStatus": {
                "Code": 24,
                "Name": "Scheduled"
              },
              "EventType": {
                "Code": 65,
                "Name": "SystemFailure.Reboot"
              },
              "EventPublishTime": "2017-11-30T06:32:31Z",
              "NotBefore": "2017-12-01T06:32:31Z"
            }
          ]
        }
      }
    ]
  },
  "PageSize": 10,
  "PageNumber": 1,
  "TotalCount": 2,
  "RequestId": "AAC49D3E-ED6F-4F00-XXXX-377C551B1DD4"
}
```

**Error response example** 

**XML format**

```
<Error>
    <RequestId>C38E0D94-C18B-44F3-8C05-6E35BE334088</RequestId>
    <HostId>ecs.aliyuncs.com</HostId>
    <Code>InstanceIdLimitExceeded</Code>
    <Message>The amount of InstanceId specified exceeds limit 100.</Message>
</Error>
```

 **JSON format** 

```
{
    "RequestId": "1A8B4B27-8B2D-XXXX-XXXX-0F64DBE4C213",
    "HostId": "ecs.aliyuncs.com"
    "Code": "InstanceIdLimitExceeded"
    "Message": "The amount of InstanceId specified exceeds limit 100."
}
```

## Error codes {#ErrorCode .section}

|Error code| Error message|HTTP status code|Description|
|:---------|:-------------|:---------------|:----------|
|InvalidParameter|The Parameter provided is not valid.|403|The specified parameter is invalid.|
|EventIdLimitExceeded|The amount of EventId specified exceeds limit 100.|403|The number of the specified `EventId` cannot be greater than 100.|
|InstanceIdLimitExceeded|The amount of InstanceId specified exceeds limit 100.|403|The number of the specified `InstanceId` cannot be greater than 100.|
|MissingParameter|The input parameter that is mandatory for processing this request is not supplied.|403|You must specify the required parameter.|
|InternalError|The request processing has failed due to some unknown error,exception or failure.|500|Internal error, please try again later.|

