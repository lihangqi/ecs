# DescribeInstances {#DescribeInstances .reference}

查询一台或多台实例的详细信息。

## 描述 {#section_phb_mrs_xdb .section}

请求参数的作用类似于一个过滤器，过滤器为逻辑与（`AND`）关系。如果某一参数为空，则过滤器不起作用。但是参数`InstanceIds`如果是一个空JSON数组，即`[]`，则视为该过滤器有效，且返回空。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeInstances|
|RegionId|String|是|地域ID。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|VpcId|String|否|专有网络VPC ID。|
|VSwitchId|String|否|虚拟交换机ID。|
|ZoneId|String|否|可用区ID。|
|InstanceIds|String|否|实例ID。取值可以由多个实例ID组成一个JSON数组，格式为\["i-xxxxxxxxx", "i-yyyyyyyyy", … "i-zzzzzzzzz"\]，最多支持100个ID，ID之间用半角逗号（`,`）隔开。|
|InstanceType|String|否|实例的规格。|
|CreditSpecification|String|否|突发性能 t5 实例的运行模式。-   Standard：标准模式，实例性能请参阅 [t5性能约束实例](../intl.zh-CN/产品简介/实例/突发性能实例/t5性能约束实例.md#)。
-   Unlimited：无性能约束模式，实例性能请参阅 [t5无性能约束实例](../intl.zh-CN/产品简介/实例/突发性能实例/t5无性能约束实例.md#)。

默认值：无。

|
|InstanceTypeFamily|String|否|实例的规格族。|
|InstanceNetworkType|String|否|实例网络类型。取值范围：-   classic：经典网络
-   vpc：VPC

|
|PrivateIpAddresses|String|否|VPC网络类型实例的私有IP。当`InstanceNetworkType=vpc`时生效，取值可以由多个IP组成一个JSON数组，格式为\["172.16.1.1", "172.16.2.1", … "172.16.10.1"\]，最多支持100个IP，IP之间用半角逗号（`,`）隔开。|
|InnerIpAddresses|String|否|经典网络类型实例的内网IP列表。当`InstanceNetworkType=classic`时生效，取值可以由多个IP组成一个JSON数组，格式为\["10.1.1.1", "10.1.2.1", … "10.1.10.1"\]，最多支持100个IP，IP之间用半角逗号（`,`）隔开。|
|PublicIpAddresses|String|否|实例的公网IP列表。当`InstanceNetworkType=classic`时生效，取值可以由多个IP组成一个JSON数组，格式为\["42.1.1.1", "42.1.2.1", … "42.1.10.1"\]，最多支持100个IP，IP之间用半角逗号（`,`）隔开。|
|EipAddresses|String|否|实例的弹性公网IP列表。当`InstanceNetworkType=vpc`时该参数生效，取值可以由多个IP组成一个JSON数组，格式为\["42.1.1.1", "42.1.2.1", … "42.1.10.1"\]，最多支持100个IP，IP之间用半角逗号（`,`）隔开。|
|SecurityGroupId|String|否|实例所属的安全组。|
|InstanceChargeType|String|否|实例的计费方式。取值范围：-   PrePaid：包年包月
-   PostPaid：按量付费

|
|SpotStrategy|String|否|按量付费实例的抢占策略。当`InstanceChargeType=PostPaid`时生效，取值范围：-   NoSpot：正常按量付费实例。
-   SpotWithPriceLimit：设置上限价格的抢占式实例。
-   SpotAsPriceGo：系统自动出价，最高按量付费价格。

默认值：NoSpot|
|InternetChargeType|String|否|网络计费方式。取值范围：-   PayByTraffic：按流量计费

|
|InstanceName|String|否|实例名称，支持使用通配符`*`进行模糊搜索。|
|ImageId|String|否|镜像ID。|
|DeploymentSetId|String|否|部署集ID。|
|Status|String|否|实例状态。取值范围：-   Running：运行中
-   Starting：启动中
-   Stopping：停止中
-   Stopped：已停止

|
|IoOptimized|Boolean|否|是否是I/O优化型实例。|
|Tag.n.Key|String|否|实例的标签键。n 的取值范围：\[1, 20\]。一旦传入该值，则不允许为空字符串。最多支持 64 个字符，不能以 aliyun、acs:、http:// 或者 https:// 开头。|
|Tag.n.Value|String|否|实例的标签值。n的取值范围：\[1, 20\]。一旦传入该值，可以为空字符串。最多支持 128 个字符，不能以 aliyun、acs:、http:// 或者 https:// 开头。|
|PageNumber|Integer|否|实例状态列表的页码。起始值：1默认值：1

|
|PageSize|Integer|否|分页查询时设置的每页行数。最大值：100默认值：10

|
|DryRun|Boolean|否|是否只预检此次请求。-   true：发送检查请求，不会查询资源状况。检查项包括AccessKey是否有效、RAM用户的授权情况和是否填写了必需参数。如果检查不通过，则返回对应错误。如果检查通过，会返回错误码`DryRunOperation`。
-   false：发送正常请求，通过检查后返回2XX HTTP状态码并直接查询资源状况。

默认值：false

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|TotalCount|Integer|实例总台数|
|PageNumber|Integer|实例列表的页码|
|PageSize|Integer|输入时设置的每页行数|
|Instances|[InstanceAttributesType](intl.zh-CN/API 参考/数据类型/InstanceAttributesType.md#)|由InstanceAttributesType组成的数组格式，返回实例的信息|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeInstances
&RegionId=cn-hangzhou
&<公共请求参数>
```

**返回示例**

**XML格式**

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
          <PrimaryIpAddress>172.17.XX.XXX</PrimaryIpAddress>
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
          <IpAddress>172.17.XX.XXX</IpAddress>
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
        <IpAddress>47.94.XX.XX</IpAddress>
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

**JSON格式**

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
            "10.170.XX.XXX"
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
            "120.25.XX.XXX"
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
  "PageSize": "10",
  "RequestId": "14A07460-EBE7-47CA-9757-12CC4761D47A",
  "TotalCount": "1"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|DryRunOperation|Request validation has been passed with DryRun flag set.|400|此次DryRun预检请求合格。|
|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|400|指定的Tag.n.Key和Tag.n.Value必须键值匹配。|
|InvalidTagCount|The specified tags are beyond the permitted range.|400|指定的标签数不能超过20个。|
|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records.|404|指定的InstanceChargeType不存在。|
|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid|404|指定的InternetChargeType不合法。|
|InvalidNetworkType.NotFound|The specified InstanceNetworkType is not found|404|指定的InstanceNetworkType不存在。|
|InvalidStatus.NotFound|The specified Status is not found|404|指定的Status不存在。|

