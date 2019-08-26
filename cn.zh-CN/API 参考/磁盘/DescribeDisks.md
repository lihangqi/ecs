# DescribeDisks {#DescribeDisks .reference}

查询您已经创建的磁盘。

## 描述 {#section_pl3_qn5_xdb .section}

-   请求参数`RegionId`、`ZoneId`、`DiskIds`和`InstanceId`等都是过滤器的概念，参数间是逻辑与（`AND`）关系。
-   请求参数`DiskIds`是一个JSON格式的数组（Array），如果参数为空，则过滤器不起作用，但是`DiskIds`如果是一个空数组，即`[]`，则视为该过滤器有效，且返回空。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeDisks|
|RegionId|String|是|磁盘所属于的地域ID。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|Encrypted|Boolean|否|是否过滤加密磁盘。取值范围:-   true：只筛选出加密磁盘
-   false：不做加密属性的筛选

默认值：false|
|ZoneId|String|否|可用区ID。|
|DiskIds|String|否|磁盘ID。一个带有格式的JSON数组，格式为\["d-xxxxxxxxx", "d-yyyyyyyyy", … "d-zzzzzzzzz"\]，最多100个ID，用半角逗号（,）隔开。|
|InstanceId|String|否|实例ID。|
|DiskType|String|否|要查询的磁盘类型。取值范围：-   all：同时查询系统盘与数据盘
-   system：只查询系统盘
-   data：只查询数据盘

默认值：all|
|Category|String|否|磁盘种类。取值范围：-   all：所有磁盘
-   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD盘
-   local\_ssd\_pro：I/O密集型本地盘
-   local\_hdd\_pro：吞吐密集型本地盘
-   ephemeral：本地磁盘
-   ephemeral\_ssd：本地SSD盘

