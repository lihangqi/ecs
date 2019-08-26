# DescribeDeploymentSets {#doc_api_1006118 .reference}

Queries a list of attributes of one or more deployment sets.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeDeploymentSets) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region where a deployment set resides. You can call [DescribeRegions](~~25609~~) to view the latest list of Alibaba Cloud regions.

 |
|Action|String|No|DescribeDeploymentSets| The operation that you want to perform. Set the value to DescribeDeploymentSets.

 |
|DeploymentSetIds|String|No|\["ds-xxxxxxxxx", "ds-yyyyyyyyy", … "ds-zzzzzzzzz"\]| The list of deployment set IDs. The value can contain a JSON array consisting of up to 100 deployment set IDs. The deployment set IDs must be separated by commas \(,\).

 |
|DeploymentSetName|String|No|FinanceJoshua| The name of a deployment set.

 |
|Domain|String|No|Default| The deployment domain.

 **Note:** The parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|Granularity|String|No|Host| The deployment granularity.

 **Note:** The parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|NetworkType|String|No|VPC| The network type in a deployment set.

 **Note:** The parameter will be removed in the future. We recommend that you use other parameters to ensure compatibility.

 |
|PageNumber|Integer|No|1| The page number to be queried in the deployment set list. Starting value: 1.

 Default value: 1.

 |
|PageSize|Integer|No|10| The number of entries per page. Maximum value: 100.

 Default value: 10.

 |
|Strategy|String|No|Availability| The deployment strategy. Value: Availability.

 Default value: null.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|DeploymentSets| | | The detailed information of deployment sets returned in an array.

 |
|└CreationTime|String|2017-12-05T22:40:00Z| The time a deployment set is created.

 |
|└DeploymentSetDescription|String|FinanceDeptHighAvailability| The description of a deployment set.

 |
|└DeploymentSetId|String|ds-deploymentsetid1| The ID of a deployment set..

 |
|└DeploymentSetName|String|FinanceJoshua| The name of a deployment set.

 |
|└DeploymentStrategy|String|Availability| The deployment strategy.

 |
|└Domain|String|Default| The deployment domain.

 |
|└Granularity|String|Host| The deployment granularity.

 |
|└InstanceAmount|Integer|1| The number of instances in a deployment set.

 |
|└InstanceIds| |\["i-instanceid1"\]| The list of instance IDs in a deployment set.

 |
|└Strategy|String|StrictDispersion| The deployment strategy.

 |
|PageNumber|Integer|1| The page number to be queried in the deployment set list.

 |
|PageSize|Integer|10| The number of entries per page.

 |
|RegionId|String|cn-hangzhou| The ID of the region where a deployment set resides.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|TotalCount|Integer|1| The total number of queried deployment sets.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeDeploymentSets
&RegionId=cn-hangzhou 
&DeploymentSetsIds=["ds-bp13v7bjnj9gisnlo1"]
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeDeploymentSetsResponse>
  <PageSize>10</PageSize>
  <TotalCount>1</TotalCount>
  <PageNumber>1</PageNumber>
  <RequestId>1CB9A584-9E43-408D-B5A8-DB42CDECE03B</RequestId>
  <DeploymentSets>
    <DeploymentSet>
      <DeploymentSetDescription>default</DeploymentSetDescription>
      <DeploymentSetId>ds-bp13v7bjnj9gisnlo1ow</DeploymentSetId>
      <DeploymentStrategy>Availability</DeploymentStrategy>
      <DeploymentSetName>test default</DeploymentSetName>
      <InstanceIds>
        <InstanceId>i-sdfkjsdfk</InstanceId>
        <InstanceId>i-kiiwsch</InstanceId>
      </InstanceIds>
    </DeploymentSet>
  </DeploymentSets>
</DescribeDeploymentSetsResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"DeploymentSets":{
		"DeploymentSet":[
			{
				"DeploymentSetDescription":"default",
				"InstanceIds":{
					"InstanceId":[
						"i-sdfkjsdfk",
						"i-kiiwsch"
					]
				},
				"DeploymentSetName":"test default",
				"DeploymentStrategy":"Availability",
				"DeploymentSetId":"ds-bp13v7bjnj9gisnlo1ow"
			}
		]
	},
	"PageNumber":1,
	"TotalCount":1,
	"PageSize":10,
	"RequestId":"1CB9A584-9E43-408D-B5A8-DB42CDECE03B"
}
```

## Error codes {#section_s1b_5w8_0h2 .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|InvalidDeploymentSetIds.TooManyInput|The parameter DeploymentSets size should less than 100.|The error message returned when the number of specified deployment sets exceeds 100.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

