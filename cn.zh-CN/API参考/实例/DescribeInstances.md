# DescribeInstances {#doc_api_Ecs_DescribeInstances .reference}

调用DescribeInstances查询一台或多台实例的详细信息。

## 接口说明 {#description .section}

请求参数的作用类似于一个过滤器，过滤器为逻辑与（AND）关系。如果某一参数为空，则过滤器不起作用。但是参数InstanceIds如果是一个空JSON数组，则视为该过滤器有效，且返回空。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeInstances&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|实例所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeInstances|系统规定参数。取值：DescribeInstances

 |
|InstanceIds|String|否|\["i-xxxxxxxxx", "i-yyyyyyyyy", … "i-zzzzzzzzz"\]|实例ID。取值可以由多个实例ID组成一个JSON数组，最多支持100个ID，ID之间用半角逗号（,）隔开。

 |
|VpcId|String|否|v-vpcid1|专有网络VPC ID。

 |
|VSwitchId|String|否|vsw-vswitchid1|虚拟交换机ID。

 |
|InstanceNetworkType|String|否|vpc|实例网络类型。取值范围：

 -   classic：经典网络
-   vpc：VPC

 |
|SecurityGroupId|String|否|sg-securitygroupid1|实例所属的安全组。

 |
|ZoneId|String|否|cn-hangzhou-g|可用区ID。

 |
|PageNumber|Integer|否|1|实例状态列表的页码。起始值：1。

 默认值：1 。

 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。最大值：100。

 默认值：10。

 |
|InnerIpAddresses|String|否|\["10.1.1.1", "10.1.2.1", … "10.1.10.1"\]|经典网络类型实例的内网IP列表。当InstanceNetworkType=classic时生效，取值可以由多个IP组成一个JSON数组，最多支持100个IP，IP之间用半角逗号（,）隔开。

 |
|PrivateIpAddresses|String|否|\["172.16.1.1", "172.16.2.1", … "172.16.10.1"\]|VPC网络类型实例的私有IP。当InstanceNetworkType=vpc时生效，取值可以由多个IP组成一个JSON数组，最多支持100个IP，IP之间用半角逗号（,）隔开。

 |
|PublicIpAddresses|String|否|\["42.1.1.1", "42.1.2.1", … "42.1.10.1"\]|实例的公网IP列表。当InstanceNetworkType=classic时生效，取值可以由多个IP组成一个JSON数组，最多支持100个IP，IP之间用半角逗号（,）隔开。

 |
|EipAddresses|String|否|\["42.1.1.1", "42.1.2.1", … "42.1.10.1"\]|实例的弹性公网IP列表。当InstanceNetworkType=vpc时该参数生效，取值可以由多个IP组成一个JSON数组，最多支持100个IP，IP之间用半角逗号（,）隔开。

 |
|InstanceChargeType|String|否|PostPaid|实例的计费方式。取值范围：

 -   PostPaid：按量付费
-   PrePaid：包年包月

 |
|InternetChargeType|String|否|PayByTraffic|网络计费方式。取值范围：

 -   PayByTraffic：按流量计费
-   PayByBandwidth：按带宽计费

 |
|InstanceName|String|否|\*Joshua|实例名称，支持使用通配符\*进行模糊搜索。

 |
|ImageId|String|否|m-imageid1|镜像ID。

 |
|Status|String|否|Running|实例状态。取值范围：

 -   Running：运行中
-   Starting：启动中
-   Stopping：停止中
-   Stopped：已停止

 |
|LockReason|String|否|security|资源被锁定的原因。

 |
|IoOptimized|Boolean|否|true|是否是I/O优化型实例。

 |
|NeedSaleCycle|Boolean|否|false|是否返回包年包月实例售卖周期。默认值：false

 |
|Tag.N.Key|String|否|FinanceDept|实例的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun和acs:开头，不能包含http://或者https://。

 |
|Tag.N.Value|String|否|FinanceDeptJoshua|实例的标签值。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持128个字符，不能以aliyun和acs:开头，不能包含http://或者https://。

 |
