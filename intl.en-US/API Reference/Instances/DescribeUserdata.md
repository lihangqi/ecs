# DescribeUserdata {#DescribeUserdata .reference}

Describes the  [user data](../../../../intl.en-US/User Guide/Instances/User-defined data and metadata/User data.md#) of an ECS instance.

## Description {#section_jwv_kws_xdb .section}

-   The returned user data is encoded by the means of Base64.
-   If the user data does not exist, a null value is returned.

## Request parameters {#RequestParameter .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: DescribeUserdata|
|RegionId|String|Yes|The region ID of the instance. You can call [DescribeRegions](intl.en-US/API Reference/Regions/DescribeRegions.md#) View the latest list of Alibaba Cloud regions.|
|InstanceId|String|Yes|The ID of the specified instance.|

## Return parameters {#ResponseParameter .section}

|Name|Type|Description|
|:---|:---|:----------|
|UserData|String|The user data of the instance, displayed in the Base64 code.|
|InstanceId|String|The instance ID.|
|RegionId|String|The region ID|

## Example { .section}

**Request example** 

```
https://ecs.aliyuncs.com/?Action=DescribeUserdata
&RegionId=cn-shenzhen
&InstanceId=i-instance1
&<Common request parameters>

```

```
https://ecs.example.com/?Action= DescribeUserdata
&RegionId=cn-shenzhen
&InstanceId=i-instance1
&<Common request parameters>

```

**Response sample** 

**XML format**

```
<DescribeUserdataResponse>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
    <UserData>userdata1</UserData>
    <InstanceId> i-instance1</InstanceId>
    <RegionId> cn-shenzhen </RegionId>
</DescribeUserdataResponse>
```

 **JSON format** 

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
    "UserData": "userdata1"
    "InstanceId": "i-instance1"
    "RegionId": "cn-shenzhen"
}
```

## Error codes {#ErrorCode .section}

Error codes specific to this interface are as follows. For more error codes, see [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

|Error code|Error message|HTTP status code |Note|
|:---------|:------------|:----------------|:---|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|The specified `RegionId` does not exist.|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|The specified `InstanceId` does not exist.|

