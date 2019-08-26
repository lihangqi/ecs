# ModifyInstanceVpcAttribute {#ModifyInstanceVpcAttribute .reference}

Modifies the attributes of a Virtual Private Cloud \(VPC\).

## Description {#section_pgl_44t_xdb .section}

-   The ECS instance must be in the `Stopped` status before the VSwitch can be changed.
-   A new instance must have been started and stopped before you call this interface.
-   An ECS instance that has successfully modified the VPC properties must have been started and stopped before you call this interface again.
-   When VPC attributes are modified for a specified `VSwitchId`, the `VSwitchId` must belong to the same VPC.
-   When `VSwitchId` is specified and `PrivateIpAddress` is not specified, the system automatically allocates a private IP address for your ECS instance.
-   The current `VSwitchId` and new VSwitch of the specified instance must belong to the same zone.
-   The current VSwitch and new `VSwitchId` of the specified instance must belong to the same VPC.
-   When both `VSwitchId` and `PrivateIpAddress` are specified, the specified PrivateIpAddress must be in the [network segment](../../../../../reseller.en-US/Product Introduction/What is VPC?.md#section_w1b_tvz_ndb) of the specified VSwitch. The value of `PrivateIpAddress` depends on `VSwitchId`. You must specify the VSwitchId when you modify the `PrivateIpAddress` of your instance.

## Request parameters {#RequestParameter .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: modifyinstancevpcattribute.|
|InstanceId|String|Yes.|Instance Id.|
|VSwitchId|String|Yes.|New VSwitch Id. Only `VSwitchId` in the same zone of the previous VSwitch can be selected.|
|Privateipaddress|String|No|New private IP addresses of your instance. The value of `PrivateIpAddress` depends on the `VSwitchId`. You must specify the VSwitch when you modify the `PrivateIpAddress` of your instance.|

## Response parameters {#section_zgl_44t_xdb .section}

All parameters are common response parameters. For more information, see [Common parameters](reseller.en-US/API Reference/Getting started/Common parameters.md#commonResponseParameters).

## Examples { .section}

**Request example** 

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceVpcAttribute
&InstanceId=35F20777-0DFF-C152-41FA-BCE0EA0B2FD7
&VSwitchId=[vswitchid]
&<Common Request Parameters>
```

**Response example** 

**XML format**

```
<ModifyInstanceAttributeResponse>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyInstanceAttributeResponse>
```

 **JSON format** 

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes {#ErrorCode .section}

|Error code|Error message|HTTP status code|Description|
|:---------|:------------|:---------------|:----------|
|Incorrectinstancestatus|The current status of instance does not support this operation.|400|Only an instance in `Stopped` status supports this operation.|
|InvalidPrivateIp.Changing|Previous action is not finished yet.|400|The private IP address cannot be modified because the previous modification is not finished yet.|
|InvalidPrivateIp.Changing|Specified private IP address is not in the CIDR block of virtual switch.|400|The private IP address is being modified by the instance \(the private IP address can be modified only when the instance is stopped\).|
|InvalidPrivateIpAddress.Duplicated|Specified private IP address is duplicate.|400|The specified private IP address is already in use.|
|InvalidPrivateIpAddress.Malformed|Specified private IP address is malformed.|400|The specified private IP address is invalid.|
|InvalidPrivateIpAddress.Mismatch|Specified private IP address is not in the CIDR block of virtual switch.|400|The specified private IP address is not in the network segment of the specified VSwitch.|
|InvalidVSwitchId.Mismatch|Specified instance and virtual switch are not in the same zone.|400|The specified instance and `VSwitchId` are not in the same zone.|
|OperationDenied|Specified operation is denied as your instance is not in VPC.|400|The network type for the specified instance must be VPC.|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|The specified ECS instance does not exist.|
|InvalidVSwitchId. NotFound|Specified virtual switch does not exist.|404|The specified VSwitch ID does not exist.|
|InvalidVSwitchId.NotFound|Specified virtual switch is not found in current VPC.|404|The specified VSwitch of the instance cannot be modified because it is not found in the current VPC.|

