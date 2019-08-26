# GetInstanceConsoleOutput {#reference_bmg_nvk_l2b .reference}

获取一台实例的系统命令行输出，数据以 Base64 编码后返回。

## 描述 {#BestPractice .section}

云服务器 ECS 是虚拟化的云上服务，无法接入显示设备，也无法手动截屏。但是我们缓存了实例最近一次启动、重启或者关机时的系统命令行输出，您可以调用 `GetInstanceConsoleOutput` 获取。

[已停售的实例规格](https://www.alibabacloud.com/help/faq-detail/55263.htm) 无法获取系统命令行输出。

Windows 实例暂不支持获取系统命令行输出。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：GetInstanceConsoleOutput|
|RegionId|String|是|实例所在地域 ID。您可以调用 [DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|InstanceId|String|是|实例 ID。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|InstanceId|String|实例 ID。|
|ConsoleOutput|String|实例的系统命令行输出，根据 Base64 编码后输出。|
|LastUpdateTime|String|实例最近一次启动、重启或者关机的时间。参数取值使用 UTC 时间，时区为 UTC+0，按照 [ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#) 标准表示，格式为 YYYY-MM-DDTHH:mm:ssZ。|

## 示例 { .section}

**请求示例** 

```
http://ecs-cn-hangzhou.aliyuncs.com/?Action=GetInstanceConsoleOutput
&RegionId=cn-shenzhen-finance-1
&InstanceId=i-j5e42sbbthlokka11eci
&<公共请求参数> 
```

**正常返回示例** 

**XML 格式**

```
<GetInstanceConsoleOutputResponse>
    <RequestId>22A1933F-AD02-4560-A6A7-53CF2231D942</RequestId>
    <InstanceId>i-j5e42sbbthlokka11ech</InstanceId>
    <LastUpdateTime>2018-03-22 10:04:57</LastUpdateTime>
    <ConsoleOutput>V2VsY29tZSB0byBDZW50T1MgCgpDaGVja2luZyBmaWxlc3lzdGVtcwpDaGVja2luZyBhbGwgZmlsZSBzeXN0ZW1zLgpbL3NiaW4vZnNjay5leHQ0ICgxKSAtLSAvXSBmc2NrLmV4dDQgLWEgL2Rldi92ZGExIAovZGV2L3ZkYTE6IGNsZWFuLCAzMjAxNi8yNjIxNDQwIGZpbGVzLCA0NDc5NzQvMTA0ODU1MDQgYmxvY2tzCgpFbnRlcmluZyBub24taW50ZXJhY3RpdmUgc3RhcnR1cApDYWxsaW5nIHRoZSBzeXN0ZW0gYWN0aXZpdHkgZGF0YSBjb2xsZWN0b3IgKHNhZGMpLi4uIAoKQnJpbmdpbmcgdXAgaW50ZXJmYWNlIGV0aDA6ICAKRGV0ZXJtaW5pbmcgSVAgaW5mb3JtYXRpb24gZm9yIGV0aDAuLi4gZG9uZS4KCmFsaXl1bi1zZXJ2aWNlIHN0YXJ0L3J1bm5pbmcsIHByb2Nlc3MgMTczMwpmaW5pc2hlZAoKQ2VudE9TIHJlbGVhc2UgNi44IChGaW5hbCkKS2VybmVsIDIuNi4zMi02OTYuMy4yLmVsNi5pNjg2IG9uIGFuIGk2ODYKCmlaMnplZDk2ZTQ2MmF5cjBxemw2czhaIGxvZ2luOg==</ConsoleOutput>
</GetInstanceConsoleOutputResponse>
```

**JSON 格式** 

```
{
    "RequestId": "22A1933F-AD02-4560-A6A7-53CF2231D942",
    "InstanceId": "i-j5e42sbbthlokka11ech",
    "LastUpdateTime": "2018-03-22 10:04:57",
    "ConsoleOutput": "V2VsY29tZSB0byBDZW50T1MgCgpDaGVja2luZyBmaWxlc3lzdGVtcwpDaGVja2luZyBhbGwgZmlsZSBzeXN0ZW1zLgpbL3NiaW4vZnNjay5leHQ0ICgxKSAtLSAvXSBmc2NrLmV4dDQgLWEgL2Rldi92ZGExIAovZGV2L3ZkYTE6IGNsZWFuLCAzMjAxNi8yNjIxNDQwIGZpbGVzLCA0NDc5NzQvMTA0ODU1MDQgYmxvY2tzCgpFbnRlcmluZyBub24taW50ZXJhY3RpdmUgc3RhcnR1cApDYWxsaW5nIHRoZSBzeXN0ZW0gYWN0aXZpdHkgZGF0YSBjb2xsZWN0b3IgKHNhZGMpLi4uIAoKQnJpbmdpbmcgdXAgaW50ZXJmYWNlIGV0aDA6ICAKRGV0ZXJtaW5pbmcgSVAgaW5mb3JtYXRpb24gZm9yIGV0aDAuLi4gZG9uZS4KCmFsaXl1bi1zZXJ2aWNlIHN0YXJ0L3J1bm5pbmcsIHByb2Nlc3MgMTczMwpmaW5pc2hlZAoKQ2VudE9TIHJlbGVhc2UgNi44IChGaW5hbCkKS2VybmVsIDIuNi4zMi02OTYuMy4yLmVsNi5pNjg2IG9uIGFuIGk2ODYKCmlaMnplZDk2ZTQ2MmF5cjBxemw2czhaIGxvZ2luOg=="
}
```

**异常返回示例** 

**XML 格式**

```
<Error>
    <RequestId>C38E0D94-C18B-44F3-8C05-6E35BE334088</RequestId>
    <HostId>ecs.aliyuncs.com</HostId>
    <Code>NotSupported</Code>
    <Message>The operation is not supported for "i-j5e42sbbthlokkaXXXXX".</Message>
</Error>
```

**JSON 格式** 

```
{
    "RequestId": "C38E0D94-C18B-44F3-8C05-6E35BE334088",
    "HostId": "ecs.aliyuncs.com",
    "Code": "NotSupported",
    "Message": "The operation is not supported for "i-j5e42sbbthlokkaXXXXX"."
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|MissingParameter|The input parameter “instanceId” that is mandatory for processing this request is not supplied.|400|您必须指定参数 `InstanceId`。|
|InvalidParameter|The “instanceId” provided is not valid.|404|指定的 `InstanceId` 不存在。|
|IncorrectInstanceStatus|The instance status “\{status\}” is not applicable|405|指定的实例已被释放或者已停止。|
|NotSupported|The operation is not supported for “\{instanceId\}”|405|[已停售的实例规格](https://www.alibabacloud.com/help/faq-detail/55263.htm) 无法获取系统命令行输出。|

