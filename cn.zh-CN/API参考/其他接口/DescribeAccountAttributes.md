# DescribeAccountAttributes {#doc_api_Ecs_DescribeAccountAttributes .reference}

调用DescribeAccountAttributes查询您在一个阿里云地域下能创建的ECS资源上限。包括您能创建的安全组数量、弹性网卡数量、按量付费vCPU核数、抢占式实例vCPU核数、专用宿主机数量、地域网络类型以及账号是否已完成实名认证。

## 接口说明 {#description .section}

[注册](https://account.aliyun.com/register/register.htm)了阿里云账号后，您可以在不同的阿里云地域中创建一定数量的ECS资源，更多详情，请参见[使用限制](~~25412~~)。

您也可以根据自己的需求[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex.htm)提高资源使用上限。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeAccountAttributes&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeAccountAttributes|系统规定参数。对于您自行拼凑HTTP/HTTPS URL发起的API请求，`Action`为必选参数。取值：DescribeAccountAttributes

 |
|ZoneId|String|否|cn-hangzhou-b|可用区ID。

 |
|AttributeName.N|RepeatList|否|max-security-groups|查询某类资源的使用上限，N的取值范围为1~8。取值范围：

 -   instance-network-type：当前地域可选择的网络类型。
-   max-security-groups：安全组数量。
-   max-elastic-network-interfaces：当前地域下弹性网卡的数量。
-   max-postpaid-instance-vcpu-count：当前地域下按量付费实例的vCPU核数。
-   max-spot-instance-vcpu-count：当前地域下抢占式实例vCPU核数。
-   max-dedicated-hosts：当前地域下专用宿主机数量。
-   supported-postpaid-instance-types：当前地域下按量付费I/O优化实例规格。
-   max-axt-command-count：当前地域下云助手命令的数量。
-   max-axt-invocation-daily：当前地域下每天可以执行的云助手命令次数。
-   real-name-authentication：账号是否完成了实名认证。

**说明：** 您只有完成了实名认证才可以创建ECS实例。


 默认值：空。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|AccountAttributeItems| | |指定地域下账号特权的信息集合。

 |
|AttributeName|String|max-security-groups|资源的使用上限分类。可能值:

 -   instance-network-type：当前地域可选择的网络类型。
-   max-security-groups：安全组数量。
-   max-elastic-network-interfaces：当前地域下弹性网卡的数量。
-   max-postpaid-instance-vcpu-count：当前地域下按量付费实例的vCPU核数。
-   max-spot-instance-vcpu-count：当前地域下抢占式实例vCPU核数。
-   max-dedicated-hosts：当前地域下专用宿主机数量。
-   supported-postpay-instance-types：当前地域下按量付费I/O优化实例规格。
-   real-name-authentication：账号是否完成了实名认证。
-   max-axt-command-count：当前地域下云助手命令的数量。
-   max-axt-invocation-daily：当前地域下每天可以执行的云助手命令次数。

 |
|AttributeValues| | |资源的使用上限具体数值。

 |
|Count|Integer|3|特权属性类型的数量。

 |
|ExpiredTime|String|2019-01-01T12:30:00Z|特权到期时间，仅存在到期时间的账号特权会返回该参数。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC +0时间。格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|InstanceChargeType|String|PrePaid|实例计费方式。

 |
|InstanceType|String|\["ecs.g5.large"\]|实例规格。

 |
|Value|String|800|当前地域或全部地域下某类资源的使用上限具体数值。可能值:

 -   分类为max-security-groups、max-elastic-network-interfaces、max-postpaid-instance-vcpu-count、max-dedicated-hosts、max-spot-instance-vcpu-count时：返回0或正整数。
-   分类为supported-postpay-instance-types时：返回实例规格取值。参见[实例规格族](~~25378~~)。
-   分类为real-name-authentications时：返回 yes | none | unnecessary。
-   分类为instance-network-type时：返回 vpc | classic。

 |
|ZoneId|String|cn-hangzhou-b|可用区ID。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeAccountAttributes
&RegionId=cn-hangzhou
&ZoneId=cn-hangzhou-b
&AttributeName.1=max-security-groups
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeAccountAttributesResponse>
    <AccountAttributeItems>
        <AccountAttributeItem>
            <AttributeName>max-security-groups</AttributeName>
            <AttributeValues>
                <ValueItem>
                    <Value>800</Value>
                <ValueItem>
            </AttributeValues>
        </AccountAttributeItem>
          <AccountAttributeItem>
            <AttributeName>instance-network-type</AttributeName>
            <AttributeValues>
                <ValueItem>
                    <Value>vpc</Value>
                    <Value>classic</Value>
                <ValueItem>
            </AttributeValues>
        </AccountAttributeItem>
     </AccountAttributeItems>
    <RequestId>675B6D89-A3EB-4987-BAF3-610591E0D019</RequestId>
</DescribeAccountAttributesResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"AccountAttributeItems":{
		"AccountAttributeItem":[
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"100"
						}
					]
				},
				"AttributeName":"max-security-groups"
			},
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"2"
						}
					]
				},
				"AttributeName":"max-dedicated-hosts"
			},
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"1000"
						}
					]
				},
				"AttributeName":"max-postpaid-instance-vcpu-count"
			},
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"1000"
						}
					]
				},
				"AttributeName":"max-spot-instance-vcpu-count"
			},
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"5000"
						}
					]
				},
				"AttributeName":"max-elastic-network-interfaces"
			},
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"yes"
						}
					]
				},
				"AttributeName":"real-name-authentication"
			},
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"vpc"
						}
					]
				},
				"AttributeName":"instance-network-type"
			},
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"ecs.f3-c16f1.4xlarge"
						},
						{
							"Value":"ecs.g5.2xlarge"
						}
					]
				},
				"AttributeName":"supported-postpaid-instance-types"
			}
		]
	},
	"RequestId":"8CE45CD5-31FB-47C2-959D-CA8144CE9F42"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Invalid.Parameter|The required parameter regionId must be not null.|缺失必需参数。|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

