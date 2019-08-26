# DescribeResourcesModification {#DescribeResourcesModification .reference}

Retrieves a list of the resources available in a certain zone. You can use this method before you upgrade or downgrade the instance specifications or the system disk capacity.

## Request parameters {#RequestParameter .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes| The name of this interface. Value: DescribeResourcesModification.|
|RegionId|String|Yes| ID of the target region. For more information, For more information, see Regions and zones, or call [DescribeRegions](intl.en-US/API Reference/Regions/DescribeRegions.md#) to obtain the latest region list.|
|ResourceId|String|Yes|Resource ID. For example, if the retrieved resources are instances, this parameter can be interpreted as InstanceId.|
|DestinationResource|String|Yes|Target resource type. Optional values:-   InstanceType: Instance type
-   SystemDisk: System disk of an instance

|
|MigrateAcrossZone|Boolean|No|Specifies whether to upgrade the instance among different clusters or not. Optional values:-   True
-   False

Default: False. When the `MigrateAcrossZone` is set to `True` and you change the instance configuration according to the returned information, you must make sure that:-   For a classic network type instance:
    -   If you upgrade the [phased-out](https://www.alibabacloud.com/help/faq-detail/55263.htm) non-I/O optimized instances to I/O optimized instances, the instance-related Intranet IP addresses, disk device names and license key of the instance may change. For a Linux instance, the system recognizes basic cloud disk \(`cloud`\) as `xvda`  or  `xvdb`, ultra cloud disk \(`cloud_efficiency`\) and SSD disk \(`cloud_ssd`\) as `vda` or `vdb` .
    -   If your classic network instances are available in the [instance type families](../../../../intl.en-US/Product Introduction/Instance type families.md#), the private IP of the instances may change.
-   For a VPC-Connected instance:

If you upgrade the [phased-out](https://www.alibabacloud.com/help/faq-detail/55263.htm) non-I/O optimized instances to I/O optimized instances, the disk device names and license key of the ECS may change. For a Linux instance,  the system recognizes basic cloud disk \(`cloud`\) as `xvda` or `xvdb`, ultra cloud disk \(`cloud_efficiency`\) and SSD disk \(`cloud_ssd`\) as `vda` or `vdb`.


|
|OperationType|String|No|Whether to upgrade or downgrade your resources. Optional values:-   Upgrade: Upgrade resources
-   Downgrade: Downgrade resources

Default: Upgrade.|
|InstanceType|String|No|Type of an instance. For more information, see [Instance Type Family](../../../../intl.en-US/Product Introduction/Instance type families.md#), or call [DescribeInstanceTypes](intl.en-US/API Reference/Instances/DescribeInstanceTypes.md#) to obtain the latest type list. If you set  `DestinationResource` to `SystemDisk`, you must specify `InstanceType`.|

## Response parameters {#ResponseParameter .section}

|Name|Type|Description|
|:---|:---|:----------|
|AvailableZones|Array of [`AvailableZones`](#AvailableZoneType)|A collection of zone types|

**AvailableZoneType** 

|Name|Type|Description|
|:---|:---|:----------|
|RegionId|String|Region ID.|
|ZoneId|String| Zone ID.|
|Status|String|Resource status. Optional values:-   Available: Resources are available.
-   SoldOut: Resources are unavailable.

|
|AvailableResources|Array of [`AvailableResourcesType`](#AvailableResourcesType)| A collection of available resource types.|

**AvailableResourcesType** 

|Name|Type|Description|
|:---|:---|:----------|
|Type|String|Resource type. Optional values:-   Zone: Zone
-   IoOptimized: Whether the instance is I/O optimized or not.
-   InstanceType: Instance type
-   SystemDisk: System disk
-   DataDisk: Data disk
-   Network: Network type of an instance

|
|SupportedResources|Array of [`SupportedResourcesType`](#SupportedResourcesType)|A collection of supported available resource types|

**SupportedResourcesType** 

|Name|Type|Description|
|:---|:---|:----------|
|Value|String|Name of the Resource.|
|Status|String| Resource status. Optional values:-   Available: Resources are available.
-   SoldOut: Resources are unavailable.

|
|Min|Integer|Minimum limit of the resource. No value is returned if the parameter is null.|
|Max|Integer|Maximum limit of the resource. No value is returned if the parameter is null.|
|Unit|Integer|Resource type unit. No value is returned if the parameter is null.|

## Examples { .section}

**Request example** 

```
https://ecs.aliyuncs.com/?Action=DescribeResourcesModification
&RegionId=cn-hangzhou
&<Common Request Parameters>
```

```
https://ecs.example.com/?Action=DescribeResourcesModification
&RegionId=cn-hangzhou
&<Common Request Parameters>
```

**Response example** 

**XML format**

```
<DescribeResourcesModificationResponse>
    <AvailableZones>
        <AvailableZone>
            <ZoneId>cn-hangzhou-d</ZoneId>
            <RegionId>cn-hangzhou</RegionId>
            <Status>Available</Status>
            <AvailableResources>
                <AvailableResource>
                    <Type>instanceType</Type>
                    <SupportedResources>
                        <SupportedResource>
                            <Value>ecs.d1ne.xlarge</Value>
                            <Status>Available</Status>
                        </SupportedResource>
                         <SupportedResource>
                            <Value>ecs.d1ne. 2xlarge</Value>
                            <Status>Available</Status>
                        </SupportedResource>
                    </SupportedResources>
                </AvailableResource>
            </AvailableResources>
        </AvailableZone>
        <AvailableZone>
            <ZoneId>cn-hangzhou-e</ZoneId>
            <RegionId>cn-hangzhou</RegionId>
            <Status>Available</Status>
            <AvailableResources>
                <AvailableResource>
                    <Type>instanceType</Type>
                    <SupportedResources>
                        <SupportedResource>
                            <Value>ecs.d1ne.xlarge</Value>
                            <Status>Available</Status>
                        </SupportedResource>
                         <SupportedResource>
                            <Value>ecs.d1ne. 2xlarge</Value>
                            <Status>Available</Status>
                        </SupportedResource>
                    </SupportedResources>
                </AvailableResource>
            </AvailableResources>
        </AvailableZone>
    </AvailableZones>
    <RequestId>6DB97BCC-92BA-424D-A7C8-3F6486612BAE</RequestId>
</DescribeResourcesModificationResponse>
```

 **JSON format** 

```

    "RequestId": "D0233A65-7F00-4B50-8023-101427229D4F",
    "AvailableZones": {
        "AvailableZone": [
            
                "Status": "available",
                "RegionId": "cn-hangzhou",
                "AvailableResources": {
                    "AvailableResource": [
                        
                            "Type": "instanceType",
                            "SupportedResources": {
                                "SupportedResource": [
                                    
                                        "Status": "available",
                                        "Value": "ecs.sn1ne.xlarge"
                                    
                                    
                                        "Status": "available",
                                        "Value": "ecs.sn2ne.xlarge"
                                    
                                
                            
                        
                    
                
                "ZoneId": "cn-hangzhou-e",
            
        
    

```

## Error codes {#ErrorCode .section}

The following error codes are restricted to this interface.  For more error codes, see [API Error Center](https://error-center.alibabacloud.com/status/product/Ecs).

|Error code|Error information|HTTP status code|Description|
|:---------|:----------------|:---------------|:----------|
|Invalid.Param|The input parameter DestinationResource that is mandatory for processing this request is not supplied.|400|You must specify the parameter `DestinationResource`.|
|Unavailable.Regions|The available regions does not exists.|404|The specified `RegionId` is unavailable.|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|The specified `RegionId` does not exist.|

