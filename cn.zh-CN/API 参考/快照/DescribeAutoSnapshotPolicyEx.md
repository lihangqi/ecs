# DescribeAutoSnapshotPolicyEx {#DescribeAutoSnapshotPolicyEx .reference}

查询您已创建的自动快照策略。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeAutoSnapshotPolicyEx|
|RegionId|String|是|要查询的自动快照策略所在的地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|AutoSnapshotPolicyId|String|否|自动快照策略 ID。|
|PageNumber|Integer|否|自动快照策略返回结果分多页展示。 起始值：1 默认值：1

|
|PageSize|Integer|否|分页展示返回的自动快照策略时的每页行数。 最大值：50默认值：10

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|TotalCount|Integer|自动快照策略的总个数|
|PageNumber|Integer|自动快照策略列表的页码|
|PageSize|Integer|分页展示返回的自动快照策略时的每页行数|
|AutoSnapshotPolicies|Array|自动快照策略详情 [AutoSnapshotPolicyType](intl.zh-CN/API参考/数据类型/AutoSnapshotPolicyType.md#) 组成的集合|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeAutoSnapshotPolicyEX
&RegionId=cn-hangzhou
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DescribeAutoSnapshotPolicyResponse>
<AutoSnapshotPolicies>
        <AntoSnapshotPolicy>
            <CreationTime>2014-04-21T12:08:52Z</CreationTime>
            <AutoSnapshotPolicyId>p-23f2i9s4t</AutoSnapshotPolicyId>
           <SettingTimePoints>[“2”, “9”]</SettingTimePoints>
            <SettingRepeatWeekdays>[“3” , “4” , “5” , “7”]</SettingRepeatWeekdays>
            <RetentionDays>-1</RetentionDays>
            </AntoSnapshotPolicy>
        <AntoSnapshotPolicy>
            <CreationTime>2014-07-24T13:00:52Z</CreationTime>
            <AutoSnapshotPolicyId>p-23f2i9s4t</AutoSnapshotPolicyId>
            <SettingTimePoints>[“0”, “1”]</SettingTimePoints>
            <SettingRepeatWeekdays>[“1”, “7”]</SettingRepeatWeekdays>
            <RetentionDays>30</RetentionDays>
        </AntoSnapshotPolicy>
    </AutoSnapshotPolicies>
    <PageNumber>1</PageNumber>
    <PageSize>2</PageSize>
    <TotalCount>2</TotalCount>
    <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</DescribeAutoSnapshotPolicyResponse>
```

 **JSON 格式** 

```
{
  "PageNumber": 1,
  "PageSize": 2,
  "RequestId": "659F91C6-1949-43B0-90C4-B6342CA757D5",
  "AutoSnapshotPolicies": {
    " AutoSnapshotPolicy": [
      {
        "CreationTime": "2014-07-24T13:00:52Z",
        "AutoSnapshotPolicyId": "p-23f2i9s4t",
        "SettingTimePoints": "[“0”, “1”]",
        "SettingRepeatWeekdays": "[“1”, “7”]",
        "RetentionDays": "30",
      },
      {
        "CreationTime": "2014-04-21T12:08:52Z",
        "AutoSnapshotPolicyId": "p-a1fd3g5s1",
        "SettingTimePoints": "[“2”, “9”]",
        "SettingRepeatWeekdays": "[“3” , “4” , “5” , “7”]",
        "RetentionDays": "-1",
      }
    ]
  },
  "TotalCount": 2
}
```

## 错误码 {#ErrorCode .section}

全是公共错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