|InstanceType|String|否|ecs.g5.larger|实例的规格。

 |
|InstanceTypeFamily|String|否|ecs.g5|实例的规格族。

 |
|KeyPairName|String|否|FinanceJoshua|实例使用的SSH密钥对名称。

 |
|ResourceGroupId|String|否|rg-resourcegroupid1|实例所在的企业资源组ID。

 |
|HpcClusterId|String|否|hpc-hpclusterid1|实例所在的HPC集群ID。

 |
|RdmaIpAddresses|String|否|10.10.10.102|HPC实例的Rdma网络IP。

 |
|DryRun|Boolean|否|false|是否只预检此次请求。

 -   true：发送检查请求，不会查询资源状况。检查项包括AccessKey是否有效、RAM用户的授权情况和是否填写了必需参数。如果检查不通过，则返回对应错误。如果检查通过，会返回错误码DryRunOperation。
-   false（默认值）：发送正常请求，通过检查后返回2XX HTTP状态码并直接查询资源状况。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Instances| | |由InstanceAttributesType组成的数组格式，返回实例的信息。

 |
|AutoReleaseTime|String|2017-12-10T04:04Z|按量付费实例的自动释放时间。

 |
|ClusterId|String|c-clusterid1|实例所在的集群 ID。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。

 |
|Cpu|Integer|8|vCPU 核数。

 |
|CreationTime|String|2017-12-10T04:04Z|实例创建时间。

 |
|CreditSpecification|String|Standard|修改t5突发性能实例的运行模式。取值范围：

 -   Standard：标准模式，实例性能请参见[什么是突发性能实例](~~59977~~)下的性能约束模式章节。
-   Unlimited：无性能约束模式，实例性能请参见[什么是突发性能实例](~~59977~~)下的无性能约束模式章节。

 默认值：无。

 |
|DedicatedHostAttribute| | |由专有宿主机ID（DedicatedHostId） 和名称（DedicatedHostName）组成的宿主机属性数组。

 |
|DedicatedHostId|String|dh-dedicatedhostid1|专有宿主机ID。

 |
|DedicatedHostName|String|FinanceDept|专有宿主机名称。

 |
|DedicatedInstanceAttribute| | |专有宿主机实例的属性。

 |
|Affinity|String|default|专有宿主机实例是否与专有宿主机关联。取值范围：

 -   default：专有宿主机实例不与专有宿主机关联。停机不收费实例重启后，可能会放置在自动资源部署池中的其它专有宿主机上。
-   host：专有宿主机实例与专有宿主机关联。停机不收费实例重启后，仍放置在原专有宿主机上。

 |
|Tenancy|String|default|实例的宿主机类型是否为专有宿主机。取值范围：

 -   default：实例的宿主机类型不是专有宿主机。
-   host：实例的宿主机类型为专有宿主机。

 |
|DeletionProtection|Boolean|false|实例释放保护属性，指定是否支持通过控制台或API（DeleteInstance）释放实例。

 -   true：已开启实例释放保护。
-   false：未开启实例释放保护。

 **说明：** 该属性仅适用于按量付费实例，且只能限制手动释放操作，对系统释放操作不生效。

 |
|DeploymentSetId|String|ds-deploymentid1|部署集 ID。

 |
|Description|String|description|实例描述。

 |
|EcsCapacityReservationAttr| | |云服务器ECS的容量预留相关参数。

 |
|CapacityReservationId|String|cr-abcd1234|容量预留ID。

 |
|CapacityReservationPreference|String|cr-abcd1234|容量预留偏好。

 |
|EipAddress| | |弹性公网IP绑定信息。

 |
|AllocationId|String|i-instanceid1|弹性公网IP绑定的实例ID。

 |
|Bandwidth|Integer|5|弹性公网IP的公网带宽限速，单位为Mbps。

 默认值：5。

 |
|InternetChargeType|String|PayByTraffic|弹性公网 IP 的计费方式。

 |
