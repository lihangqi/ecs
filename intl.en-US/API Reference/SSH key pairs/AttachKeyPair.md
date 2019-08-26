# AttachKeyPair {#doc_api_999669 .reference}

Attaches an SSH key pair to one or multiple Linux-based instances.

## Description {#description .section}

When you call this operation, note that:

-   SSH key pairs are not supported on Windows-based instances.
-   Once an SSH key pair is attached to an instance, the username-password authentication method is disabled on the instance.
-   If an instance is in the Running state, call [RebootInstance](~~25502~~) to restart the instance for the operation to take effect.
-   If an instance is in the Stopped state, call [StartInstance](~~25500~~) to start the instance for the operation to take effect.
-   If an instance already has an SSH key pair attached, the new SSH key pair will automatically replace the original one.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=AttachKeyPair) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceIds|String|Yes|\["i-xxxxxxxxx", "i-yyyyyyyyy", … "i-zzzzzzzzz"\]| The IDs of instances to which you want to attach an SSH key pair. The value can contain a JSON array consisting of up to 50 instance IDs. The IDs must be separated by commas \(,\).

 |
|KeyPairName|String|Yes|FinanceJoshuaV25| The name of the SSH key pair.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region where the SSH key pair resides. You can call [DescribeRegions](~~25609~~) to view the latest list of Alibaba Cloud regions.

 |
|Action|String|No|AttachKeyPair| The operation that you want to perform. Set the value to AttachKeyPair.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|FailCount|String|0| The number of instances to which key pairs fail to be attached.

 |
|KeyPairName|String|FinanceJoshuaV25| The name of a key pair.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|Results| | | The result set of attachment operations.

 |
|└Code|String|200| The operation status code returned. 200 indicates that the operation is successful.

 |
|└InstanceId|String|i-instanceid1| The ID of an instance.

 |
|└Message|String|successful| The operation information returned. When the value of code is 200, the value of message becomes successful.

 |
|└Success|String|true| The message returned indicating whether the operation is successful.

 |
|TotalCount|String|2| The total number of instances to which key pairs are bound.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=AttachKeyPair
&InstanceIds=["i-xxxxxxxxx", "i-yyyyyyyyy", … "i-zzzzzzzzz"]
&KeyPairName=FinanceJoshuaV25
&RegionId=cn-hangzhou 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<AttachKeyPairResponse>
  <TotalCount>2</TotalCount>
  <RequestId>4ADF7A06-66BD-4FBF-A2ED-2364E41D8C06</RequestId><RequestId> 4ADF7A06-66BD-4FBF-A2ED-2364E41D8C06 </RequestId>
  <Results>
    </Result>
      <Message>AccessDenied</Message>
       <InstanceId>i-m5eg7be9ndloji64jknv</InstanceId>
      <Success>true</Success>
      <Code>200</Code>
    </Result>
    </Result>
      <Message>AccessDenied</Message>
       <InstanceId>i-m5e25x2mwr0hk33dwv0h</InstanceId>
      <Success>true</Success>
      <Code>200</Code>
    </Result>
  </Results>
  <FailCount>0</FailCount>
</AttachKeyPairResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"TotalCount":2,
	"RequestId":"4ADF7A06-66BD-4FBF-A2ED-2364E41D8C06",
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
	"FailCount":0
}
```

## Error codes {#section_s4h_p03_tem .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|DependencyViolation.WindowsInstance|The instance creating is windows, cannot use ssh key pair to login|The error message returned when you cannot detach key pairs from the specified Windows-based instance.|
|400|DependencyViolation.IoOptimize|The specified parameter InstanceIds is not valid.|The error message returned when the specified instance ID is invalid.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

