# DescribeCloudAssistantStatus {#DescribeCloudAssistantStatus .reference}

查询一台或者多台实例是否安装了云助手客户端。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeCloudAssistantStatus|
|RegionId|String|是|实例所在地域ID。您可以调用[DescribeRegions](intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|InstanceId.N|Array|是|实例ID列表。单次请求最多支持20台实例，N的取值范围为\[1, 20\]。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|InstanceCloudAssitantStatus|[InstanceCloudAssitantStatusSet](#)|实例云助手安装状态结果集合。|

 **InstanceCloudAssitantStatusSet**

|名称|类型|描述|
|:-|:-|:-|
|InstanceId|String|实例ID。|
|CloudAssitantStatus|Boolean|实例是否已经安装了云助手。|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeCloudAssistantStatus
&RegionId=cn-hangzhou
&InstanceId.N="i-bp11f7trr4hbi1xxxxxx"
&InstanceId.N="i-bp1iudwa5b1tqaxxxxxx"
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DescribeCloudAssistantStatusResponse>
	<InstanceCloudAssitantStatus>
		<InstanceCloudAssitantStatusSet>
			<InstanceId>i-bp11f7trr4hbi1xxxxxx</InstanceId>
			<CloudAssitantStatus>True</CloudAssitantStatus>
		</InstanceCloudAssitantStatusSet>
		<InstanceCloudAssitantStatusSet>
			<InstanceId>i-bp1iudwa5b1tqaxxxxxx</InstanceId>
			<CloudAssitantStatus>True</CloudAssitantStatus>
		</InstanceCloudAssitantStatusSet>
	</InstanceCloudAssitantStatus>
</DescribeCloudAssistantStatusResponse>
```

**JSON 格式**

```
{
  "InstanceCloudAssitantStatus": {
    "InstanceCloudAssitantStatusSet": [
      {
        "InstanceId": "i-bp11f7trr4hbi1xxxxxx",
        "CloudAssitantStatus": "True"
      },
      {
        "InstanceId": "i-bp1iudwa5b1tqaxxxxxx",
        "CloudAssitantStatus": "True"
      }
    ]
  }
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|MissingParameter.InstanceIds|The input parameter “InstanceIds” that is mandatory for processing this request is not supplied.|400|`InstanceIds`为必需参数。|
|MissingParameter.RegionId|The input parameter “RegionId” that is mandatory for processing this request is not supplied.|400|`RegionId`为必需参数。或者您暂时无法使用该地域里的资源。|
|InvalidInstance.NotFound|The specified instances do not exist.|404|指定的`InstanceId`不存在。|
|InvalidRegionId.NotFound|The RegionId provided does not exist inour items.|404|指定的`RegionId`不存在。|

