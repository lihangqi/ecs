# DescribeResourcesModification {#doc_api_1105039 .reference}

Views the resources available in a zone before reconfiguring the instance specifications or the system disk capacity.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeResourcesModification) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|DestinationResource|String|Yes|InstanceType| The type of the target resource. Valid values:

 -   InstanceType
-   SystemDisk

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the target region. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|ResourceId|String|Yes|i-instanceid| The ID of the resource. When the retrieved resources are instances, this parameter can be interpreted as InstanceId.

 |
|Action|String|No|DescribeResourcesModification| The operation that you want to perform. Set the value to DescribeResourcesModification.

 |
|Cores|Integer|No|2| The number of vCPU cores of the instance type. For more information, see [Instance type families](~~25378~~). The Cores parameter is valid only when the DestinationResource parameter is set to InstanceType.

 |
|InstanceType|String|No|ecs.g5.large| The type of the instance. For more information, see [Instance type families](~~25378~~), or call [DescribeInstanceTypes](~~25620~~) to query the latest instance types. When the DestinationResource parameter is set to SystemDisk, you must specify the InstanceType parameter.

 |
|Memory|Float|No|8.0| The memory size of the instance type. Unit: GiB. For more information, see [Instance type families](~~25378~~). The Memory parameter is valid only when the DestinationResource parameter is set to InstanceType.

 |
|MigrateAcrossZone|Boolean|No|true| Indicates whether instance specifications can be upgraded across clusters. Valid values:

 -   True
-   False

 Default value: False.

 When the MigrateAcrossZone parameter is set to True, and you upgrade the ECS instance based on the returned information, you must make sure that:

 -   Instances of classic network:
    -   For [phased-out instance types](~~55263~~), when a non-I/O optimized instance is upgraded to an I/O optimized instance, the instance information, including the private IP address, software authorization code, and the device name of the disk, will be changed. For Linux-based instances, device names of basic disks \(cloud\) will be changed to the form of xvda or xvdb, while device names of ultra disks \(cloud\_efficiency\) and SSDs \(cloud\_ssd\) are changed to the form of vda or vdb.
    -   For [available instance types](~~25378~~), the private IP address of the instance will be changed.
-   VPC-type instances: For [phased-out instance types](~~55263~~), when a non-I/O optimized instance is upgraded to an I/O optimized instance, the instance information, including the software authorization code and the device name of the disk, will be changed. For Linux-based instances, device names of basic disks \(cloud\) will be changed to the form of xvda or xvdb, while device names of ultra disks \(cloud\_efficiency\) and SSDs \(cloud\_ssd\) are changed to the form of vda or vdb.

 |
|OperationType|String|No|Upgrade| The operation types for the Subscription-based instance. Valid values:

 -   Upgrade
-   Downgrade
-   RenewDowngrade
-   RenewModify

 Default value: Upgrade.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|AvailableZones| | | An array of zone types.

 |
|└AvailableResources| | | An array of available resource types.

 |
|└SupportedResources| | | A collection of supported resource types.

 |
|└Max|Integer|2| The maximum value of the resource type. No value is returned when this parameter is null.

 |
|└Min|Integer|1| The minimum value of a resource type. No value is returned when the parameter is null.

 |
|└Status|String|Available| The status of the resource. Valid values:

 -   Available
-   SoldOut

 |
|└StatusCategory|String|WithStock| The resource category based on the stock. Valid values:

 -   WithStock: sufficient stock
-   ClosedWithStock: insufficient stock
-   WithoutStock: running out of stock

 |
|└Unit|String|null| The unit of the resource type. No value is returned when the parameter is null.

 |
|└Value|String|ecs.sn1ne.xlarge| The value of the resource.

 |
|└Type|String|InstanceType| The type of the resource. Valid values:

 -   Zone
-   IoOptimized
-   InstanceType
-   SystemDisk
-   DataDisk
-   Network

 |
|└RegionId|String|cn-hangzhou| The ID of the region.

 |
|└Status|String|Available| The status of the resource. Valid values:

 -   Available
-   SoldOut

 |
|└StatusCategory|String|WithStocK| The resource category based on the stock. Valid values:

 -   WithStock: sufficient stock
