# DeleteDeploymentSet {#doc_api_999646 .reference}

Deletes a deployment set.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DeleteDeploymentSet) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|DeploymentSetId|String|Yes|ds-deploymentsetid1| The ID of the deployment set. You cannot delete a deployment set that contains instances.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region where the deployment set resides. You can call [DescribeRegions](~~25609~~) to view the latest list of Alibaba Cloud regions.

 |
|Action|String|No|DeleteDeploymentSet| The operation that you want to perform. Set the value to DeleteDeploymentSet.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DeleteDeploymentSet
&RegionId=cn-hangzhou 
&DeploymentSetId=ds-bp1frxuzdg87zh4pzqkc
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DeleteDeploymentSetResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</DeleteDeploymentSetResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## Error codes {#section_osj_i1r_f7l .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter|The input parameter "DeploymentSetId" that is mandatory for processing this request is not supplied.|The error message returned when the DeploymentSetId parameter is empty.|
|403|DependencyViolation.ReferByHPC|The specified deployment set is still referred by an HPC cluster.|The error message returned when the specified deployment set is associated with other HPC clusters.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

