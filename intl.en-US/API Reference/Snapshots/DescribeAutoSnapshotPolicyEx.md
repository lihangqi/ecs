# DescribeAutoSnapshotPolicyEx {#DescribeAutoSnapshotPolicyEx .reference}

Describes your available automatic snapshot policies.

## Request parameters {#RequestParameter .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: DescribeAutoSnapshotPolicyEx.|
|RegionId|String|Yes|The region of the automatic snapshot policies. For more information, see Regions and zones, or call [DescribeRegions](intl.en-US/API Reference/Regions/DescribeRegions.md#) to obtain the latest region list.|
|AutoSnapshotPolicyId|String|No|The ID of the automatic snapshot policy to query.|
|PageNumber|Integer|No|Displays the automatic snapshot policies on several pages. Initial value: 1. Default value: 1.

|
|PageSize|Integer|No|Specifies the number of rows per page in case of querying by page. Maximum value: 50.Default value: 10.

|

## Response parameters {#ResponseParameter .section}

|Name|Type|Description|
|:---|:---|:----------|
|TotalCount|Integer|The total number of automatic snapshot policies.|
|PageNumber|Integer|The page number of the automatic snapshot policy list.|
|PageSize|Integer|The input number of rows per page.|
|AutoSnapshotPolicies|Array|The automatic snapshot policy details, an array composed of [AutoSnapshotPolicyType](intl.en-US/API Reference/Data type/AutoSnapshotPolicyType.md#).|

## Examples { .section}

**Request example** 

```
https://ecs.aliyuncs.com/?Action=DescribeAutoSnapshotPolicyEX
&RegionId=cn-hangzhou
&<Common Request Parameters>
```

**Response example** 

**XML format**

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

 **JSON format** 

```

  "PageNumber": 1,
  "PageSize": 2,
  "RequestId": "659F91C6-1949-43B0-90C4-B6342CA757D5",
  "AutoSnapshotPolicies": {
    " AutoSnapshotPolicy": [
      
        "CreationTime": "2014-07-24T13:00:52Z",
        "AutoSnapshotPolicyId": "p-23f2i9s4t",
        "SettingTimePoints": "[“0”, “1”]",
        "SettingRepeatWeekdays": "[“1”, “7”]",
        "RetentionDays": "30",
      
      
        "CreationTime": "2014-04-21T12:08:52Z",
        "AutoSnapshotPolicyId": "p-a1fd3g5s1",
        "SettingTimePoints": "[“2”, “9”]",
        "SettingRepeatWeekdays": "[“3” , “4” , “5” , “7”]",
        "RetentionDays": "-1",
      
    
  
  "TotalCount": 2

```

## Error codes {#ErrorCode .section}

All are common error codes. For more error codes, see [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