默认值：all|
|Status|String|否|磁盘状态，参考文档[普通云盘状态](intl.zh-CN/API 参考/附录/普通云盘状态表.md#)。取值范围：-   In\_use
-   Available
-   Attaching
-   Detaching
-   Creating
-   ReIniting
-   All

默认值：All|
|SnapshotId|String|否|创建磁盘使用的快照。|
|DiskName|String|否|磁盘名称。|
|Portable|Boolean|否|要查询的磁盘是否支持卸载，该属性为不可修改属性。取值范围：-   true：可卸载磁盘，可以独立存在且可以自由在可用区内挂载和卸载
-   false：不可卸载磁盘，不可以独立存在且不可以自由在可用区内挂载和卸载

这个属性为`true`的磁盘才能挂载和卸载，其中：-   本地盘
-   本地SSD盘
-   普通云盘，高效云盘和SSD盘的系统盘
-   包年包月的普通云盘、高效云盘、SSD盘

该属性都为`false`。|
|DeleteWithInstance|String|否|磁盘是否随实例释放。取值范围：-   true：实例释放时，这块磁盘随实例一起释放
-   false：实例释放时，这块磁盘保留不释放

默认值：false|
|DeleteAutoSnapshot|Boolean|否|删除磁盘时，是否同时删除自动快照。取值范围：-   true：同时删除自动快照
-   false：保留自动快照

默认值：false|
|EnableAutoSnapshot|String|否|磁盘是否执行自动快照策略（前提是用户整体的自动快照策略已经开启）。取值范围：-   true：表示这块磁盘执行自动快照策略
-   false：表示这块磁盘不执行自动快照策略

默认值：false|
|Tag.n.Key|String|否|磁盘的标签键。n的取值范围：\[1, 20\]。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun、acs:、http://或者https://开头。|
|Tag.n.Value|String|否|磁盘的标签值。n的取值范围：\[1, 20\]。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun、acs:、http://或者https://开头。|
|PageNumber|Integer|否|磁盘状态列表的页码，起始值：1默认值：1

|
|PageSize|Integer|否|分页查询时设置的每页行数，最大值：100默认值：10

|
|DryRun|Boolean|否|是否只预检此次请求。-   true：发送检查请求，不会查询资源状况。检查项包括AccessKey是否有效、RAM用户的授权情况和是否填写了必需参数。如果检查不通过，则返回对应错误。如果检查通过，会返回错误码`DryRunOperation`。
-   false：发送正常请求，通过检查后返回2XX HTTP状态码并直接查询资源状况。

默认值：false

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|Encrypted|Boolean|是否为加密磁盘|
|TotalCount|Integer|磁盘总数|
|PageNumber|Integer|磁盘列表的页码|
|PageSize|Integer|输入时设置的每页行数|
|Disks|[DiskItemType](intl.zh-CN/API 参考/数据类型/DiskItemType.md#)|磁盘信息组成的集合|

## 示例 { .section}

**请求示例**

```
https://ecs.aliyuncs.com/?action=DescribeDisks
&RegionId=cn-qingdao
&PageNumber=1
&ZoneId=cn-qingdao-b
&<公共请求参数>
```

**返回示例**

**XML格式**

```
<DescribeDisksResponse>
    <Disks>
        <Disk>
            <DeleteAutoSnapshot>true</DeleteAutoSnapshot>
            <DeleteWithInstance>false</DeleteWithInstance>
            <EnableAutoSnapshot>false</EnableAutoSnapshot>
            <Category>cloud</Category>
            <Description></Description>
            <DiskName></DiskName>
            <Size>5</Size>
            <Type>data</Type>
            <InstanceId></InstanceId>
            <CreationTime>2014-07-23T02:44:07Z</CreationTime>
            <ImageId></ImageId>
            <ZoneId>cn-qingdao-b</ZoneId>
            <AttachedTime>2014-07-23T07:47:35Z</AttachedTime>
            <DetachedTime>2014-07-23T08:28:48Z</DetachedTime>
            <Device></Device>
            <OperationLocks></OperationLocks>
            <Portable>true</Portable>
            <ProductCode></ProductCode>
            <RegionId>cn-qingdao</RegionId>
            <DiskId>d-28m5zbua0</DiskId>
            <SourceSnapshotId></SourceSnapshotId>
            <Status>Available</Status>
        </Disk>
        <Disk>
            <DeleteAutoSnapshot>true</DeleteAutoSnapshot>
            <DeleteWithInstance>false</DeleteWithInstance>
            <EnableAutoSnapshot>false</EnableAutoSnapshot>
            <Category>cloud</Category>
            <Description></Description>
            <DiskName></DiskName>
            <Size>5</Size>
            <Type>data</Type>
            <InstanceId></InstanceId>
            <CreationTime>2014-07-23T02:44:06Z</CreationTime>
            <ImageId></ImageId>
            <ZoneId>cn-qingdao-b</ZoneId>
            <AttachedTime></AttachedTime>
            <DetachedTime></DetachedTime>
            <Device></Device>
            <OperationLocks></OperationLocks>
            <Portable>true</Portable>
            <ProductCode></ProductCode>
            <RegionId>cn-qingdao</RegionId>
            <DiskId>d-28zfrmo13</DiskId>
            <SourceSnapshotId></SourceSnapshotId>
            <Status>Available</Status>
        </Disk>
    </Disks>
    <PageNumber>1</PageNumber>
    <PageSize>2</PageSize>
    <TotalCount>9</TotalCount>
    <RequestId>ED5CF6DD-71CA-462C-9C94-A61A78A01479</RequestId>
</DescribeDisksResponse>
```

**JSON格式**

```
{
  "Disks": {
    "Disk": [
      {
        "AttachedTime": "2014-07-23T07:47:35Z",
        "Category": "cloud",
        "CreationTime": "2014-07-23T02:44:07Z",
        "DeleteAutoSnapshot": true,
        "DeleteWithInstance": false,
        "EnableAutoSnapshot": false
        "Description": "",
        "DetachedTime": "2014-07-23T08:28:48Z",
        "Device": "",
        "DiskId": "d-28m5zbua0",
        "DiskName": "",
        "ImageId": "",
        "InstanceId": "",
        "OperationLocks": {
            "OperationLock": []
        },
        "Portable": true,
        "ProductCode": "",
        "RegionId": "cn-qingdao",
        "Size": 5,
        "SourceSnapshotId": "",
        "Status": "Available",
        "Type": "data",
        "ZoneId": "cn-qingdao-b"
      },
      {
        "AttachedTime": "",
        "Category": "cloud",
        "CreationTime": "2014-07-23T02:44:06Z",
        "DeleteAutoSnapshot": true,
        "DeleteWithInstance": false,
        "EnableAutoSnapshot": false
        "Description": "",
        "DetachedTime": "",
        "Device": "",
        "DiskId": "d-28zfrmo13",
        "DiskName": "",
        "ImageId": "",
        "InstanceId": "",
        "OperationLocks": {
            "OperationLock": []
        },
        "Portable": true,
        "ProductCode": "",
        "RegionId": "cn-qingdao",
        "Size": 5,
        "SourceSnapshotId": "",
        "Status": "Available",
        "Type": "data",
        "ZoneId": "cn-qingdao-b"
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

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|InvalidCategory.ValueNotSupported|The specified disk category is not supported.|400|指定的磁盘种类不支持，或者您暂时没有权限使用此类磁盘。|
|InvalidDiskType.ValueNotSupported|The specified disk type is not supported.|400|指定的磁盘属性不支持。|
|InvalidRegion.NotFound|The specified parameter RegionId is not valid.|400|指定的`RegionId`不存在。|
|InvalidStatus.ValueNotSupported|The specified disk status is not supported.|400|指定的磁盘状态不支持。|
|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|400|指定的`Tag.n.Key`和`Tag.n.Value`不匹配。|
|InvalidTagCount|The specified tags are beyond the permitted range.|400|指定的标签数超过了5个。|
|InvalidZoneId.NotFound|The ZoneId provided does not exist.|400|指定的`ZoneId`不存在。|
|InvalidDiskIds.Malformed|The amount of specified disk Ids exceeds the limit.|403|指定的`DiskId`格式不正确。|
|InvalidDiskChargeType.NotFound|The DiskChargeType does not exist.|404|指定的`DiskChargeType`不存在。|
|DryRunOperation|Request validation has been passed with DryRun flag set.|400|此次DryRun预检请求合格。|
|InvalidLockReason.NotFound|The specified LockReason is not found|404|指定的`LockReason`不存在。|