|IpAddress|String|xxx.xx.xxx.xx|弹性公网 IP。

 |
|IsSupportUnassociate|Boolean|true|是否可以解绑弹性公网 IP。

 |
|ExpiredTime|String|2017-12-10T04:04Z|过期时间。按照[ISO8601](~~25696~~)标准表示，并使用UTC +0时间，格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|GPUAmount|Integer|4|实例规格附带的GPU数量。

 |
|GPUSpec|String|NVIDIA V100|实例规格附带的GPU类型。

 |
|HostName|String|JoshuaHost|实例主机名。

 |
|HpcClusterId|String|hpc-hpcclusterid1|实例所属的HPC集群ID。

 |
|ImageId|String|m-imageid1|实例运行的镜像ID。

 |
|InnerIpAddress| |10.170.XX.XXX|实例的内网IP地址。

 |
|InstanceChargeType|String|PostPaid|实例的计费方式。可能值：

 -   PrePaid：包年包月。
-   PostPaid：按量付费。

 |
|InstanceId|String|i-instanceid1|实例ID。

 |
|InstanceName|String|FinanceJoshua|实例名称。

 |
|InstanceNetworkType|String|vpc|实例网络类型。可能值：

 -   Classic
-   Vpc

 |
|InstanceType|String|ecs.g5.large|实例规格。

 |
|InstanceTypeFamily|String|ecs.g5|实例规格族。

 |
|InternetChargeType|String|PayByTraffic|网络计费类型。可能值：

 -   PayByBandwidth：按带宽计费。
-   PayByTraffic：按流量计费。

 |
|InternetMaxBandwidthIn|Integer|100|公网入带宽最大值，单位为Mbps。

 |
|InternetMaxBandwidthOut|Integer|5|公网出带宽最大值，单位为Mbps。

 |
|IoOptimized|Boolean|true|是否为I/O优化型实例。

 |
|KeyPairName|String|FinanceJoshua|密钥对名称。

 |
|LocalStorageAmount|Integer|2|实例挂载的本地存储数量。

 |
|LocalStorageCapacity|Long|1000|实例挂载的本地存储容量。

 |
|Memory|Integer|1024|内存大小，单位MiB。

 |
|NetworkInterfaces| | |实例包含的弹性网卡集合。

 |
|MacAddress|String|00:16:3e:32:b4:dc|弹性网卡的MAC地址。

 |
|NetworkInterfaceId|String|eni-2zeh9atclduxvf1zc\*\*\*|弹性网卡的 ID

 |
|PrimaryIpAddress|String|172.17.XX.XXX|弹性网卡主私有 IP 地址

 |
|OSName|String|Ubuntu 16.04 64|实例的操作系统名称。

 |
|OSNameEn|String|Ubuntu 16.04 64|实例操作系统的英文名称。

 |
|OSType|String|linux|实例的操作系统类型，分为Windows和Linux两种。

 |
|OperationLocks| | |实例的锁定原因。

 |
|LockMsg|String|The specified instance is locked due to financial reason.|实例被锁定的描述信息。

 |
|LockReason|String|Recycling|锁定类型。可能值：

 -   financial：因欠费被锁定。
-   security：因安全原因被锁定。
-   Recycling：抢占式实例的待释放锁定状态。
-   dedicatedhostfinancial：因为专有宿主机欠费导致ECS实例被锁定。

 |
|PublicIpAddress| |172.17.XX.XXX|实例公网IP地址。

 |
|RdmaIpAddress| |10.10.10.102|HPC实例的Rdma网络IP。

 |
|Recyclable|Boolean|false|实例是否可以回收。

 |
|RegionId|String|cn-hangzhou|实例所属地域ID。

 |
|ResourceGroupId|String|rg-resourcegroupid1|实例所属的企业资源组ID。

 |
|SaleCycle|String|month|当实例计费方式为包年包月时，实例购买的周期单位。取值范围：

 -   week
-   month
-   year

 |
|SecurityGroupIds| |sg-securitygroupid1|实例所属安全组集合。

 |
