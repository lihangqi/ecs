# DescribeSnapshotsUsage {#DescribeSnapshotsUsage .reference}

查询您在一个地域下的快照数量以及快照容量。如果您想知道当前地域下每块磁盘的快照使用情况，推荐使用 DescribeSnapshotLinks 查询磁盘快照链。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeSnapshotsUsage|
|RegionId|String|是|快照所属的地域 ID。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|SnapshotCount|Integer|当前地域下的快照份数。|
|SnapshotSize|Long|当前地域下已产生的快照容量，单位 B。|

## 示例 {#Samples .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeSnapshotsUsage
&RegionId=cn-hangzhou
&<公共请求参数>
```

**返回示例**

**XML 格式**

```
<DescribeSnapshotsUsageResponse>
	<SnapshotCount>5</SnapshotCount>
	<SnapshotSize>122</SnapshotSize>
    
    <RequestId>ED5CF6DD-71CA-462C-9C94-A61A78A01479</RequestId>
</DescribeSnapshotsUsageResponse>
```

**JSON 格式**

```
{
	"SnapshotCount": "5",
	"SnapshotSize": "122",
	"RequestId": "ACD9BBB0-A9D1-46D7-9630-B7A69889E110"
}
```

## 错误码 {#ErrorCode .section}

全是公共错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