-   ClosedWithStock: insufficient stock
-   WithoutStock: running out of stock

 |
|└ZoneId|String|cn-hangzhou-e| The ID of the zone.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeResourcesModification
&DestinationResource=InstanceType
&RegionId=cn-hangzhou
&ResourceId=i-instanceid 
&MigrateAcrossZone=true 
&OperationType=Upgrade 
&InstanceType=["ecs.g5.large"] 
&Cores=2 
&Memory=8.0 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeResourcesModificationResponse> 
  <RequestId>994F2B60-B050-49E3-9283-44655FAC7A4X</RequestId> 
  <AvailableZones> 
    <AvailableZone> 
      <Status>Available</Status> 
      <RegionId>cn-hangzhou-dg-a01</RegionId> 
      <AvailableResources> 
        <AvailableResource> 
          <Type>InstanceType</Type> 
          <SupportedResources> 
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.g5.xlarge</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.t5-lc1m2.large</Value>
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.t5-c1m4.2xlarge</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.c5.xlarge</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.hfg5.large</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.hfc5.3xlarge</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.hfg5.4xlarge</Value> 
            </SupportedResource> 
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.hfg5.6xlarge</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.c5.4xlarge</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.t5-c1m2.xlarge</Value>
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.t5-c1m1.2xlarge</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.ic5.xlarge</Value>
            </SupportedResource>
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.t5-lc1m4.large</Value> 
            </SupportedResource> 
            <SupportedResource>
              <Status>Available</Status> 
              <Value>ecs.hfg5.3xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.t5-c1m2.4xlarge</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.ic5.3xlarge</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status> 
              <Value>ecs.g5.6xlarge</Value>
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.ic5.large</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.ic5.2xlarge</Value>
            </SupportedResource>
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.hfc5.large</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.r5.large</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status> 
              <Value>ecs.g5.large</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.hfg5.xlarge</Value> 
            </SupportedResource> 
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.r5.4xlarge</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.hfc5.xlarge</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.hfc5.4xlarge</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.t5-lc1m2.small</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status> 
              <Value>ecs.t5-c1m1.large</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.g5.2xlarge</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.r5.6xlarge</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status> 
              <Value>ecs.t5-c1m2.2xlarge</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status> 
              <Value>ecs.g5.3xlarge</Value>
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status> 
              <Value>ecs.t5-c1m1.xlarge</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status> 
              <Value>ecs.hfc5.6xlarge</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status>
              <Value>ecs.t5-c1m4.xlarge</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status> 
              <Value>ecs.hfg5.2xlarge</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status> 
              <Value>ecs.hfc5.2xlarge</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status> 
              <Value>ecs.c5.large</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status> 
              <Value>ecs.c5.6xlarge</Value> 
            </SupportedResource> 
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.t5-c1m4.large</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status> 
              <Value>ecs.r5.2xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status> 
              <Value>ecs.r5.xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status> 
              <Value>ecs.c5.3xlarge</Value> 
            </SupportedResource> 
            <SupportedResource> 
              <Status>Available</Status> 
              <Value>ecs.ic5.4xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.t5-lc1m1.small</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.c5.2xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.t5-c1m1.4xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.t5-lc2m1.nano</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.g5.4xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.r5.3xlarge</Value>
            </SupportedResource>
            <SupportedResource>
              <Status>Available</Status>
              <Value>ecs.t5-c1m2.large</Value>
            </SupportedResource>
          </SupportedResources> 
        </AvailableResource>
      </AvailableResources>
      <ZoneId>cn-hangzhou-h</ZoneId>
    </AvailableZone>
  </AvailableZones>
</DescribeResourcesModificationResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"994F2B60-B050-49E3-9283-44655FAC7A4X",
	"AvailableZones":{
		"AvailableZone":[
			{
				"Status":"Available",
				"RegionId":"cn-hangzhou-dg-a01",
				"AvailableResources":{
					"AvailableResource":[
						{
							"Type":"InstanceType",
							"SupportedResources":{
								"SupportedResource":[
									{
										"Status":"Available",
										"Value":"ecs.g5.xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-lc1m2.large"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-c1m4.2xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.c5.xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfg5.large"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfc5.3xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfg5.4xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfg5.6xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.c5.4xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-c1m2.xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-c1m1.2xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.ic5.xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-lc1m4.large"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfg5.3xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-c1m2.4xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.ic5.3xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.g5.6xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.ic5.large"
									},
									{
										"Status":"Available",
										"Value":"ecs.ic5.2xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfc5.large"
									},
									{
										"Status":"Available",
										"Value":"ecs.r5.large"
									},
									{
										"Status":"Available",
										"Value":"ecs.g5.large"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfg5.xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.r5.4xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfc5.xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfc5.4xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-lc1m2.small"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-c1m1.large"
									},
									{
										"Status":"Available",
										"Value":"ecs.g5.2xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.r5.6xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-c1m2.2xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.g5.3xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-c1m1.xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfc5.6xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-c1m4.xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfg5.2xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.hfc5.2xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.c5.large"
									},
									{
										"Status":"Available",
										"Value":"ecs.c5.6xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-c1m4.large"
									},
									{
										"Status":"Available",
										"Value":"ecs.r5.2xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.r5.xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.c5.3xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.ic5.4xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-lc1m1.small"
									},
									{
										"Status":"Available",
										"Value":"ecs.c5.2xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-c1m1.4xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-lc2m1.nano"
									},
									{
										"Status":"Available",
										"Value":"ecs.g5.4xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.r5.3xlarge"
									},
									{
										"Status":"Available",
										"Value":"ecs.t5-c1m2.large"
									}
								]
							}
						}
					]
				},
				"ZoneId":"cn-hangzhou-h"
			}
		]
	}
}
```

## Error codes {#section_48j_w4u_oo2 .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|Invalid.RegionId|The specified RegionId does not exist.|The error message returned when the RegionId parameter is invalid.|
|400|Invalid.OperationType|The specified operationType is not valid.|The error message returned when the operationType parameter is invalid.|
|400|Invalid.Param|The input parameter DestinationResource that is mandatory for processing this request is not supplied.|The error message returned when the DestinationResource parameter is invalid.|
|404|Invalid.ResourceType|The ResourceType provided does not exist in our records.|The error message returned when the ResourceType parameter is invalid.|
|404|Invalid.DestinationResource|The specified DestinationResource is not valid.|The error message returned when the DestinationResource parameter is invalid.|
|404|Invalid.IoOptimized|The specified IoOptimized is not valid.|The error message returned when the IoOptimized parameter is invalid.|
|404|Invalid.NetworkCategory|The specified NetworkCategory is not valid.|The error message returned when the NetworkCategory parameter is invalid.|
|404|Invalid.SpotStrategy|The specified SpotStrategy is not valid.|The error message returned when the SpotStrategy parameter is invalid.|
|400|Invalid.InstanceChargeType|The specified InstanceChargeType is not valid.|The error message returned when the InstanceChargeType parameter is invalid.|
|404|Invalid.ResourceId|The specified ResourceId is not valid.|The error message returned when the resource does not exist in the region or has been released.|
|404|Invalid.InstancePayType|The specified InstancePayType is not valid.|The error message returned when the InstancePayType parameter is invalid.|
|403|InvalidDedicatedHostId.NotFound|The specified DedicatedHostId does not exist in our records.|The error message returned when the resource does not exist in the region or has been released.|
|404|InvalidInstanceId.NotFound|The specified InstanceId provided does not exist in our records.|The error message returned when the resource does not exist in the region or has been released.|
|404|InvalidResourceId.NotFound|The specified ResourceId is not found in our records|The error message returned when the specified ResourceId does not exist.|
|403|InvalidParam.TypeAndCpuMem.Conflict|The specified 'InstanceType' and 'Cores','Memory' are not blank at the same time.|The error message returned when the specified ResourceId does not exist.|
|403|InvalidParam.Cores|The specified parameter 'Cores' should be empty|The error message returned when the Cores parameter is invalid.|
|403|InvalidParam.Memory|The specified parameter 'Memory' should be empty|The error message returned when the resource does not exist in the region or has been released.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

