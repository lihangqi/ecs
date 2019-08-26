# DescribeSnapshots {#DescribeSnapshots .reference}

查询一台ECS实例或一块磁盘设备所有的快照列表。`InstanceId`、`DiskId`和`SnapshotIds`不是必需参数，但是可以构建过滤器逻辑，参数之间为逻辑与（`And`）关系。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeSnapshots|
|RegionId|String|是|磁盘所属于的地域ID。您可以调用[DescribeRegions](../cn.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|InstanceId|String|否|指定的实例ID。|
|DiskId|String|否|指定的磁盘设备ID。|
|Encrypted|Boolean|否|过滤加密快照。取值范围：-   true：只筛选出加密快照
-   false：不做加密属性的筛选

默认值：False|
|SnapshotIds|String|否|快照标识编码。取值可以由多个快照ID组成一个JSON数组，格式为\["s-xxxxxxxxx", "s-yyyyyyyyy", … "s-zzzzzzzzz"\]，最多支持100个ID，ID之间用半角逗号（`,`）隔开。|
|SnapshotName|String|否|快照名称。|
|Status|String|否|快照状态。取值范围：-   progressing：正在创建的快照
-   accomplished：创建成功的快照
-   failed：创建失败的快照
-   all：所有快照状态

默认值：all|
|SnapshotType|String|否|快照类型。取值范围：-   auto：自动快照
-   user：手动创建的快照
-   all：所有快照类型

默认值：all|
|SourceDiskType|String|否|快照源磁盘的磁盘类型。取值范围：-   System：根据系统盘创建的快照
-   Data：根据数据盘创建的快照

|
|Usage|String|否|有引用关系的资源类型。取值范围：-   image：使用快照 [CreateImage](cn.zh-CN/API 参考/镜像/CreateImage.md#)
-   disk：使用快照 [CreateDisk](cn.zh-CN/API 参考/磁盘/CreateDisk.md#)
-   image\_disk：使用快照创建了数据盘和自定义镜像
-   none：暂无引用关系

|
|Tag.n.Key|String|否|快照的标签键。n的取值范围：\[1, 20\]。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun、acs:、http://或者https://开头。|
|Tag.n.Value|String|否|快照的标签值。n的取值范围：\[1, 20\]。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun、acs:、http://或者https://开头。|
|PageNumber|Integer|否|快照列表的页码。起始值：1默认值：1

|
|PageSize|Integer|否|分页查询时设置的每页行数。最大值：100默认值：10

|
|DryRun|Boolean|否|是否只预检此次请求。-   true：发送检查请求，不会查询资源状况。检查项包括AccessKey是否有效、RAM用户的授权情况和是否填写了必需参数。如果检查不通过，则返回对应错误。如果检查通过，会返回错误码`DryRunOperation`。
-   false：发送正常请求，通过检查后返回2XX HTTP状态码并直接查询资源状况。

默认值：false

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|TotalCount|Integer|快照总个数|
|PageNumber|Integer|快照列表的页码|
|PageSize|Integer|输入时设置的每页行数|
|Snapshots|[SnapshotType](cn.zh-CN/API 参考/数据类型/SnapshotType.md#)|快照详情集合|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeSnapshots
&RegionId=cn-hangzhou
&<公共请求参数>
```

**返回示例**

**XML格式**

```
<DescribeSnapshotsResponse>
    <Snapshots>
        <Snapshot>
            <CreationTime>2014-07-24T13:00:52Z</CreationTime>
            <Description></Description>
            <SourceDiskId>d-23x0r79qy</SourceDiskId>
            <SourceDiskType>DATA</SourceDiskType>
            <ProductCode></ProductCode>
            <SnapshotName>auto_20140724_2</SnapshotName>
            <Progress>100%</Progress>
            <SourceDiskSize>50</SourceDiskSize>
            <Status>accomplished</Status>
            <SnapshotId>s-23f2i9s4t</SnapshotId>
            <Usage>none</Usage>
        </Snapshot>
        <Snapshot>
            <CreationTime>2014-07-24T13:00:42Z</CreationTime>
            <Description></Description>
            <SourceDiskId>101-70105379</SourceDiskId>
            <SourceDiskType>DATA</SourceDiskType>
            <ProductCode></ProductCode>
            <SnapshotName>auto_20140724_2</SnapshotName>
            <Progress>100%</Progress>
            <SourceDiskSize>5</SourceDiskSize>
            <Status>accomplished</Status>
            <SnapshotId>s-23izto5qm</SnapshotId>
            <Usage>none</Usage>
        </Snapshot>
    </Snapshots>
    <PageNumber>1</PageNumber>
    <PageSize>2</PageSize>
    <TotalCount>36</TotalCount>
    <RequestId>2F409D67-329A-4405-B924-2FC28566B366</RequestId>
</DescribeSnapshotsResponse>
```

**JSON格式** 

```
{
  "PageNumber": 1,
  "PageSize": 2,
  "RequestId": "659F91C6-1949-43B0-90C4-B6342CA757D5",
  "Snapshots": {
    "Snapshot": [
      {
        "CreationTime": "2015-07-30T05:00:14Z",
        "Progress": "100%",
        "SnapshotId": "s-943ypfgic",
        "SnapshotName": "auto_20150730_3",
        "SourceDiskId": "d-944qyqjfa",
        "SourceDiskSize": 20,
        "SourceDiskType": "system",
        "Status": "accomplished",
        "Usage": "none"
      },
      {
        "CreationTime": "2015-07-30T05:00:14Z",
        "Progress": "100%",
        "SnapshotId": "s-94osg320e",
        "SnapshotName": "auto_20150730_3",
        "SourceDiskId": "d-94j355jsq",
        "SourceDiskSize": 20,
        "SourceDiskType": "system",
        "Status": "accomplished",
        "Usage": "none"
      }
    ]
  },
  "TotalCount": 36
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|DryRunOperation|Request validation has been passed with DryRun flag set.|400|此次DryRun预检请求合格。|
|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|400|指定的参数`Tag.n.Key`和`Tag.n.Value`不匹配。|
|InvalidTagCount|The specified tags are beyond the permitted range.|400|指定的标签数超过了5个。|
|InvalidSnapshotIds.Malformed|The amount of specified specified snapshot Ids exceeds the limit.|403|指定的参数`SnapshotIds`格式不正确。|
|InvalidSnapshotType.NotFound|The specfied SnapshotType is not found.|404|指定的参数`SnapshotType`取值有误。|
|InvalidSourceDiskType|The specifed SourceDiskType is not valid.|404|指定的参数`SourceDiskType`不合法。|
|InvalidStatus.NotFound|The specified Status is not found.|404|指定的参数`Status`取值有误。|
|InvalidUsage|The specifed Usage is not valid.|404|指定的参数`Usage`不合法。|

