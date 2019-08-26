# GetInstanceConsoleOutput {#doc_api_999421 .reference}

Obtains the command output of an instance. The returned command output is encoded in Base64.

## Description {#description .section}

ECS is a virtualized cloud-based service that cannot be connected to any display devices. However, the command output for the last start, restart, or shutdown of the instance is cached. You can call GetInstanceConsoleOutput to obtain this information.

For [phased-out instance types](~~55263~~), you cannot obtain the command output.

You cannot obtain the command output of Windows-based instances.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=GetInstanceConsoleOutput) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId|String|Yes|i-myInstance| The ID of the instance.

 |
|RegionId|String|Yes|cn-shenzhen-finance-1| The ID of the region where the instance is located. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|GetInstanceConsoleOutput| The operation that you want to perform. Set the value to GetInstanceConsoleOutput.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|ConsoleOutput|String|V2VsY29tZSB0byBDZW50T1MgCgpDaGVja2luZyBmaWxlc3lzdGVtcwpDaGVja2luZyBhbGwgZmlsZSBzeXN0ZW1zLgpbL3NiaW4vZnNjay5leHQ0ICgxKSAtLSAvXSBmc2NrLmV4dDQgLWEgL2Rldi92ZGExIAovZGV2L3ZkYTE6IGNsZWFuLCAzMjAxNi8yNjIxNDQwIGZpbGVzLCA0NDc5NzQvMTA0ODU1MDQgYmxvY2tzCgpFbnRlcmluZyBub24taW50ZXJhY3RpdmUgc3RhcnR1cApDYWxsaW5nIHRoZSBzeXN0ZW0gYWN0aXZpdHkgZGF0YSBjb2xsZWN0b3IgKHNhZGMpLi4uIAoKQnJpbmdpbmcgdXAgaW50ZXJmYWNlIGV0aDA6ICAKRGV0ZXJtaW5pbmcgSVAgaW5mb3JtYXRpb24gZm9yIGV0aDAuLi4gZG9uZS4KCmFsaXl1bi1zZXJ2aWNlIHN0YXJ0L3J1bm5pbmcsIHByb2Nlc3MgMTczMwpmaW5pc2hlZAoKQ2VudE9TIHJlbGVhc2UgNi44IChGaW5hbCkKS2VybmVsIDIuNi4zMi02OTYuMy4yLmVsNi5pNjg2IG9uIGFuIGk2ODYKCmlaMnplZDk2ZTQ2MmF5cjBxemw2czhaIGxvZ2luOg==| The command output of the instance, in Base64 encoding.

 |
|InstanceId|String|i-myInstance| The ID of the instance.

 |
|LastUpdateTime|String|2018-03-22 10:04:57| The time the instance was last started, restarted, or shut down. The time format follows the [ISO 8601](~~25696~~) standard and uses UTC time. The format is yyyy-MM-ddTHH:mm:ssZ.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
http://ecs-cn-hangzhou.aliyuncs.com/?Action=GetInstanceConsoleOutput
&InstanceId=i-myInstance
&RegionId=cn-shenzhen-finance-1 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<GetInstanceConsoleOutputResponse>
  <RequestId>22A1933F-AD02-4560-A6A7-53CF2231D942</RequestId>
  <InstanceId>i-j5e42sbbthlokka11ech</InstanceId>
  <LastUpdateTime>2018-03-22 10:04:57</LastUpdateTime>
  <ConsoleOutput>V2VsY29tZSB0byBDZW50T1MgCgpDaGVja2luZyBmaWxlc3lzdGVtcwpDaGVja2luZyBhbGwgZmlsZSBzeXN0ZW1zLgpbL3NiaW4vZnNjay5leHQ0ICgxKSAtLSAvXSBmc2NrLmV4dDQgLWEgL2Rldi92ZGExIAovZGV2L3ZkYTE6IGNsZWFuLCAzMjAxNi8yNjIxNDQwIGZpbGVzLCA0NDc5NzQvMTA0ODU1MDQgYmxvY2tzCgpFbnRlcmluZyBub24taW50ZXJhY3RpdmUgc3RhcnR1cApDYWxsaW5nIHRoZSBzeXN0ZW0gYWN0aXZpdHkgZGF0YSBjb2xsZWN0b3IgKHNhZGMpLi4uIAoKQnJpbmdpbmcgdXAgaW50ZXJmYWNlIGV0aDA6ICAKRGV0ZXJtaW5pbmcgSVAgaW5mb3JtYXRpb24gZm9yIGV0aDAuLi4gZG9uZS4KCmFsaXl1bi1zZXJ2aWNlIHN0YXJ0L3J1bm5pbmcsIHByb2Nlc3MgMTczMwpmaW5pc2hlZAoKQ2VudE9TIHJlbGVhc2UgNi44IChGaW5hbCkKS2VybmVsIDIuNi4zMi02OTYuMy4yLmVsNi5pNjg2IG9uIGFuIGk2ODYKCmlaMnplZDk2ZTQ2MmF5cjBxemw2czhaIGxvZ2luOg==</ConsoleOutput> 
</GetInstanceConsoleOutputResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"ConsoleOutput":"V2VsY29tZSB0byBDZW50T1MgCgpDaGVja2luZyBmaWxlc3lzdGVtcwpDaGVja2luZyBhbGwgZmlsZSBzeXN0ZW1zLgpbL3NiaW4vZnNjay5leHQ0ICgxKSAtLSAvXSBmc2NrLmV4dDQgLWEgL2Rldi92ZGExIAovZGV2L3ZkYTE6IGNsZWFuLCAzMjAxNi8yNjIxNDQwIGZpbGVzLCA0NDc5NzQvMTA0ODU1MDQgYmxvY2tzCgpFbnRlcmluZyBub24taW50ZXJhY3RpdmUgc3RhcnR1cApDYWxsaW5nIHRoZSBzeXN0ZW0gYWN0aXZpdHkgZGF0YSBjb2xsZWN0b3IgKHNhZGMpLi4uIAoKQnJpbmdpbmcgdXAgaW50ZXJmYWNlIGV0aDA6ICAKRGV0ZXJtaW5pbmcgSVAgaW5mb3JtYXRpb24gZm9yIGV0aDAuLi4gZG9uZS4KCmFsaXl1bi1zZXJ2aWNlIHN0YXJ0L3J1bm5pbmcsIHByb2Nlc3MgMTczMwpmaW5pc2hlZAoKQ2VudE9TIHJlbGVhc2UgNi44IChGaW5hbCkKS2VybmVsIDIuNi4zMi02OTYuMy4yLmVsNi5pNjg2IG9uIGFuIGk2ODYKCmlaMnplZDk2ZTQ2MmF5cjBxemw2czhaIGxvZ2luOg==",
	"InstanceId":"i-j5e42sbbthlokka11ech",
	"RequestId":"22A1933F-AD02-4560-A6A7-53CF2231D942",
	"LastUpdateTime":"2018-03-22 10:04:57"
}
```

## Error codes {#section_z4n_x1j_qm5 .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter|%s|The error message returned when a required parameter is not specified.|
|404|InvalidParameter|%s|The error message returned when the parameter format is invalid.|
|405|IncorrectInstanceStatus|%s|The error message returned when the specified resource is in a state that does not support the current operation.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

