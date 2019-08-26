# ReportInstancesStatus {#doc_api_Ecs_ReportInstancesStatus .reference}

调用ReportInstancesStatus反馈一台或者多台ECS实例的异常问题。您可以反馈多台ECS实例发生的相同问题，也可以反馈一台ECS实例的多块磁盘发生的相同问题。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ReportInstancesStatus)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId.N|RepeatList|是|i-2ze9y\*\*\*\*wtqcvai68rl|一台或者多台ECS实例ID。

 N的取值范围：1~100，多个取值使用重复列表的形式。

 |
|RegionId|String|是|cn-hangzhou|实例所在地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|Reason|String|是|abnormal-local-disk|反馈原因，即实例发生的异常类型。取值范围：

 -   instance-hang：ECS实例不可用，或无法连接。
-   instance-stuck-in-status：ECS实例长时间停留在某一个状态，如Starting或Stopping状态。
-   abnormal-network：ECS实例发生网络异常。
-   abnormal-local-disk：ECS实例挂载的本地盘出现异常。
-   abnormal-cloud-disk：ECS实例挂载的云盘或共享块存储出现异常。
-   others：其他异常类型。当以上异常类型不符合条件时，您可以设置`Reason=Other`并在`Description`中描述更多信息。

 |
|Action|String|否|ReportInstancesStatus|系统规定参数。对于您自行拼凑HTTP/HTTPS URL发起的API请求，`Action`为必选参数。取值：ReportInstancesStatus

 |
|Description|String|否|本地盘不可用，挂载点拒绝访问，无法加载文件。|异常问题的详细描述。

 **说明：** 当`reason=abnormal-local-disk`时，`Description`为必选参数。

 |
|DiskId.N|RepeatList|否|d-ab3f7y0e\*\*\*\*\*\*\*\*68rl|发生相同异常问题的一块或者多块磁盘ID。如果您使用的是弹性裸金属服务器实例，请填写磁盘设备对应的SN列表。

 N的取值范围：1~100，多个取值使用重复列表的形式。

 |
|Device.N|RepeatList|否|/dev/xvdb|发生相同异常问题的一块或多块磁盘的挂载的设备名列表。如果您使用的是弹性裸金属服务器实例，请填写磁盘设备对应SLOT槽位信息列表。

 N的取值范围：1~100，多个取值使用重复列表的形式。

 |
|EndTime|String|否|2017-11-31T06:32:31Z|实例异常问题结束时间。按照ISO8601标准表示，并需要使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|StartTime|String|否|2017-11-30T06:32:31Z|实例异常问题开始时间。按照ISO8601标准表示，并需要使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
http(s)://ecs.aliyuncs.com/?Action=ReportInstancesStatus
&InstanceId.1=i-2ze9y****wtqcvai68rl
&Reason=abnormal-local-disk
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ReportInstancesStatusResponse>
  <RequestId>4DD56CA6-6D75-4D33-BE34-E4A44EBE1C3D</RequestId>
</ReportInstancesStatusResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"4DD56CA6-6D75-4D33-BE34-E4A44EBE1C3D"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|MissingParameter|%s|缺失必需参数。|
|403|InvalidParameter|%s|参数格式不正确。|
|403|InstanceIdLimitExceeded|%s|指定的InstanceId个数不得超过100个。|
|403|DiskIdLimitExceeded|%s|指定的DiskId个数不得超过100个。|
|403|InvalidInstanceId.NotFound|%s|指定的实例不存在。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

