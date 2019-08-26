# AttachNetworkInterface  {#AttachNetworkInterface .reference}

Attaches an ENI \(Elastic Network Interface\) to a VPC-Connected instance.

## Description  {#section_wwz_f34_ydb .section}

-   The ENI must be in the **Available** \(`Available`\) status.

-   The instance must be in the **Stopped** \(`Stopped`\) or **Running** \(`Running`\) status.

-   You can only attach one ENI to a VPC-Connected instance, and the ENI must be in the same VPC as the instance.

-   One ENI can only be attached to one instance.

-   One instance can be attached with multiple ENIs at the same time. See [Elastic network interfaces](../../../../intl.en-US/Product Introduction/Network and security/Elastic network interfaces.md#) for the number of ENIs allowed to be attached for each instance type.

-   Since you cannot deploy VSwitches from different zones into one VPC, an ENI attached to the instance must be in the same zone as the VSwitch to which the ENI belongs.


## Request parameters {#RequestParameter .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: attachnetworkinterface.|
|RegionId|String|Yes|ID of the region of the ECS instance. For more information, call [DescribeRegions](intl.en-US/API Reference/Regions/DescribeRegions.md#) to obtain the latest region list.|
|NetworkInterfaceId|String|Yes|ENI ID.|
|InstanceId|String|Yes|Instance ID.|

## Response parameters {#section_f54_lk5_xdb .section}

For more information about all the common response parameters, see [Common parameters](intl.en-US/API Reference/Call methods/Common parameters.md#).

## Examples { .section}

**Request example** 

```
https://ecs.aliyuncs.com/?Action=AttachNetworkInterface
&RegionId=cn-hangzhou
&NetworkInterfaceId=[networkInterfaceId]
&InstanceId=AY121018033933eae8xxxxx
&<Common Request Parameters>
```

**Response example** 

**XML format**

```
<AttachNetworkInterfaceResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
</AttachNetworkInterfaceResponse>
```

 **JSON format** 

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FExxxxx"
}
```

## Error codes {#ErrorCode .section}

The following error codes are specific to this interface. For more error codes, visit the [API error center](https://error-center.alibabacloud.com/status/product/Ecs).

|Error code|Error message|HTTP status code|Description|
|:---------|:------------|:---------------|:----------|
|UnsupportedParameter|The parameters is unsupported.|400|The specified parameter does not exist. Alternatively, the specified parameter is not supported.|
|InvalidOperation.InvalidEcsState|The operation is not allowed in the current ECS state.|400|The specified action failed due to the status of the instance.|
|InvalidOperation.DetachPrimaryEniNotAllowed|Detaching primary ENI from ECS instance is not allowed.|400|You cannot detach the primary network interface from an ECS instance.|
|MissingParameter|The input parameter that is mandatory for processing this request is not supplied.|400|You must specify the required parameters.|
|Abs.InvalidAccount.NotFound|The Account is not found or AK is expired.|403|The specified Alibaba Cloud account does not exist. Alternatively, your AccessKey expired.|
|Forbidden.NotSupportRAM|This action does not support accessed by RAM mode.|403|A RAM user is limited to access the resource.|
|Forbidden.SubUser|The specified action is not available for you.|403|A RAM user is limited to access the resource.|
|EniPerInstanceLimitExceeded|The number of ENI exceeds the limit for the type of instance you are trying to launch.|403|For the specified type of ECS instance, the maximum number of ENI is exceeded.|
|InvalidOperation.VpcMismatch|The VPC of the specified ENI and security group are not in the same VPC.|403|The specified ENI and SecurityGroupId are not in the same VPC.|
|SecurityGroupInstanceLimitExceed|The maximum number of instances in a security group is exceeded.|403|The maximum number of instance in the specified SecurityGroupId is exceeded.|
|InvalidOperation.InvalidEniType|The operation is not allowed in the current ENI type.|403|The specified action failed due to the type of the ENI.|
|InvalidEcsId.NotFound|The specified EcsId is not found.|404|The specified InstanceId does not exist.|

