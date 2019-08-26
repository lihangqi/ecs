# DescribeTaskAttribute {#DescribeTaskAttribute .reference}

查询异步任务的详细信息。目前，可以查询的异步任务有导入镜像（[ImportImage](intl.zh-CN/API 参考/镜像/ImportImage.md#)）和导出镜像（[ExportImage](intl.zh-CN/API 参考/镜像/ExportImage.md#)）两种。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeTaskAttribute|
|RegionId|String|是|地域 ID。您可以调用 [DescribeRegions](intl.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|TaskId|String|否|任务 ID。您可以调用 [DescribeTasks](intl.zh-CN/API 参考/其他接口/DescribeTasks.md#) 查看任务 ID。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|askId|String|任务状态|
|TaskAction|String|任务操作的接口名称|
|RegionId|String|地域 ID|
|TaskStatus|String|任务状态|
|Progress|String|任务进度|
|SupportCancel|String|是否可以取消任务（[CancelTask](intl.zh-CN/API 参考/其他接口/CancelTask.md#)）。可能值：-   True：可以取消
-   False：无法取消

|
|SuccessCount|Integer|成功任务数|
|FailedCount|Integer|失败任务数|
|CreationTime|String|任务创建时间。按照 [ISO8601](intl.zh-CN/API 参考/附录/时间格式.md#) 标准表示，并使用 UTC 时间，格式为 YYYY-MM-DDThh:mm:ssZ|
|FinishedTime|String|任务完成时间。按照 ISO8601 标准表示，并使用 UTC 时间，格式为 YYYY-MM-DDThh:mm:ssZ|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeTaskAttribute
&RegionId=cn-hangzhou
&TaskId=t-23ym6mvro
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DescribeTaskAttributeResponse>
  <CreationTime>2015-11-23T02:13Z</CreationTime>
  <OperationProgressSet>
    <OperationProgress>
      <RelatedItemSet>
        <RelatedItem>
          <Name>OSSBucket</Name>
          <Value>image-temp</Value>
        </RelatedItem>
        <RelatedItem>
          <Name>OSSObject</Name>
          <Value>MYOSSPRE_m-23f8tcp8y_t-23ym6mvro.vhd</Value>
        </RelatedItem>
        <RelatedItem>
          <Name>ImageFormat</Name>
          <Value>vhd</Value>
        </RelatedItem>
      </RelatedItemSet>
      <ErrorMsg/>
      <ErrorCode/>
      <OperationStatus>Success</OperationStatus>
    </OperationProgress>
  </OperationProgressSet>
  <FinishedTime>2015-11-23T02:19Z</FinishedTime>
  <FailedCount>0</FailedCount>
  <SupportCancel>true</SupportCancel>
  <TotalCount>1</TotalCount>
  <SuccessCount>1</SuccessCount>
  <RequestId>EF0C5969-279B-49C8-AD83-BACCC74DD38C</RequestId>
  <RegionId>cn-hangzhou</RegionId>
  <TaskAction>ExportImage</TaskAction>
  <TaskStatus>Finished</TaskStatus>
  <TaskProcess>100%</TaskProcess>
  <TaskId>t-23ym6mvro</TaskId>
</DescribeTaskAttributeResponse>
```

 **JSON 格式** 

```
{
    "CreationTime": "2015-11-23T02:13Z",
    "OperationProgressSet": {
        "OperationProgress": [
            {
                "RelatedItemSet": {
                    "RelatedItem": [
                        {
                            "Name": "OSSBucket",
                            "Value": "image-temp"
                        },
                        {
                            "Name": "OSSObject",
                            "Value": "MYOSSPRE_m-23f8tcp8y_t-23ym6mvro.vhd"
                        },
                        {
                            "Name": "ImageFormat",
                            "Value": "vhd"
                        }
                    ]
                },
                "ErrorMsg": "",
                "ErrorCode": "",
                "OperationStatus": "Success"
            }
        ]
    },
    "FinishedTime": "2015-11-23T02:19Z",
    "FailedCount": 0,
    "SupportCancel": true,
    "TotalCount": 1,
    "SuccessCount": 1,
    "RequestId": "4BE2C7FE-C7A4-4675-A153-174E032AABFB",
    "RegionId": "cn-hangzhou",
    "TaskAction": "ExportImage",
    "TaskStatus": "Finished",
    "TaskProcess": "100%",
    "TaskId": "t-23ym6mvro"
}
```

## 错误码 {#ErrorCode .section}

全是公共错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

