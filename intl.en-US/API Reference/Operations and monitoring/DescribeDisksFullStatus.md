# DescribeDisksFullStatus {#DescribeDisksFullStatus .reference}

Describes the full status information of a disk.

## Description {#section_gpz_ts4_ydb .section}

-   The full status information of a disk includes the disk life cycle status \(`Status`\), disk health status \(`HealthStatus`\), and disk event type \(`EventType`\).

-   Because the disk-related **event release time**, **scheduled event execution time**, and **actual event execution time** are the same, if you specify a period \[`EventTime.Start`, `EventTime.End`\], the system queries all history events that have occurred during the period. Currently, you can query the system events history within the last week.


## Request parameters {#RequestParameter .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: DescribeDisksFullStatus.|
|RegionId|String|Yes|ID of the region where the specified disk belongs. For more information, call [DescribeRegions](../intl.en-US/API Reference/Regions/DescribeRegions.md#) to obtain the latest region list.|
|DiskId.N|String|No|Disk ID. Value range of N: \[1, 100\].|
|EventId.N|String|No|Event ID. Value range of N: \[1, 100\].|
|Status|String|No|Life cycle status of the disk. For more information, see [Cloud disk status table](intl.en-US/API Reference/Appendix/Basic cloud disk status table.md#). Optional values:-   In Use
-   Available
-   Attaching
-   Detaching
-   Creating
-   Resilience

|
|HealthStatus|String|No|Health status of the disk. Optional values:-   Impaired: The disk is damaged.
-   Warning: The performance of disk may be degraded because of maintenance or technical issues.
-   Initializing: The disk is in reinitialization process.
-   InsufficientData: The event details cannot be determined because of insufficient data.
-   NotApplicable: Not applicable.

|
|EventType|String|No|Disk event type. Optional values:-   Degraded: The disk performance is downgraded.
-   SeverelyDegraded: The disk performance is seriously downgraded.
-   Stalled: The disk may be stalled with I/O suspended.

|
|EventTime.Start|String|No|Queries the start time of the event occurrence time. The time format follows the [ISO8601](../intl.en-US/API Reference/Appendix/ISO 8601 Time Format.md#) standard, and the UTC time is used. The format is yyyy-MM-ddTHH:mm:ssZ.|
|EventTime.End|String|No|Queries the end time of the event occurrence time. The time format follows the [ISO8601](../intl.en-US/API Reference/Appendix/ISO 8601 Time Format.md#) standard, and the UTC time is used. The format is yyyy-MM-ddTHH:mm:ssZ.|
|PageNumber|Integer|No|Page number of the query result. The value must be a positive integer.Default value: 1.

|
|PageSize|Integer|No|Page size of the query result. Value range: \[1, 100\].Default value: 10.

|

## Response parameters {#ResponseParameter .section}

|Name|Type|Description|
|:---|:---|:----------|
|TotalCount|Integer|Total number of the status of the disks.|
|Page number of the status list of the disks|Integer|ECS instance list page number.|
|Pagesize|Integer|Size of each page.|
|DiskFullStatusSet|Array of [DiskFullStatusType](#)|Array of full disk status information.|

**DiskFullStatusType**

|Name|Type|Description|
|:---|:---|:----------|
|DiskId|String|Disk ID.|
|InstanceId|String|Instance ID.|
|Device|String|Device information of the related instance, such as /dev/xvdb. It is null unless the `Status` is **In Use** \(`In_use`\).|
|Diskeventset|Array of [DiskEventType](#)|Array of disk events.|
|Status.Code|Integer|Code of the disk life cycle status.|
|Status.Name|String|Name of the disk life cycle status.|
|HealthStatus.Code|Integer|Code of the disk health status.|
|HealthStatus.Name|String|Name of the disk health status.|

**DiskEventType**

|Name|Type|Description|
|:---|:---|:----------|
|EventId|String|Disk event ID.|
|EventType.Code|Integer|Event type code.|
|EventType.Name|String|Event type name.|
|EventTime|String|Event occurrence time. The time format follows the [ISO8601](../intl.en-US/API Reference/Appendix/ISO 8601 Time Format.md#) standard, and the UTC time is used. The format is yyyy-MM-ddTHH:mm:ssZ.|
|EventEndTime|String|Event terminal time. The time format follows the [ISO8601](../intl.en-US/API Reference/Appendix/ISO 8601 Time Format.md#) standard, and the UTC time is used. The format is yyyy-MM-ddTHH:mm:ssZ.|

## Examples { .section}

**Request example**

```
https://ecs.aliyuncs.com/?Action=DescribeDisksFullStatus
&RegionId=cn-hangzhou
&<Common Request Parameters>
```

**Success response example**

**XML format**

```
<DescribeDisksFullStatusResponse>
    <DiskFullStatusSet>
        <DiskFullStatusType>
            <DiskEventSet>
                <DiskEventType>
                    <EventId>e-event1</EventId>
                    <EventType>
                        <Code>7</Code>
                        <Name>Stalled</Name>
                    </EventType>
                    <EventTime>2018-05-08T02:43:10Z</EventTime>
                </DiskEventType>
            </DiskEventSet>
            <DiskId>d-disk1</DiskId>
            <InstanceId>i-instance1</InstanceId>
            <HealthStatus>
                <Code>128</Code>
                <Name>Impaired</Name>
            </HealthStatus>
            <Status>
                <Code>129</Code>
                <Name>Available</Name>
            </Status>
        </DiskFullStatusType>
        <DiskFullStatusType>
            <DiskEventSet>
                <DiskEventType>
                    <EventId>e-event2</EventId>
                    <EventType>
                        <Code>1</Code>
                        <Name>Degraded</Name>
                    </EventType>
                    <EventTime>2018-05-06T02:43:10Z</EventTime>
                    <EventEndTime>2018-05-06T02:48:52Z</EventEndTime>
                </DiskEventType>
            </DiskEventSet>
            <DiskId>d-disk2</DiskId>
            <InstanceId>i-instance2</InstanceId>
            <HealthStatus>
                <Code>64</Code>
                <Name>Warning</Name>
            </HealthStatus>
            <Status>
                <Code>0</Code>
                <Name>Ok</Name>
            </Status>
        </DiskFullStatusType>
    </DiskFullStatusSet>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <RequestId>1A8B4B27-8B2D-XXXX-XXXX-0F64DBE4C211</RequestId>
    <TotalCount>2</TotalCount>
</DescribeDisksFullStatusResponse>
```

**JSON format**

```
{
    "DiskFullStatusSet": {
        "DiskFullStatusType": [
            {
                "DiskEventSet": {
                    "DiskEventType": [
                        {
                            "EventId": "e-event1",
                            "EventType": {
                                "Code": "7",
                                "Name": "Stalled"
                            },
                            "EventTime": "2018-05-08T02:43:10Z"
                        }
                    ]
                },
                "DiskId": "d-disk1",
                "InstanceId": "i-instance1",
                "HealthStatus": {
                    "Code": 128,
                    "Name": "Impaired"
                },
                "Status": {
                    "Code": 129,
                    "Name": "Available"
                }
            },
            {
                "DiskEventSet": {
                    "DiskEventType": [
                        {
                            "EventId": "e-event2",
                            "EventType": {
                                "Code": "1",
                                "Name": "Degraded"
                            },
                            "EventTime": "2018-05-06T02:43:10Z",
                            "EventEndTime": "2018-05-06T02:48:52Z"
                        }
                    ]
                },
                "DiskId": "d-disk2",
                "InstanceId": "i-instance2",
                "HealthStatus": {
                    "Code": 0,
                    "Name": "Ok"
                },
                "Status": {
                    "Code": 129,
                    "Name": "Available"
                }
            }
        ]
    },
    "PageNumber": 1,
    "PageSize": 10,
    "RequestId": "1A8B4B27-8B2D-XXXX-XXXX-0F64DBE4C211",
    "TotalCount": 2
}
```

**Error response example**

**XML format**

```
<Error>
    <RequestId>C38E0D94-C18B-44F3-8C05-6E35BE334086</RequestId>
    <HostId>ecs.aliyuncs.com</HostId>
    <Code>MissingParameter</Code>
    <Message>The input parameter that is mandatory for processing this request is not supplied.</Message>
</Error>
```

**JSON format**

```
{
    "RequestId": "1A8B4B27-8B2D-XXXX-XXXX-0F64DBE4C211",
    "HostId": "ecs.aliyuncs.com"
    "Code": "MissingParameter"
    "Message": "The input parameter that is mandatory for processing this request is not supplied."
}
```

## Error codes {#ErrorCode .section}

Error codes specific to this interface are as follows. For more information, see [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

|Error code|Error information|HTTP status code|Description|
|:---------|:----------------|:---------------|:----------|
|InvalidParameter|The Parameter provided is not valid.|403|The parameter is invalid.|
|InvalidParameter.LengthExceeded|The Parameter provided exceeds maximum length.|403|The value range of N in EventId.N must be \[1, 100\].|
|InvalidParameter.TooManyDiskId|The diskIds provided is out of bounds \[1,100\].|403|The specified parameter value is out of the valid range.|
|InvalidParameter.TimeEndBeforeStart|The event time end should be after event time start.|403|The specified event time filter condition is not legal and the end time must be later than the start time.|
|MissingParameter|The input parameter that is mandatory for processing this request is not supplied.|403|You must specify the required parameter.|
|InternalError|The request processing has failed due to some unknown error, exception or failure.|500|Internal error, please try again later.|

