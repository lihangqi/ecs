# DescribeSecurityGroupAttribute {#doc_api_Ecs_DescribeSecurityGroupAttribute .reference}

调用DescribeSecurityGroupAttribute查询一个安全组的详情。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeSecurityGroupAttribute&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|安全组所属地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|SecurityGroupId|String|是|sg-securitygroupid1|安全组ID。

 |
|Action|String|否|DescribeSecurityGroupAttribute|系统规定参数。取值：DescribeSecurityGroupAttribute

 |
|Direction|String|否|all|安全组规则授权方向。取值范围：

 -   egress：安全组出方向
-   ingress：安全组入方向
-   all：不区分方向

 默认值：all

 |
|NicType|String|否|intranet|网卡类型。取值范围：

 -   internet：公网
-   intranet：内网

 默认值：internet

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Description|String|FinanceDept|安全组描述信息。

 |
|InnerAccessPolicy|String|accept|安全组内网络连通策略。可能值：

 -   Accept：内网互通
-   Drop：内网隔离

 |
|Permissions| | |安全组权限规则集合。

 |
|CreateTime|String|2018-12-12T07:28:38Z|创建时间，UTC时间。

 |
|Description|String|FinanceDept|安全组描述信息。

 |
|DestCidrIp|String|0.0.0.0/0|目标IP地址段，用于出方向授权。

 |
|DestGroupId|String|sg-securitygroupid1|目标安全组，用于出方向授权。

 |
|DestGroupName|String|SecurityGuard|目的端安全组名称。

 |
|DestGroupOwnerAccount|String|SecurityGuard|目标安全组所属阿里云账户ID。

 |
|Direction|String|ingress|授权方向。

 |
|IpProtocol|String|TCP|IP协议。

 |
|Ipv6DestCidrIp|String|2001:db8:1233:1a00::\*\*\*|目的IPv6地址段。

 |
|Ipv6SourceCidrIp|String|2001:db8:1234:1a00::\*\*\*|源IPv6地址段。

 |
|NicType|String|intranet|网络类型。

 |
|Policy|String|Accept|授权策略。

 |
|PortRange|String|80/80|端口范围。

 |
|Priority|String|1|规则优先级。

 |
|SourceCidrIp|String|0.0.0.0/0|源IP地址段，用于入方向授权。

 |
|SourceGroupId|String|sg-securitygroupid2|源安全组，用于入方向授权。

 |
|SourceGroupName|String|FinanceDeptJoshua|源端安全组名称。

 |
|SourceGroupOwnerAccount|String|FinanceJoshua|源安全组所属阿里云账户ID。

 |
|SourcePortRange|String|80/80|源端端口范围。

 |
|RegionId|String|cn-hangzhou|地域ID。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |
|SecurityGroupId|String|sg-securityid1|目标安全组ID。

 |
|SecurityGroupName|String|FinanceJoshua|目标安全组名称。

 |
