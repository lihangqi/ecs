# DescribeInstances {#DescribeInstances .reference}

Describes the details of one or more instances.

## Description {#section_phb_mrs_xdb .section}

The request parameters are filters used for describing a specific list of results. The filters use the \(`AND`\) logic, which matches a set of resources by specific criteria, such as IDs, billing methods, or tags. A parameter with null value does not play the role of a filter. However, if the `InstanceIds` parameter is a null JSON array `InstanceIds=[]`, it is regarded as a valid filter and the responded value is null.

## Request parameters {#RequestParameter .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: Description instances.|
|RegionId|String|No|Regional ID. For more information, call [DescribeRegions](../reseller.en-US/API Reference/Regions/DescribeRegions.md#) to obtain the latest region list.|
|VpcId|String|No|VPC ID. |
|VSwitchId|String|No|VSwitch ID.|
|ZoneId|String|No|The default value is blank, which indicates a query of disks in all zones.|
|InstanceIds|String|No|Instance ID. The value can contain an array of up to 100 instance IDs. The IDs are displayed in the format of \["i-xxxxxxxxx", "i-yyyyyyyyy", … "i-zzzzzzzzz"\] and are separated by commas \(`,`\).|
|InstanceType|String|No|Instance type.|
|CreditSpecification|String|No| The running mode of an unlimited credit enabled t5 instance. Optional values:

 -   Standard: The standard running mode. For more information, see [t5 standard instances](../reseller.en-US/Instances/Instance type families/Burstable performance instances/t5 standard instances.md#).
-   Unlimited: The unlimited running mode. For more information, see [t5 unlimited instances](../reseller.en-US/Instances/Instance type families/Burstable performance instances/t5 unlimited instances.md#).

 Default value: null.

 |
|InstanceTypeFamily|String|No|Instance type family.|
|InstanceNetworkType|String|No|Network type of the instance. Optional values:-   classic: Classic network.
-   vpc: Private network.

|
|PrivateIpAddresses|String|No|List of private IP addresses of VPC-Connected instances. This parameter is effective when `InstanceNetworkType=vpc`. The value can contain an array of up to 100 IP addresses. The IP addresses are displayed in the format of \["172.16.1.1", "172.16.2.1", … "172.16.10.1"\] and are separated by commas \(`,`\).|
|InnerIpAddresses|String|No|List of private IP addresses of classic network-connected instances. This parameter is effective when `InstanceNetworkType=classic`. The value can contain an array of up to 100 IP addresses. The IP addresses are displayed in the format of \["10.16.1.1", "10.16.2.1", … "10.16.10.1"\] and are separated by commas \(`,`\).|
|PublicIpAddresses|String|No|List of public IP addresses of classic network-connected instances. The PublicIpAddresses is valid when `InstanceNetworkType=classic`. The value can contain an array of up to 100 IP addresses. The IP addresses are displayed in the format of \["42.1.1.1", "42.1.2.1", … "42.1.10.1"\] and are separated by commas \(`,`\).|
|SecurityGroupId|String|No|Security group to which the instances belong.|
|InstanceChargeType|String|No|Billing method of the instances. Optional values:-   PrePaid: Subscribed instances.
-   PostPaid: Pay-As-You-Go instances.

|
|SpotStrategy|String|No|The spot price you are willing to accept for preemptible instances. This parameter is effective for `InstanceChargeType=PostPaid`. Optional values:-   NoSpot: A normal Pay-As-You-Go instance.
-   SpotWithPriceLimit: Sets the maximum price for a spot instance.
-   SpotAsPriceGo: A price that is based on the highest Pay-As-You-Go instance.

Default value: NoSpot.|
|InternetChargeType|String|No|Billing method of the instance bandwidth. Optional values:-   PayByTraffic: You are billed based on the traffic.

|
|InstanceName|String|No|The name of the instance. You can use wildcard \(\*\) for fuzzy search.|
|ImageId|String|No|Image ID.|
|DeploymentSetId|String|No|Deployment Set ID.|
|Status|String|No|Status of the instances. Optional values:-   Running
-   Starting
-   Stopping
-   Stopped

|
|IoOptimized|String|No|Whether an instance is I/O optimized. Optional values:-   true
-   false

|
|Tag.n.Key|String|No|The key of a tag of which n is from 1 to 20. Once you use this parameter, it cannot be a null string. It can be up to 64 characters in length. It cannot begin with "aliyun", "acs:", "http://", or "https://".|
|Tag.n.Value|String|No|The value of a tag of which n is a number from 1 to 20. Once you use this parameter, it can be a null string. It can be up to 128 characters in length. It cannot begin with "aliyun", "acs:", "http://", or "https://".|
|PageNumber|Integer|No|Displays the instances on several pages. Start value: 1.Default: 1.

|
|PageSize|Integer|No|The number of rows per page. Maximum value: 100Default: 10.

|

## Response parameters {#ResponseParameter .section}

|Name|Type|Description|
|:---|:---|:----------|
|TotalCount|Integer|Total number of instances.|
|PageNumber|Integer|Page number of the instance list.|
|PageSize|Integer|Number of lines per page set during input.|
|Instances|[InstanceAttributesType](reseller.en-US/API Reference/Data type/InstanceAttributesType.md#)|Array format composed of InstanceAttributesType, which returns instance information.|

## Examples { .section}

**Request example** 

```
https://ecs.aliyuncs.com/?Action=DescribeInstances
&RegionId=cn-hangzhou
&<Common Response Parameters>
```

**Response example** 

**XML format**

```
<DescribeInstancesResponse>
  <PageNumber>1</PageNumber>
  <TotalCount>6</TotalCount>
  <PageSize>10</PageSize>
  <RequestId>8EF01A45-FFFA-497B-B5C3-1DE1B74DB32D</RequestId>
  <Instances>
    <Instance>
      <InnerIpAddress/>
      <ImageId>ubuntu_16_0402_64_20G_alibase_20170818.vhd</ImageId>
      <InstanceTypeFamily>ecs.g5</InstanceTypeFamily>
      <VlanId/>
      <NetworkInterfaces>
        <NetworkInterface>
          <MacAddress>00:16:3e:32:b4:dc</MacAddress>
          <PrimaryIpAddress>172.17. XX.XXX</PrimaryIpAddress>
          <NetworkInterfaceId>eni-2zeh9atclduxvf1zcyal</NetworkInterfaceId>
        </NetworkInterface>
      </NetworkInterfaces>
      <InstanceId>XXXXXXXXXXX</InstanceId>
      <EipAddress>
        <IpAddress/>
        <AllocationId/>
        <InternetChargeType/>
      </EipAddress>
      <InternetMaxBandwidthIn>1000</InternetMaxBandwidthIn>
      <ZoneId>cn-beijing-e</ZoneId>
      <InternetChargeType>PayByBandwidth</InternetChargeType>
      <SpotStrategy>NoSpot</SpotStrategy>
      <StoppedMode>Not-applicable</StoppedMode>
      <SerialNumber>d9bd1cdc-624d-4736-9da5-2ba2f741a304</SerialNumber>
      <IoOptimized>true</IoOptimized>
      <Memory>8192</Memory>
      <Cpu>2</Cpu>
      <VpcAttributes>
        <NatIpAddress/>
        <PrivateIpAddress>
          <IpAddress>172.17. XX.XXX</IpAddress>
        </PrivateIpAddress>
        <VSwitchId>vsw-2zeh0r1pabwtg6wcssgca</VSwitchId>
        <VpcId>vpc-2zeuphj08tt7q3brdb36x</VpcId>
      </VpcAttributes>
      <InternetMaxBandwidthOut>1</InternetMaxBandwidthOut>
      <DeviceAvailable>true</DeviceAvailable>
      <SecurityGroupIds>
        <SecurityGroupId>sg-2ze21r9qb638hvtrvsus</SecurityGroupId>
      </SecurityGroupIds>
      <SpotPriceLimit>0.0</SpotPriceLimit>
      <SaleCycle>Week</SaleCycle>
      <AutoReleaseTime/>
      <InstanceName>ECS-BUY-2017-57-10</InstanceName>
      <Description/>
      <ResourceGroupId/>
      <OSType>linux</OSType>
      <OSName>Ubuntu 16.04 64</OSName>
      <InstanceNetworkType>vpc</InstanceNetworkType>
      <PublicIpAddress>
        <IpAddress>47.94. XX.XX</IpAddress>
      </PublicIpAddress>
      <HostName>iZ2zeh9atclduxvf1zxuylZ</HostName>
      <InstanceType>ecs.g5.large</InstanceType>
      <CreationTime>2017-12-10T04:04Z</CreationTime>
      <Tags>
        <Tag>
          <TagValue>fqwfew</TagValue>
          <TagKey>fefqe</TagKey>
        </Tag>
        <Tag>
          <TagValue>weqfwq</TagValue>
          <TagKey>fqewfwqewf</TagKey>
        </Tag>
        <Tag>
          <TagValue>ewqffeqw</TagValue>
          <TagKey>fqfwewfqw</TagKey>
        </Tag>
      </Tags>
      <Status>Running</Status>
      <ClusterId/>
      <Recyclable>false</Recyclable>
      <RegionId>cn-beijing</RegionId>
      <GPUSpec/>
      <OperationLocks/>
      <GPUAmount>0</GPUAmount>
      <InstanceChargeType>PrePaid</InstanceChargeType>
      <ExpiredTime>2017-12-17T16:00Z</ExpiredTime>
    </Instance>
  </Instances>
</DescribeInstancesResponse>
```

**JSON format** 

```
{
  "Instances": {
    "Instance": [
      {
        "CreationTime": "2015-07-27T07:08Z",
        "DeviceAvailable": "true",
        "EipAddress": {},
        "ExpiredTime": "2011-09-08T16:00Z",
        "HostName": "iZ94t3s0jxkZ",
        "ImageId": "centos6u5_64_20G_aliaegis_20150130.vhd",
        "InnerIpAddress": {
          "IpAddress": [
            "10.170. XX.XXX"
          ]
        },
        "InstanceChargeType": "PostPaid",
        "InstanceId": "XXXXXXXXX",
        "InstanceName": "dd\u6027\u80fd\u6d4b\u8bd5",
        "InstanceNetworkType": "classic",
        "InstanceType": "ecs.s2.large",
        "InternetChargeType": "PayByTraffic",
        "InternetMaxBandwidthIn": "-1",
        "InternetMaxBandwidthOut": "1",
        "IoOptimized": "false",
        "OperationLocks": {
          "LockReason": []
        },
        "PublicIpAddress": {
          "IpAddress": [
            "120.25. XX.XXX"
          ]
        },
        "RegionId": "cn-shenzhen",
        "SecurityGroupIds": {
          "SecurityGroupId": [
            "sg-94kd0cyg0"
          ]
        },
        "SerialNumber": "51d1353b-22bf-4567-a176-8b3e12e43135",
        "Status": "Running",
        "VpcAttributes": {
          "PrivateIpAddress": {
            "IpAddress": []
          }
        },
        "ZoneId": "cn-shenzhen-a"
      }
    ]
  },
  "PageNumber": "1",
  "PageSize": 10,
  "RequestId": "14A07460-EBE7-47CA-9757-12CC4761D47A",
  "TotalCount": "1"
}
```

## Error codes {#ErrorCode .section}

|Error code|Error messages|HTTP status code |Description|
|:---------|:-------------|:----------------|:----------|
|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|400|The specified `Tag.n.Key` and `Tag.n.Value` must be key-value matched.|
|InvalidTagCount|The specified tags are beyond the permitted range.|400|You can add up to five tags to the specified ECS resource in this query request.|
|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records.|404|The specified `InstanceChargeType` does not exist.|
|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid|404|The specified `InternetChargeType` is invalid.|
|InvalidNetworkType.NotFound|The specified InstanceNetworkType is not found|404|The specified `InstanceNetworkType` does not exist.|
|InvalidStatus.NotFound|The specified Status is not found|404|The specified`Status` does not exist.|