|SerialNumber|String|51d1353b-22bf-4567-a176-8b3e12e43135|实例序列号。

 |
|SpotPriceLimit|Float|0.98|实例的每小时最高价格。支持最大3位小数，参数SpotStrategy=SpotWithPriceLimit时，该参数生效。

 |
|SpotStrategy|String|NoSpot|抢占式实例的抢占策略。可能值：

 -   NoSpot：正常按量付费实例。
-   SpotWithPriceLimit：设置上限价格的抢占式实例。
-   SpotAsPriceGo：系统自动出价，最高按量付费价格。

 默认值：NoSpot。

 |
|StartTime|String|2017-12-10T04:04Z|实例的竞价模式开始时间。

 |
|Status|String|Running|实例状态。

 |
|StoppedMode|String|KeepCharging|实例停机后是否继续收费。可能值：

 -   KeepCharging：停机后继续收费，为您继续保留库存资源。
-   StopCharging：停机后不收费。停机后，我们释放实例对应的资源，例如vCPU、内存和公网IP等资源。重启是否成功依赖于当前地域中是否仍有资源库存。
-   Not-applicable：本实例不支持停机不收费功能。

 |
|Tags| | |实例的标签集合。

 |
|TagKey|String|FinanceDept|实例的标签键。

 |
|TagValue|String|FinanceDept.Joshua|实例的标签值。

 |
|VlanId|String|10|实例的VLAN ID。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。

 |
|VpcAttributes| | |专有网络VPC属性。

 |
|NatIpAddress|String|172.17.XX.XXX|云产品IP，用于云产品之间的网络互通。

 |
|PrivateIpAddress| |172.17.XX.XXX|私有IP地址。

 |
|VSwitchId|String|vsw-2zeh0r1pabwtg6wcss\*\*\*|虚拟交换机ID。

 |
|VpcId|String|vpc-2zeuphj08tt7q3brdb\*\*\*|专有网络VPC ID。

 |
|ZoneId|String|cn-hangzhou-g|实例所属可用区。

 |
|PageNumber|Integer|1|实例列表的页码。

 |
|PageSize|Integer|10|输入时设置的每页行数。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |
|TotalCount|Integer|6|查询到的实例总数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeInstances
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeInstancesResponse>
    <PageNumber>1</PageNumber>
    <TotalCount>6</TotalCount>
    <PageSize>10</PageSize>
    <RequestId>8EF01A45-FFFA-497B-B5C3-1DE1B74DB32D</RequestId>
    <Instances>
        <Instance>
            <InnerIpAddress></InnerIpAddress>
            <ImageId>ubuntu_16_0402_64_20G_alibase_20170818.vhd</ImageId>
            <InstanceTypeFamily>ecs.g5</InstanceTypeFamily>
            <VlanId></VlanId>
            <NetworkInterfaces>
                <NetworkInterface>
                    <MacAddress>00:16:3e:32:b4:dc</MacAddress>
                    <PrimaryIpAddress>172.17.XX.XXX</PrimaryIpAddress>
                    <NetworkInterfaceId>eni-2zeh9atclduxvf1zc***</NetworkInterfaceId>
                </NetworkInterface>
            </NetworkInterfaces>
            <InstanceId>XXXXXXXXXXX</InstanceId>
            <EipAddress>
                <IpAddress></IpAddress>
                <AllocationId></AllocationId>
                <InternetChargeType></InternetChargeType>
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
                <NatIpAddress></NatIpAddress>
                <PrivateIpAddress>
                    <IpAddress>172.17.XX.XXX</IpAddress>
                </PrivateIpAddress>
                <VSwitchId>vsw-2zeh0r1pabwtg6wcss***</VSwitchId>
                <VpcId>vpc-2zeuphj08tt7q3brdb***</VpcId>
            </VpcAttributes>
            <InternetMaxBandwidthOut>1</InternetMaxBandwidthOut>
            <SecurityGroupIds>
                <SecurityGroupId>sg-2ze21r9qb638hvtrv***</SecurityGroupId>
            </SecurityGroupIds>
            <SpotPriceLimit>0.0</SpotPriceLimit>
            <SaleCycle>Week</SaleCycle>
            <AutoReleaseTime></AutoReleaseTime>
            <InstanceName>ECS-BUY-2017-57-10</InstanceName>
            <Description></Description>
            <ResourceGroupId></ResourceGroupId>
            <OSType>linux</OSType>
            <OSName>Ubuntu 16.04 64</OSName>
            <InstanceNetworkType>vpc</InstanceNetworkType>
            <PublicIpAddress>
                <IpAddress>47.94.XX.XX</IpAddress>
            </PublicIpAddress>
            <HostName>iZ2zeh9atclduxvf1zxu***</HostName>
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
            <ClusterId></ClusterId>
            <Recyclable>false</Recyclable>
            <RegionId>cn-beijing</RegionId>
            <GPUSpec></GPUSpec>
            <OperationLocks></OperationLocks>
            <GPUAmount>0</GPUAmount>
            <InstanceChargeType>PrePaid</InstanceChargeType>
            <ExpiredTime>2017-12-17T16:00Z</ExpiredTime>
        </Instance>
    </Instances>
</DescribeInstancesResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":"1",
	"TotalCount":"1",
	"PageSize":"10",
	"RequestId":"14A07460-EBE7-47CA-9757-12CC4761D47A",
	"Instances":{
		"Instance":[
			{
				"ImageId":"centos6u5_64_20G_aliaegis_20150130.vhd",
				"InnerIpAddress":{
					"IpAddress":[
						"10.170.XX.XXX"
					]
				},
				"InstanceId":"XXXXXXXXX",
				"EipAddress":{},
				"InternetMaxBandwidthIn":"-1",
				"ZoneId":"cn-shenzhen-a",
				"InstanceNetworkType":"classic",
				"PublicIpAddress":{
					"IpAddress":[
						"120.25.XX.XXX"
					]
				},
				"InternetChargeType":"PayByTraffic",
				"HostName":"iZ94t3s0j***",
				"InstanceType":"ecs.s2.large",
				"SerialNumber":"51d1353b-22bf-4567-a176-8b3e12e43135",
				"IoOptimized":"false",
				"CreationTime":"2015-07-27T07:08Z",
				"Status":"Running",
				"VpcAttributes":{
					"PrivateIpAddress":{
						"IpAddress":[]
					}
				},
				"InternetMaxBandwidthOut":"1",
				"SecurityGroupIds":{
					"SecurityGroupId":[
						"sg-94kd0c***"
					]
				},
				"RegionId":"cn-shenzhen",
				"OperationLocks":{
					"LockReason":[]
				},
				"InstanceChargeType":"PostPaid",
				"ExpiredTime":"2011-09-08T16:00Z",
				"InstanceName":"FinanceJoshua"
			}
		]
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidInstanceChargeType.NotFound|The InstanceChargeType does not exist in our records|指定的实例升降配规格不存在。|
|404|InvalidInternetChargeType.ValueNotSupported|The specified InternetChargeType is not valid|指定的网络计费方式不合法。|
|404|InvalidLockReason.NotFound|The specified LockReason is not found|指定的锁定类型不存在。|
|404|InvalidFilterKey.NotFound| |指定的起始时间或到期时间参数错误。|
|404|InvalidFilterValue| |您输了的时间格式不合法。|
|404|InvalidNetworkType.NotFound|The specified InstanceNetworkType is not found|指定的带宽类型不存在。|
|404|InvalidStatus.NotFound|The specified Status is not found|指定的资源状态不存在。|
|400|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|指定的 Tag.n.Key 和 Tag.n.Value 不匹配。|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|指定的标记超出取值范围。|
|400|InvalidHpcClusterId.NotFound|The specified HpcClusterId is not found.|指定的HPC集群ID不存在。|
|400|InvalidHpcClusterId.Creating|The specified HpcClusterId is creating.|指定的HPC集群正在创建中。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

