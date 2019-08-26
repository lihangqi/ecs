# GetInstanceConsoleOutput {#reference_bmg_nvk_l2b .reference}

Obtains the console output of an instance. The returned command line output is encoded in Base64 format.

## Description {#BestPractice .section}

ECS instances are virtualized cloud-based services that cannot be connected to display devices or make mobile snapshots. However, the instance console output for the last start, restart, or shutdown of the instance is cached. You can call the `GetInstanceConsoleOutput` to monitor and analyze the instance exceptions.

Currently, the [phased-out instance types](https://www.alibabacloud.com/help/faq-detail/55263.htm) cannot obtain the console output.

Moreover, Windows instances cannot obtain console output as well.

## Request parameters  {#RequestParameter .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: GetInstanceConsoleOutput.|
|RegionId|String|Yes|ID of the region where the ECS instance is located. For more information, use [DescribeRegions](../intl.en-US/API Reference/Regions/DescribeRegions.md#) to obtain the latest region list.|
|InstanceId|String|Yes|Instance ID.|

## Response parameters {#ResponseParameter .section}

|Name|Type|Description|
|:---|:---|:----------|
|InstanceId|String|ID of the instance.|
|ConsoleOutput|String|The instance console output of the instance, in Base64 encoding.|
|LastUpdateTime|String|The time the instance was last started, restarted, or shut down. The value of this parameter uses the offset UTC+0 and is expressed according to the [ISO8601](../intl.en-US/API Reference/Appendix/ISO 8601 Time Format.md#) standard. Format: YYYY-MM-DDTHH:mm:ssZ.|

## Examples { .section}

**Request example** 

```
http://ecs-cn-hangzhou.aliyuncs.com/?Action=GetInstanceConsoleOutput
&RegionId=cn-shenzhen-finance-1
&InstanceId=i-j5e42sbbthlokka11eci
&<Common Request Parameters> 
```

**Success response example** 

**XML format**

```
<GetInstanceConsoleOutputResponse>
    <RequestId>22A1933F-AD02-4560-A6A7-53CF2231D942</RequestId>
    <InstanceId>i-j5e42sbbthlokka11ech</InstanceId>
    <LastUpdateTime>2018-03-22 10:04:57</LastUpdateTime>
    <ConsoleOutput>V2VsY29tZSB0byBDZW50T1MgCgpDaGVja2luZyBmaWxlc3lzdGVtcwpDaGVja2luZyBhbGwgZmlsZSBzeXN0ZW1zLgpbL3NiaW4vZnNjay5leHQ0ICgxKSAtLSAvXSBmc2NrLmV4dDQgLWEgL2Rldi92ZGExIAovZGV2L3ZkYTE6IGNsZWFuLCAzMjAxNi8yNjIxNDQwIGZpbGVzLCA0NDc5NzQvMTA0ODU1MDQgYmxvY2tzCgpFbnRlcmluZyBub24taW50ZXJhY3RpdmUgc3RhcnR1cApDYWxsaW5nIHRoZSBzeXN0ZW0gYWN0aXZpdHkgZGF0YSBjb2xsZWN0b3IgKHNhZGMpLi4uIAoKQnJpbmdpbmcgdXAgaW50ZXJmYWNlIGV0aDA6ICAKRGV0ZXJtaW5pbmcgSVAgaW5mb3JtYXRpb24gZm9yIGV0aDAuLi4gZG9uZS4KCmFsaXl1bi1zZXJ2aWNlIHN0YXJ0L3J1bm5pbmcsIHByb2Nlc3MgMTczMwpmaW5pc2hlZAoKQ2VudE9TIHJlbGVhc2UgNi44IChGaW5hbCkKS2VybmVsIDIuNi4zMi02OTYuMy4yLmVsNi5pNjg2IG9uIGFuIGk2ODYKCmlaMnplZDk2ZTQ2MmF5cjBxemw2czhaIGxvZ2luOg==</ConsoleOutput>
</GetInstanceConsoleOutputResponse>
```

**JSON format** 

```
{
    "RequestId": "22A1933F-AD02-4560-A6A7-53CF2231D942",
    "InstanceId": "i-j5e42sbbthlokka11ech",
    "LastUpdateTime": "2018-03-22 10:04:57",
    "ConsoleOutput": "V2VsY29tZSB0byBDZW50T1MgCgpDaGVja2luZyBmaWxlc3lzdGVtcwpDaGVja2luZyBhbGwgZmlsZSBzeXN0ZW1zLgpbL3NiaW4vZnNjay5leHQ0ICgxKSAtLSAvXSBmc2NrLmV4dDQgLWEgL2Rldi92ZGExIAovZGV2L3ZkYTE6IGNsZWFuLCAzMjAxNi8yNjIxNDQwIGZpbGVzLCA0NDc5NzQvMTA0ODU1MDQgYmxvY2tzCgpFbnRlcmluZyBub24taW50ZXJhY3RpdmUgc3RhcnR1cApDYWxsaW5nIHRoZSBzeXN0ZW0gYWN0aXZpdHkgZGF0YSBjb2xsZWN0b3IgKHNhZGMpLi4uIAoKQnJpbmdpbmcgdXAgaW50ZXJmYWNlIGV0aDA6ICAKRGV0ZXJtaW5pbmcgSVAgaW5mb3JtYXRpb24gZm9yIGV0aDAuLi4gZG9uZS4KCmFsaXl1bi1zZXJ2aWNlIHN0YXJ0L3J1bm5pbmcsIHByb2Nlc3MgMTczMwpmaW5pc2hlZAoKQ2VudE9TIHJlbGVhc2UgNi44IChGaW5hbCkKS2VybmVsIDIuNi4zMi02OTYuMy4yLmVsNi5pNjg2IG9uIGFuIGk2ODYKCmlaMnplZDk2ZTQ2MmF5cjBxemw2czhaIGxvZ2luOg=="
}
```

**Error response example** 

**XML format**

```
<Error>
    <RequestId>C38E0D94-C18B-44F3-8C05-6E35BE334088</RequestId>
    <HostId>ecs.aliyuncs.com</HostId>
    <Code>NotSupported</Code>
    <Message>The operation is not supported for "i-j5e42sbbthlokkaXXXXX".</Message>
</Error>
```

**JSON format** 

```
{
    "RequestId": "C38E0D94-C18B-44F3-8C05-6E35BE334088",
    "HostId": "ecs.aliyuncs.com",
    "Code": "NotSupported",
    "Message": "The operation is not supported for "i-j5e42sbbthlokkaXXXXX"."
}
```

## Error codes {#ErrorCode .section}

Error codes specific to this interface are as follows. For more information, see [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

|Error code|Error message|HTTP status code|Description|
|:---------|:------------|:---------------|:----------|
|MissingParameter|The input parameter “instanceId” that is mandatory for processing this request is not supplied.|400|`InstanceId` is required.|
|InvalidParameter|The “instanceId” provided is not valid.|404|The specified `InstanceId` does not exist.|
|IncorrectInstanceStatus|The instance status “\{status\}” is not applicable|405|The specified instance has been released or stopped.|
|NotSupported|The operation is not supported for “\{instanceId\}”|405|[Phased-out instance types](https://www.alibabacloud.com/help/faq-detail/55263.htm) cannot obtain console output.|

