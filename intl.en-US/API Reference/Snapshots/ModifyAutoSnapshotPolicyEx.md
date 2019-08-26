# ModifyAutoSnapshotPolicyEx {#doc_api_999633 .reference}

Modifies an automatic snapshot policy. After you modify an automatic snapshot policy, the new policy takes effect immediately on the disks that have applied the policy.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyAutoSnapshotPolicyEx) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|autoSnapshotPolicyId|String|Yes|p-autopolicyid1| The ID of the automatic snapshot policy to be modified. You can call [DescribeAutoSnapshotPolicyEx](~~25530~~) to view available automatic snapshot policies.

 |
|regionId|String|Yes|cn-hangzhou| The ID of the region to which the automatic snapshot policy belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|ModifyAutoSnapshotPolicyEx| The operation that you want to perform. Set the value to ModifyAutoSnapshotPolicyEx.

 |
|autoSnapshotPolicyName|String|No|FinanceJoshua| The name of the automatic snapshot policy. If this parameter is not specified, the policy name is not modified.

 |
|repeatWeekdays|String|No|\["1", "7"\]| The repeat date for the automatic snapshot. This parameter specifies which day of the week that the automatic snapshot is created on. Valid values: 1 to 7, corresponding to the days of a week, where 1 indicates Monday. To schedule multiple automatic snapshot tasks for a disk in a week, you can set the RepeatWeekdays parameter to an array.

 -   You can specify a maximum of seven dates.
-   You must specify the parameter in a JSON-formatted array: \["1", "2", … "7"\]. Separate multiple values with commas \(,\).

 |
|retentionDays|Integer|No|30| The retention period of the automatic snapshot. Unit: days. Valid values:

 -   -1 \(default\): The automatic snapshot is retained permanently.
-   1-65536: The automatic snapshot is retained for the specified number of days.

 |
|timePoints|String|No|\["0", "1"\]| The point in time at which automatic snapshots are created. Valid values: 0 to 23, corresponding to the 24 hours within the range of 00:00 to 23:00. For example, 1 indicates 01:00. To schedule multiple automatic snapshot tasks for a disk in a day, you can set the TimePoints parameter to an array.

 -   You can specify a maximum of 24 points in time.
-   You must specify the parameter in a JSON-formatted array: \["0", "1", … "23"\]. Separate multiple values with commas \(,\).

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ModifyAutoSnapshotPolicyEx
&autoSnapshotPolicyId=p-autopolicyid1
&regionId=cn-hangzhou
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyAutoSnapshotPolicyResponse>
  <RequestId>F3CD6886-D8D0-4FEE-B93E-1B73239673DE</RequestId>
</ModifyAutoSnapshotPolicyResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"F3CD6886-D8D0-4FEE-B93E-1B73239673DE"
}
```

## Error codes {#section_06n_j8o_ckh .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|ParameterInvalid|The specified automatic snapshot policy does not exist.|The error message returned when the specified automatic snapshot policy does not exist. Check whether the policy ID is correct.|
|404|ParameterInvalid|The specified automatic snapshot policy does not exist in the region.|The error message returned when the specified automatic snapshot policy does not exist. Check whether the policy ID is correct.|
|403|ParameterInvalid|The specified RegionId parameter is invalid.|The error message returned when the specified value of the RegionId parameter is invalid.|
|403|ParameterInvalid|The specified RepeatWeekDays parameter is invalid.|The error message returned when the specified value of the RepeatWeekDays parameter is invalid.|
|403|ParameterInvalid|The specified TimePoints parameter is invalid.|The error message returned when the specified value of the TimePoints parameter is invalid.|
|403|ParameterInvalid|The specified AutoSnapshotPolicyId is invalid.|The error message returned when the specified value of the AutoSnapshotPolicyId parameter is invalid.|
|403|ParameterInvalid|The specified RetentionDays parameter is invalid.|The error message returned when the specified value of the RetentionDays parameter is invalid.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

