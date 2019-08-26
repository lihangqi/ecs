# DetachClassicLinkVpc {#doc_api_1000064 .reference}

Unlinks a classic network-connected instance from the VPC. After the ClassicLink is disabled, the classic network-connected instance cannot access the VPC.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DetachClassicLinkVpc) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId|String|Yes|i-test| The ID of the classic network-connected instance.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region where the instance resides. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|VpcId|String|Yes|vpc-test| The ID of the VPC to which the instance is linked.

 |
|Action|String|No|DetachClassicLinkVpc| The operation that you want to perform. Set the value to DetachClassicLinkVpc.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DetachClassicLinkVpc
&RegionId=cn-hangzhou 
&VpcId=vpc-test
&InstanceId=i-test
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DetachClassicLinkVpcResponse>
  <RequestId>C0003E8B-B930-4F59-ADC0-0E209A9012A8</RequestId>
</DetachClassicLinkVpcResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"C0003E8B-B930-4F59-ADC0-0E209A9012A8"
}
```

## Error codes {#section_dps_n73_kjc .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|InvalidRegionId.Malformed|The specified parameter ? RegionId? is not valid.|The error message returned when the specified region ID is invalid.|
|403|OperationDenied|The instances are not allowed to detach from the linked vpc.|The error message returned when the linked instance cannot be detached from the VPC.|
|403|InvalidStatus.InstanceStatus|The specified instance status is not support this operation ,expect status is running or shutted.|The error message returned when the operation is not supported under the instance state. The expected state is Running or Shutted.|
|403|Forbidden.SubUser|User not authorized to operate on the specified resource.|The error message returned when the RAM user is not authorized to perform operations on this resource.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

