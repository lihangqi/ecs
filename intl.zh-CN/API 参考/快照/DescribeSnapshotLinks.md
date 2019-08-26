# DescribeSnapshotLinks {#DescribeSnapshotLinks .reference}

查询磁盘快照链。快照链是一个磁盘所有快照组成的关系链，一个磁盘对应一条快照链，所以快照链 ID 即磁盘 ID。

## 描述 {#section_vg2_jb1_ydb .section}

调用该接口时，您需要注意：

-   请求参数 `RegionId`、`DiskIds` 和 `InstanceId` 等充当过滤器功能，参数间是逻辑与关系。

-   如果不指定任何参数，则过滤器不起作用。当 `DiskIds` 和 `SnapshotLinkIds` 都为空数组时，即 `[]`，同样视该过滤器有效，但是返回结果为空。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeSnapshotLinks|
|RegionId|String|是|磁盘所属于的地域 ID。您可以调用 [DescribeRegions](cn.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|InstanceId|String|否|实例 ID。|
|DiskIds|String|否|磁盘 ID。一次最多指定 100 个磁盘 ID。`DiskIds` 参数取值格式为 JSON 数组，如 \["d-xxxxxxxxx", "d-yyyyyyyyy", … "d-zzzzzzzzz"\]，ID 之间用半角逗号（`,`）隔开。|
|SnapshotLinkIds|String|否|快照 ID。一次最多指定 100 个快照 ID。`SnapshotLinkIds`参数取值格式为 JSON 数组，如 \["p-xxxxxxxxx", "p-yyyyyyyyy", … "p-zzzzzzzzz"\]，ID 之间用半角逗号（`,`）隔开。|
|PageNumber|Integer|否|磁盘状态列表的页码。起始值：1默认值：1

|
|PageSize|Integer|否|分页查询时设置的每页行数。取值范围：\[1, 50\]。默认值：10

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|RegionId|String|快照链源磁盘所属地域 ID|
|TotalCount|Integer|快照链总个数|
|PageNumber|Integer|快照链列表的页码|
|PageSize|Integer|输入时设置的每页行数|
|SnapshotLinks|[SnapshotLinkType](cn.zh-CN/API 参考/数据类型/SnapshotLinkType.md#)|快照链信息组成的集合|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeSnapshotLinks
&RegionId=cn-beijing
&ZoneId=cn-beijing-btc-a01
&PageNumber=1
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DescribeSnapshotLinksResponse>
    <SnapshotLinks>
        <SnapshotLink>
            <SnapshotLinkId>d-25okbh2pj</SnapshotLinkId >
            <SourceDiskId>d-25okbh2pj</SourceDiskId>
            <SourceDiskType>data</SourceDiskType>
            <SourceDiskSize>20</SourceDiskSize>
            <RegionId> cn-beijing-btc-a01</RegionId>
            <TotalCount>1</TotalCount>
            <TotalSize>2097152</TotalSize>
        </SnapshotLink>
        <SnapshotLink>
            <SnapshotLinkId>d-2ze0y1jwzpb1geqxkroq</SnapshotLinkId >
            <SourceDiskId>d-2ze0y1jwzpb1geqxkroq</SourceDiskId>
            <SourceDiskType>system</SourceDiskType>
            <SourceDiskSize>40</SourceDiskSize>
            <RegionId> cn-beijing-btc-a01</RegionId>
            <TotalCount>1</TotalCount>
            <TotalSize>2097152</TotalSize>
         </SnapshotLink>
    </SnapshotLinks>
    <PageNumber>1</PageNumber>
    <PageSize>2</PageSize>
    <TotalCount>9</TotalCount>
    <RequestId>ED5CF6DD-71CA-462C-9C94-A61A78A01479</RequestId>
</DescribeSnapshotLinksResponse>
```

 **JSON 格式** 

```
{
    "SnapshotLinks": {
    "SnapshotLink": [
    {
        "SourceDiskSize": 20,
        "TotalSize": 2097152,
        "SourceDiskType": "data",
        "RegionId": "cn-beijing-btc-a01",
        "SnapshotLinkId": "d-25okbh2pj",
        "SourceDiskId": "d-25okbh2pj",
        "TotalCount": 1
    },
    {
        "SourceDiskSize": 40,
        "TotalSize": 2097152,
        "SourceDiskType": "data",
        "RegionId": "cn-beijing-btc-a01",
        "SnapshotLinkId": "d-2ze0y1jwzpb1geqxkroq",
        "SourceDiskId": "d-2ze0y1jwzpb1geqxkroq",
        "TotalCount": 1
    }
    ]
    },
    "PageNumber": 1,
    "PageSize": 2,
    "RequestId": "ACD9BBB0-A9D1-46D7-9630-B7A69889E110",
    "TotalCount": 9
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidDiskIds|The specified diskIds is invalid.|400|指定的 `DiskIds` 不合法。|
|InvalidRegionId|The specified regionId is invalid.|400|指定的 `RegionId` 不合法。|
|InvalidSnapshotLinkIds|The specified snapshotLinkIds is invalid.|400|指定的 `SnapshotLinkIds` 不合法。|
|InternalError|The request processing has failed due to some unknown error.|500|内部错误。|

