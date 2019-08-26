# AllocatePublicIpAddress {#doc_api_999740 .reference}

Assigns a public IP address to an instance.

## Description {#description .section}

When you call this operation, note that:

-   Before you can assign a public IP address to an instance, the instance must be in the Running or Stopped state.
-   No public IP addresses can be assigned to a VPC-connected instance bound with an Elastic IP \(EIP\).
-   You can assign only one public IP address to an instance. If an instance has a public IP address, the AllocatedAlready error message is returned.
-   After you restart an instance \([RebootInstance](~~25502~~)\) or start an instance \([StartInstance](~~25500~~)\), the new public IP address takes effect.
-   If an instance is [locked for security reasons](~~25695~~) \(the OperationLocks parameter is "LockReason": "security"\), no public IP addresses can be assigned to the instance.

You can also bind an EIP to an instance. For more information, see [AssociateEipAddress](~~36017~~).

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=AllocatePublicIpAddress) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|InstanceId|String|Yes|i-instance1| The ID of the instance to be allocated an IP address.

 |
|Action|String|No|AllocatePublicIpAddress| The operation that you want to perform. Set the value to AllocatePublicIpAddress.

 |
|IpAddress|String|No|10.1.149.159| The public IP address of an instance.

 |
|VlanId|String|No|100| The VLAN ID.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|IpAddress|String|10.1.149.159| The public IP address of an instance.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=AllocatePublicIpAddress
&InstanceId=i-instance1
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<AllocatePublicIpAddressResponse>
  <RequestId>F2EF6A3B-E345-46B9-931E-0EA094818567</RequestId>
   <IpAddress>10.1.149.159</IpAddress>
</AllocatePublicIpAddressResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId": "F2EF6A3B-E345-46B9-931E-0EA094818567",
	"IpAddress": "10.1.149.159"
}
```

## Error codes {#section_9cs_lih_ams .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidVlanId. NotFound|The VlanId provided does not exist in our records.|The error message returned when the ID of the specified VLAN does not exist.|
|403|InstanceExpiredOrInArrears|The specified operation is denied as your prepay instance is expired \(prepay mode\) or in arrears \(afterpay mode\).|The error message returned when the subscription of an instance has expired. You need to renew the subscription before proceeding.|
|404|InvalidIpAddress. NotFound|The specified IP is not in the specified vlan.|The error message returned when the specified IP address is not in the specified VLAN.|
|403|AllocatedAlready|There is an IpAddress allocated already for the specified instance.|The error message returned when you try to assign a specified IP address to an instance that already has an IP address.|
|400|OperationDenied|Specified operation is denied as your instance is in VPC.|The error message returned when the specified operation does not support VPC-connected instances.|
|400|AllocateIpInvalidInstanceBandwidth|OperationDenied The InternetMaxBandwidthOut of the specified instance cannot be less than 0.|The error message returned when the Internet bandwidth is less than 0.|
|400|OperationDenied|The specified parameter "VlanId" is not valid or vlan has not enough IP address.|The error message returned when the specified VLAN ID is invalid or the number of IP addresses in the VLAN reaches the upper limit.|
|403|NAT\_PUBLIC\_IP\_BINDING\_FAILED|Binding nat public ip failed|The error message returned when you fail to bind a public IP address to an instance.|
|403|NAT\_PUBLIC\_IP\_ALLOCATE\_FAILED|Nat public ip binding failed.|The error message returned when ECS fails to assign a public IP address to an instance.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

