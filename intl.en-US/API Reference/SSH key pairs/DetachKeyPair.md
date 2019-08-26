# DetachKeyPair {#doc_api_999668 .reference}

Detaches SSH key pairs from one or multiple Linux-based instances.

## Description {#description .section}

When you call this operation, note that:

-   After you detach an SSH key pair, you must restart the instance \([RebootInstance](~~25502~~)\) for the operation to take effect.
-   After an SSH key pair is detached from an instance, the account-password authentication method is used by default.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DetachKeyPair) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceIds|String|Yes|\["d-xxxxxxxxx", "d-yyyyyyyyy", … "d-zzzzzzzzz"\]| The IDs of instances from which SSH key pairs are detached. The value can be a JSON array consisting of up to 50 instance IDs. Multiple IDs must be separated by commas \(,\).

 |
|KeyPairName|String|Yes|FinanceJoshuaV26| The SSH key pair names.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region where an SSH key pair resides. You can call [DescribeRegions](~~25609~~) to view the latest list of Alibaba Cloud regions.

 |
|Action|String|No|DetachKeyPair| The operation that you want to perform. Set the value to DetachKeyPair.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|FailCount|String|0| The number of instances from which key pairs fail to be detached.

 |
|KeyPairName|String|FinanceJoshuaV26| The name of a key pair.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |
|Results| | | The result set of detach operation.

 |
|└Code|String|200| The operation status code returned. 200 indicates that the operation is successful.

 |
|└InstanceId|String|i-instanceid1| The ID of an instance.

 |
|└Message|String|successful| The operation information returned. When the value of code is 200, the value of message is successful.

 |
|└Success|String|true| The message returned indicating whether the operation is successful.

 |
|TotalCount|String|2| The total number of instances from which key pairs are detached.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DetachKeyPair
&RegionId=cn-qingdao
&InstanceIds=["i-xxxxxxx", "i-yyyyyyy"]
&KeyPairName=test
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DetachKeyPairResponse>
  <TotalCount>2</TotalCount>
   <RequestId>834B3E6B-2D1D-482F-81A4-810C327D4735</RequestId>
  <Results>
    </Result>
      <Message>AccessDenied</Message>
      <InstanceId>i-m5eg7be9ndloji64jknv</InstanceId>
      <Success>true</Success>
      <Code>200</Code>
    </Result>
    </Result>
      <Message>successful</Message>
      <InstanceId>i-m5e25x2mwr0hk33dwv0h</InstanceId>
      <Success>true</Success>
      <Code>200</Code>
    </Result>
  </Results>
  <FailCount>0</FailCount>
 </DetachKeyPairResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"TotalCount":2,
	"RequestId":"834B3E6B-2D1D-482F-81A4-810C327D4735",
	"Results":{
		"Result":[
			{
				"Message":"successful",
				"InstanceId":"i-m5eg7be9ndloji64jknv",
				"Success":true,
				"Code":"200"
			},
			{
				"Message":"successful",
				"InstanceId":"i-m5e25x2mwr0hk33dwv0h",
				"Success":true,
				"Code":"200"
			}
		]
	},
	"FailCount": 0
}
```

## Error codes {#section_w9q_s3a_fyh .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|DependencyViolation.WindowsInstance|The instance creating is windows, cannot use ssh key pair to login|The error message returned when you cannot detach key pairs from the specified Windows-based instance.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