|VpcId|String|v-vpcid1|VPC ID。如果返回VPC ID，表示该安全组网络类型为VPC。否则，表示是经典网络类型安全组。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?RegionId=cn-hangzhou
&SecurityGroupId=sg-securitygroupid1
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeSecurityGroupAttributeResponse>
	  <SecurityGroupId>sg-bp1gxw6bznjjvhu3g***</SecurityGroupId>
	  <InnerAccessPolicy>Accept</InnerAccessPolicy>
	  <SecurityGroupName>FinanceJoshua</SecurityGroupName>
	  <Description>FinanceDept</Description>
	  <RegionId>cn-hangzhou</RegionId>
	  <RequestId>A72322C1-47C0-491E-8088-8B17E4EA859F</RequestId>
	  <Permissions>
		    <Permission>
			      <SourceCidrIp>10.0.0.0/8</SourceCidrIp>
			      <Description></Description>
			      <DestCidrIp></DestCidrIp>
			      <NicType>intranet</NicType>
			      <DestGroupName></DestGroupName>
			      <PortRange>22/22</PortRange>
			      <DestGroupId></DestGroupId>
			      <Ipv6DestCidrIp></Ipv6DestCidrIp>
			      <Direction>ingress</Direction>
			      <Priority>1</Priority>
			      <IpProtocol>TCP</IpProtocol>
			      <SourcePortRange></SourcePortRange>
			      <SourceGroupOwnerAccount></SourceGroupOwnerAccount>
			      <Policy>Accept</Policy>
			      <CreateTime>2018-12-12T07:28:38Z</CreateTime>
			      <SourceGroupId></SourceGroupId>
			      <DestGroupOwnerAccount></DestGroupOwnerAccount>
			      <Ipv6SourceCidrIp></Ipv6SourceCidrIp>
			      <SourceGroupName></SourceGroupName>
		    </Permission>
		    <Permission>
			      <SourceCidrIp>0.0.0.0/0</SourceCidrIp>
			      <Description></Description>
			      <DestCidrIp></DestCidrIp>
			      <NicType>intranet</NicType>
			      <DestGroupName></DestGroupName>
			      <PortRange>443/443</PortRange>
			      <DestGroupId></DestGroupId>
			      <Ipv6DestCidrIp></Ipv6DestCidrIp>
			      <Direction>ingress</Direction>
			      <Priority>1</Priority>
			      <IpProtocol>TCP</IpProtocol>
			      <SourcePortRange></SourcePortRange>
			      <SourceGroupOwnerAccount></SourceGroupOwnerAccount>
			      <Policy>Accept</Policy>
			      <CreateTime>2018-12-12T07:28:38Z</CreateTime>
			      <SourceGroupId></SourceGroupId>
			      <DestGroupOwnerAccount></DestGroupOwnerAccount>
			      <Ipv6SourceCidrIp></Ipv6SourceCidrIp>
			      <SourceGroupName></SourceGroupName>
		    </Permission>
		    <Permission>
			      <SourceCidrIp>10.0.0.0/8</SourceCidrIp>
			      <Description></Description>
			      <DestCidrIp></DestCidrIp>
			      <NicType>intranet</NicType>
			      <DestGroupName></DestGroupName>
			      <PortRange>80/80</PortRange>
			      <DestGroupId></DestGroupId>
			      <Ipv6DestCidrIp></Ipv6DestCidrIp>
			      <Direction>ingress</Direction>
			      <Priority>1</Priority>
			      <IpProtocol>TCP</IpProtocol>
			      <SourcePortRange></SourcePortRange>
			      <SourceGroupOwnerAccount></SourceGroupOwnerAccount>
			      <Policy>Accept</Policy>
			      <CreateTime>2018-12-12T07:28:38Z</CreateTime>
			      <SourceGroupId></SourceGroupId>
			      <DestGroupOwnerAccount></DestGroupOwnerAccount>
			      <Ipv6SourceCidrIp></Ipv6SourceCidrIp>
			      <SourceGroupName></SourceGroupName>
		    </Permission>
		    <Permission>
			      <SourceCidrIp>10.0.0.0/8</SourceCidrIp>
			      <Description></Description>
			      <DestCidrIp></DestCidrIp>
			      <NicType>intranet</NicType>
			      <DestGroupName></DestGroupName>
			      <PortRange>-1/-1</PortRange>
			      <DestGroupId></DestGroupId>
			      <Ipv6DestCidrIp></Ipv6DestCidrIp>
			      <Direction>ingress</Direction>
			      <Priority>1</Priority>
			      <IpProtocol>ICMP</IpProtocol>
			      <SourcePortRange>-1/-1</SourcePortRange>
			      <SourceGroupOwnerAccount></SourceGroupOwnerAccount>
			      <Policy>Accept</Policy>
			      <CreateTime>2018-12-12T07:28:38Z</CreateTime>
			      <SourceGroupId></SourceGroupId>
			      <DestGroupOwnerAccount></DestGroupOwnerAccount>
			      <Ipv6SourceCidrIp></Ipv6SourceCidrIp>
			      <SourceGroupName></SourceGroupName>
		    </Permission>
	  </Permissions>
	  <VpcId>vpc-bp1opxu1zkhn00gzv2***</VpcId>
</DescribeSecurityGroupAttributeResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"SecurityGroupId":"sg-bp1gxw6bznjjvhu3g***",
	"Description":"FinanceDept",
	"SecurityGroupName":"FinanceJoshua",
	"InnerAccessPolicy":"Accept",
	"RequestId":"A72322C1-47C0-491E-8088-8B17E4EA859F",
	"RegionId":"cn-hangzhou",
	"Permissions":{
		"Permission":[
			{
				"SourceCidrIp":"10.0.0.0/8",
				"Description":"",
				"DestCidrIp":"",
				"NicType":"intranet",
				"DestGroupName":"",
				"PortRange":"22/22",
				"DestGroupId":"",
				"Ipv6DestCidrIp":"",
				"Direction":"ingress",
				"Priority":1,
				"IpProtocol":"TCP",
				"SourcePortRange":"",
				"SourceGroupOwnerAccount":"",
				"Policy":"Accept",
				"CreateTime":"2018-12-12T07:28:38Z",
				"SourceGroupId":"",
				"DestGroupOwnerAccount":"",
				"Ipv6SourceCidrIp":"",
				"SourceGroupName":""
			},
			{
				"SourceCidrIp":"0.0.0.0/0",
				"Description":"",
				"DestCidrIp":"",
				"NicType":"intranet",
				"DestGroupName":"",
				"PortRange":"443/443",
				"DestGroupId":"",
				"Ipv6DestCidrIp":"",
				"Direction":"ingress",
				"Priority":1,
				"IpProtocol":"TCP",
				"SourcePortRange":"",
				"SourceGroupOwnerAccount":"",
				"Policy":"Accept",
				"CreateTime":"2018-12-12T07:28:38Z",
				"SourceGroupId":"",
				"DestGroupOwnerAccount":"",
				"Ipv6SourceCidrIp":"",
				"SourceGroupName":""
			},
			{
				"SourceCidrIp":"0.0.0.0/0",
				"Description":"",
				"DestCidrIp":"",
				"NicType":"intranet",
				"DestGroupName":"",
				"PortRange":"80/80",
				"DestGroupId":"",
				"Ipv6DestCidrIp":"",
				"Direction":"ingress",
				"Priority":1,
				"IpProtocol":"TCP",
				"SourcePortRange":"",
				"SourceGroupOwnerAccount":"",
				"Policy":"Accept",
				"CreateTime":"2018-12-12T07:28:38Z",
				"SourceGroupId":"",
				"DestGroupOwnerAccount":"",
				"Ipv6SourceCidrIp":"",
				"SourceGroupName":""
			},
			{
				"SourceCidrIp":"10.0.0.0/8",
				"Description":"",
				"DestCidrIp":"",
				"NicType":"intranet",
				"DestGroupName":"",
				"PortRange":"-1/-1",
				"DestGroupId":"",
				"Ipv6DestCidrIp":"",
				"Direction":"ingress",
				"Priority":1,
				"IpProtocol":"ICMP",
				"SourcePortRange":"-1/-1",
				"SourceGroupOwnerAccount":"",
				"Policy":"Accept",
				"CreateTime":"2018-12-12T07:28:38Z",
				"SourceGroupId":"",
				"DestGroupOwnerAccount":"",
				"Ipv6SourceCidrIp":"",
				"SourceGroupName":""
			}
		]
	},
	"VpcId":"vpc-bp1opxu1zkhn00gzv2***"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|指定的 RegionId 不存在，请您检查此产品在该地域是否可用。|
|404|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|指定的安全组在该用户账号下不存在，请您检查安全组id是否正确。|
|400|InvalidNicType.ValueNotSupported|The specified NicType does not exist.|指定的网络类型不存在，请您检查网络类型是否正确。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|
|400|InvalidParamter|Invalid Parameter|指定的参数不合法。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

