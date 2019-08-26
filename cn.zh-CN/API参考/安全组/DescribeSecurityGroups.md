# DescribeSecurityGroups {#doc_api_Ecs_DescribeSecurityGroups .reference}

调用DescribeSecurityGroups查询您创建的安全组的基本信息，例如安全组ID和安全组描述等。返回列表按照安全组ID降序排列。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Ecs&api=DescribeSecurityGroups&type=RPC&version=2014-05-26)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeSecurityGroups|系统规定参数。取值：DescribeSecurityGroups

 |
|DryRun|Boolean|否|false|是否只预检此次请求。

 -   true：发送检查请求，不会查询资源状况。检查项包括AccessKey是否有效、RAM用户的授权情况和是否填写了必需参数。如果检查不通过，则返回对应错误。如果检查通过，会返回错误码DryRunOperation。
-   false：发送正常请求，通过检查后返回2XX HTTP状态码并直接查询资源状况。

 默认值：false

 |
|NetworkType|String|否|vpc|网络类型。

 |
|PageNumber|Integer|否|1|安全组列表的页码。起始值：1

 默认值：1

 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。最大值：50

 默认值：10

 |
|ResourceGroupId|String|否|rg-resourcegroupid1|安全组所在的企业资源组ID。

 |
|SecurityGroupId|String|否|sg-securitygroupid|安全组ID。

 |
|SecurityGroupIds|String|否|\["sg-id1", "sg-id2", "sg-id2",....\]|安全组ID列表。一次最多支持100个安全组ID，ID之间用半角逗号（,）隔开，格式为JSON数组。

 |
|SecurityGroupName|String|否|test1|安全组名称。

 |
|Tag.N.Key|String|否|FinanceDept|安全组的标签键。N的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun和acs:开头，不能包含http://或者https://。

 |
|Tag.N.Value|String|否|FinanceJoshua|安全组的标签值。N的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun和acs:开头，不能包含http://或者https://。

 |
|Tag.N.key|String|否|FinanceDept|安全组的标签键。

 **说明：** 为提高兼容性，建议您尽量使用Tag.N.Key参数。

 |
|Tag.N.value|String|否|FinanceJoshua|安全组的标签值。

 **说明：** 为提高兼容性，建议您尽量使用Tag.N.Value参数。

 |
|VpcId|String|否|vpc-vpcid1|安全组所在的专有网络ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|当前页码

 |
|PageSize|Integer|10|每页行数

 |
|RegionId|String|cn-hangzhou|安全组所属地域ID

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID

 |
|SecurityGroups| | |安全组信息集合

 |
|CreationTime|String|2017-12-05T22:40:00Z|创建时间。按照[ISO8601](~~25696~~)标准表示，并需要使用UTC时间。格式为：yyyy-MM-ddThh:mmZ

 |
|Description|String|FinanceDept|描述信息

 |
|ResourceGroupId|String|rg-resourcegroupid1|安全组所在的企业资源组 ID

 |
|SecurityGroupId|String|sg-securitygroupid1|安全组ID

 |
|SecurityGroupName|String|FinanceJoshua|安全组名称

 |
|SecurityGroupType|String|normal|安全组类型。可能值：

 -   normal：普通安全组
-   enterprise：企业安全组

 |
|Tags| | |安全组的标签

 |
|TagKey|String|FinanceDept|安全组的标签键

 |
|TagValue|String|FinanceJoshua|安全组的标签值

 |
|VpcId|String|vpc-vpcid1|安全组所属的专有网络

 |
|TotalCount|Integer|4|安全组的总数

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeSecurityGroups
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeSecurityGroupsResponse>
      <RequestId>94D38899-626D-434A-891F-7E1F77A81525</RequestId>
      <TotalCount>4</TotalCount>
      <PageNumber>1</PageNumber>
      <PageSize>10</PageSize>
      <RegionId>cn-hangzhou</RegionId>
      <SecurityGroups>
            <SecurityGroup>
                  <SecurityGroupId>sg-securityGroupId1</SecurityGroupId>
                  <Description>Test</Description>
            </SecurityGroup>
            <SecurityGroup>
                  <SecurityGroupId>sg-securityGroupId2</SecurityGroupId>
                  <Description>test00212</Description>
            </SecurityGroup>
            <SecurityGroup>
                  <SecurityGroupId>sg-securityGroupId3</SecurityGroupId>
                  <Description>cn-hangzhou test group</Description>
            </SecurityGroup>
            <SecurityGroup>
                  <SecurityGroupId>sg-securityGroupId4</SecurityGroupId>
                  <Description>cn-hangzhou test group</Description>
            </SecurityGroup>
      </SecurityGroups>
</DescribeSecurityGroupsResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":"1",
	"TotalCount":4,
	"PageSize":"10",
	"RegionId":"cn-hangzhou",
	"RequestId":"94D38899-626D-434A-891F-7E1F77A81525",
	"SecurityGroups":{
		"SecurityGroup":[
			{
				"SecurityGroupId":"sg-securityGroupId1",
				"Description":"TestByXcf"
			},
			{
				"SecurityGroupId":"sg-securityGroupId2",
				"Description":"test00212"
			},
			{
				"SecurityGroupId":"sg-securityGroupId3",
				"Description":"cn-hangzhou test group"
			},
			{
				"SecurityGroupId":"sg-securityGroupId4",
				"Description":"cn-hangzhou test group"
			}
		]
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|

访问[错误中心](https://error-center.aliyun.com/status/product/Ecs)查看更多错误码。

