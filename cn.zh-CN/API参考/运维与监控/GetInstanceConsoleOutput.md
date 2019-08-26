# GetInstanceConsoleOutput {#doc_api_Ecs_GetInstanceConsoleOutput .reference}

调用GetInstanceConsoleOutput获取一台实例的系统命令行输出，数据以Base64编码后返回。

## 接口说明 {#description .section}

-   云服务器ECS是虚拟化的云上服务，无法接入显示设备，也无法手动截屏。但是我们缓存了实例最近一次启动、重启或者关机时的系统命令行输出，您可以调用GetInstanceConsoleOutput获取。
-   [已停售的实例规格](~~55263~~) 无法获取系统命令行输出。
-   Windows实例暂不支持获取系统命令行输出。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=GetInstanceConsoleOutput)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-myInstance|实例ID。

 |
|RegionId|String|是|cn-shenzhen-finance-1|实例所在地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|GetInstanceConsoleOutput|系统规定参数。取值：GetInstanceConsoleOutput

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|ConsoleOutput|String|V2VsY29tZSB0byBDZW50T1MgCgpDaGVja2luZyBmaWxlc3lzdGVtcwpDaGVja2luZyBhbGwgZmlsZSBzeXN0ZW1zLgpbL3NiaW4vZnNjay5leHQ0ICgxKSAtLSAvXSBmc2NrLmV4dDQgLWEgL2Rldi92ZGExIAovZGV2L3ZkYTE6IGNsZWFuLCAzMjAxNi8yNjIxNDQwIGZpbGVzLCA0NDc5NzQvMTA0ODU1MDQgYmxvY2tzCgpFbnRlcmluZyBub24taW50ZXJhY3RpdmUgc3RhcnR1cApDYWxsaW5nIHRoZSBzeXN0ZW0gYWN0aXZpdHkgZGF0YSBjb2xsZWN0b3IgKHNhZGMpLi4uIAoKQnJpbmdpbmcgdXAgaW50ZXJmYWNlIGV0aDA6ICAKRGV0ZXJtaW5pbmcgSVAgaW5mb3JtYXRpb24gZm9yIGV0aDAuLi4gZG9uZS4KCmFsaXl1bi1zZXJ2aWNlIHN0YXJ0L3J1bm5pbmcsIHByb2Nlc3MgMTczMwpmaW5pc2hlZAoKQ2VudE9TIHJlbGVhc2UgNi44IChGaW5hbCkKS2VybmVsIDIuNi4zMi02OTYuMy4yLmVsNi5pNjg2IG9uIGFuIGk2ODYKCmlaMnplZDk2ZTQ2MmF5cjBxemw2czhaIGxvZ2luOg==|实例的系统命令行输出，根据Base64编码后输出。

 |
|InstanceId|String|i-myInstance|实例ID。

 |
|LastUpdateTime|String|2018-03-22 10:04:57|实例最近一次启动、重启或者关机的时间。按照 [ISO8601](~~25696~~) 标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
http://ecs-cn-hangzhou.aliyuncs.com/?Action=GetInstanceConsoleOutput
&InstanceId=i-myInstance
&RegionId=cn-shenzhen-finance-1
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<GetInstanceConsoleOutputResponse>
  <RequestId>22A1933F-AD02-4560-A6A7-53CF2231D942</RequestId>
  <InstanceId>i-j5e42sbbthlokka11***</InstanceId>
  <LastUpdateTime>2018-03-22 10:04:57</LastUpdateTime>
  <ConsoleOutput>V2VsY29tZSB0byBDZW50T1MgCgpDaGVja2luZyBmaWxlc3lzdGVtcwpDaGVja2luZyBhbGwgZmlsZSBzeXN0ZW1zLgpbL3NiaW4vZnNjay5leHQ0ICgxKSAtLSAvXSBmc2NrLmV4dDQgLWEgL2Rldi92ZGExIAovZGV2L3ZkYTE6IGNsZWFuLCAzMjAxNi8yNjIxNDQwIGZpbGVzLCA0NDc5NzQvMTA0ODU1MDQgYmxvY2tzCgpFbnRlcmluZyBub24taW50ZXJhY3RpdmUgc3RhcnR1cApDYWxsaW5nIHRoZSBzeXN0ZW0gYWN0aXZpdHkgZGF0YSBjb2xsZWN0b3IgKHNhZGMpLi4uIAoKQnJpbmdpbmcgdXAgaW50ZXJmYWNlIGV0aDA6ICAKRGV0ZXJtaW5pbmcgSVAgaW5mb3JtYXRpb24gZm9yIGV0aDAuLi4gZG9uZS4KCmFsaXl1bi1zZXJ2aWNlIHN0YXJ0L3J1bm5pbmcsIHByb2Nlc3MgMTczMwpmaW5pc2hlZAoKQ2VudE9TIHJlbGVhc2UgNi44IChGaW5hbCkKS2VybmVsIDIuNi4zMi02OTYuMy4yLmVsNi5pNjg2IG9uIGFuIGk2ODYKCmlaMnplZDk2ZTQ2MmF5cjBxemw2czhaIGxvZ2luOg==</ConsoleOutput>
</GetInstanceConsoleOutputResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"ConsoleOutput":"V2VsY29tZSB0byBDZW50T1MgCgpDaGVja2luZyBmaWxlc3lzdGVtcwpDaGVja2luZyBhbGwgZmlsZSBzeXN0ZW1zLgpbL3NiaW4vZnNjay5leHQ0ICgxKSAtLSAvXSBmc2NrLmV4dDQgLWEgL2Rldi92ZGExIAovZGV2L3ZkYTE6IGNsZWFuLCAzMjAxNi8yNjIxNDQwIGZpbGVzLCA0NDc5NzQvMTA0ODU1MDQgYmxvY2tzCgpFbnRlcmluZyBub24taW50ZXJhY3RpdmUgc3RhcnR1cApDYWxsaW5nIHRoZSBzeXN0ZW0gYWN0aXZpdHkgZGF0YSBjb2xsZWN0b3IgKHNhZGMpLi4uIAoKQnJpbmdpbmcgdXAgaW50ZXJmYWNlIGV0aDA6ICAKRGV0ZXJtaW5pbmcgSVAgaW5mb3JtYXRpb24gZm9yIGV0aDAuLi4gZG9uZS4KCmFsaXl1bi1zZXJ2aWNlIHN0YXJ0L3J1bm5pbmcsIHByb2Nlc3MgMTczMwpmaW5pc2hlZAoKQ2VudE9TIHJlbGVhc2UgNi44IChGaW5hbCkKS2VybmVsIDIuNi4zMi02OTYuMy4yLmVsNi5pNjg2IG9uIGFuIGk2ODYKCmlaMnplZDk2ZTQ2MmF5cjBxemw2czhaIGxvZ2luOg==",
	"InstanceId":"i-j5e42sbbthlokka11***",
	"RequestId":"22A1933F-AD02-4560-A6A7-53CF2231D942",
	"LastUpdateTime":"2018-03-22 10:04:57"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter|%s|缺失必需参数。|
|404|InvalidParameter|%s|参数格式不正确。|
|405|IncorrectInstanceStatus|%s|实例当前的状态不支持该操作。|
|405|NotSupported|%s|HPC集群不存在。|
|429|Throttling|%s|请求被流控。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

