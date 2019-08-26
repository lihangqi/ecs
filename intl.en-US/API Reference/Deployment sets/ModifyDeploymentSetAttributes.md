# ModifyDeploymentSetAttributes {#doc_api_999649 .reference}

Modifies the name and description of a deployment set.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=ModifyDeploymentSetAttribute) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|DeploymentSetId|String|Yes|ds-deploymentsetid| The ID of a deployment set.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region where the deployment set resides. You can call DescribeRegions to view the latest list of Alibaba Cloud regions.

 |
|Action|String|No|ModifyDeploymentSetAttribute| The operation that you want to perform. Set the value to ModifyDeploymentSetAttributes.

 |
|DeploymentSetName|String|No|FinanceJoshua| The name of the deployment set. It must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\).

 |
|Description|String|No|FinanceDept| The description of the deployment set. It must be 2 to 256 characters in length and cannot start with http:// or https://.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ModifyDeploymentSetAttributes
&RegionId=cn-hangzhou 
&Strategy=Availability
&DeploymentSetId=ds-bp1frxuzdg87zh4pzqkc
&DeploymentSetName=AvailMySet
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ModifyDeploymentSetAttributesResponse>
  <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
</ModifyDeploymentSetAttributesResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## Error codes {#section_pco_n9a_fay .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter|The input parameter RegionId that is mandatory for processing this request is not supplied.|The error message returned when the RegionId parameter is empty.|
|400|InvalidDescription.Malformed|The specified parameter Description is not valid.|The error message returned when the specified description is invalid. It must be 2 to 256 characters in length and cannot start with http:// or https://.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

