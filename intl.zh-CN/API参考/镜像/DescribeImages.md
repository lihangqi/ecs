# DescribeImages {#doc_api_Ecs_DescribeImages .reference}

查询您可以使用的镜像资源。

## 接口说明 {#description .section}

-   您可以查询的镜像资源包括您的自定义镜像、阿里云提供的公共镜像、云市场镜像以及其他阿里云用户主动共享给您的共享镜像。
-   支持分页查询，查询结果包括可使用的镜像资源的总数和当前页的镜像资源。每页的数量默认为10条。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeImages)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|实例所属的地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeImages|系统规定参数。取值：DescribeImages

 |
|ActionType|String|否|CreateEcs|镜像需要被使用到的场景。取值范围：

 -   CreateEcs（默认）：创建实例
-   ChangeOS：更换系统盘/更换操作系统

 |
|Architecture|String|否|i386|镜像的体系架构。取值范围：

 -   i386
-   x86\_64

 |
|DryRun|Boolean|否|false|是否只预检此次请求。

 -   true：发送检查请求，不会查询资源状况。检查项包括AccessKey是否有效、RAM用户的授权情况和是否填写了必需参数。如果检查不通过，则返回对应错误。如果检查通过，会返回错误码DryRunOperation。
-   false：发送正常请求，通过检查后返回2XX HTTP状态码并直接查询资源状况。

 默认值：false

 |
|Filter.N.Key|String|否|CreationStartTime|指定过滤类型的 Key。

 |
|Filter.N.Value|String|否|2017-12-05T22:40:00Z|指定过滤类型的 Value。

 |
|ImageId|String|否|m-imageid1|镜像ID。

 |
|ImageName|String|否|FinanceJoshua|镜像名称。

 |
|ImageOwnerAlias|String|否|self|镜像来源。取值范围：

 -   system：阿里云提供的公共镜像。
-   self：您创建的自定义镜像。
-   others：其他阿里云用户共享给您的镜像。
-   marketplace：镜像市场提供的镜像。您查询到的云市场镜像可以直接使用，无需提前订阅。您需要自行留意云市场镜像的收费详情。

 默认值：空，空表示返回取值为system、self以及others的结果。

 |
|InstanceType|String|否|ecs.g5.large|指定实例类型可以使用的镜像。

 |
|IsSupportCloudinit|Boolean|否|true|镜像是否支持 Cloud Init。

 |
|IsSupportIoOptimized|Boolean|否|true|镜像是否可以运行在I/O优化实例上。

 |
|OSType|String|否|linux|镜像的操作系统类型。取值范围：

 -   windows
-   linux

 |
|PageNumber|Integer|否|1|镜像资源列表的页码。起始值：1

 默认值：1

 |
|PageSize|Integer|否|10|分页查询时设置的每页行数。最大值：100

 默认值：10

 |
|ResourceGroupId|String|否|rg-resourcegroupid1|自定义镜像所在的企业资源组 ID。

 |
|ShowExpired|Boolean|否|false|订阅型镜像是否已经超过使用期限。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用其他参数。

 |
|SnapshotId|String|否|s-snapshotid1|根据某一快照ID创建的自定义镜像。

 |
|Status|String|否|Available|查询某种状态下的镜像。取值范围：

 -   Creating：镜像正在创建中。
-   Waiting：多任务排队中。
-   Available（默认）：您可以使用的镜像。
-   UnAvailable：您不能使用的镜像。
-   CreateFailed：创建失败的镜像。

 支持同时取多个值，值之间以半角逗号（,）隔开。

 |
|Tag.N.Key|String|否|FinanceJoshua|镜像的标签键。N 的取值范围：1~20。一旦传入该值，则不允许为空字符串。最多支持 64 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。

 |
|Tag.N.Value|String|否|FinanceDept|镜像的标签值。N 的取值范围：1~20。一旦传入该值，可以为空字符串。最多支持 128 个字符，不能以 aliyun 和 acs: 开头，不能包含 http:// 或者 https:// 。

 |
|Tag.N.key|String|否|FinanceJoshua|镜像的标签键。

 **说明：** 该参数即将被弃用，为提高兼容性，建议您尽量使用Tag.N.Key参数。

 |
|Tag.N.value|String|否|FinanceDept|镜像的标签值。

 **说明：** 该参数即将被弃用，为提高兼容性，建议您尽量使用Tag.N.Value参数。

 |
|Usage|String|否|instance|镜像是否已经运行在ECS实例中。取值范围：

 -   instance：镜像处于运行状态，有ECS实例使用。
-   none：镜像处于闲置状态，暂无ECS实例使用。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Images| | |镜像信息ImageType组成的集合

 |
|└Architecture|String|x86\_64|镜像系统类型：

 -   i386
-   x86\_64

 |
|└CreationTime|String|2018-01-10T01:01:10Z|镜像的创建时间

 |
|└Description|String|FinanceDept|描述信息

 |
|└DiskDeviceMappings| | |镜像下包含磁盘和快照的系统描述

 |
|└Device|String|/dev/xvdb|生成磁盘的Device信息：比如/dev/xvdb

 |
|└Format|String|qcow2|镜像格式

 |
|└ImportOSSBucket|String|testEcsImport|导入镜像的oss的bucket

 |
|└ImportOSSObject|String|imageImport|导入镜像文件的所属OSS的object

 |
|└Progress|String|32%|对于复制中的镜像, 返回复制任务的进度

 |
|└RemainTime|Integer|213|对于复制中的镜像, 返回复制任务的剩余时间，单位为秒

 |
|└Size|String|80|生成磁盘的大小

 |
|└SnapshotId|String|s-snapshotid1|快照ID

 |
|└Type|String|custom|镜像的类型。

 |
|└ImageId|String|m-imageid1|镜像编码

 |
|└ImageName|String|Joshua-Finance|镜像的名称

 |
|└ImageOwnerAlias|String|self|镜像所有者别名有效值：

 -   system – 系统公共镜像
-   self – 用户的自定义镜像
-   others – 其他用户的公开镜像
-   marketplace -镜像市场镜像

 |
|└ImageVersion|String|2|镜像版本

 |
|└IsCopied|Boolean|false|是否是拷贝的镜像

 |
|└IsSelfShared|String|true|是否共享过该自定义镜像给其他用户。

 |
|└IsSubscribed|Boolean|false|用户是否订阅了该镜像的商品码对应的镜像商品的服务条款.

 -   true：表示已经订阅
-   false：表示未订阅

 |
|└IsSupportCloudinit|Boolean|true|是否支持 Cloud Init。

 |
|└IsSupportIoOptimized|Boolean|true|是否可以在 I/O 优化实例上运行。

 |
|└OSName|String|Aliyun Linux 17.1|操作系统的显示名称

 |
|└OSType|String|Linux|操作系统类型，可选值有：

 -   windows
-   linux

 |
|└Platform|String|Aliyun Linux|操作系统平台

 |
|└ProductCode|String|jxsc000204|镜像市场的镜像商品标示

 |
|└Progress|String|100|镜像完成的进度，单位为百分比

 |
|└ResourceGroupId|String|rg-resourcegroupid1|镜像所在的企业资源组 ID。

 |
|└Size|Integer|80|镜像大小

 |
|└Status|String|Available|镜像的状态，可能的值有：

 -   UnAvailable 不可用
-   Available 可用
-   Creating 创建中
-   CreateFailed 创建失败

 |
|└Tags| | |镜像的标签对信息。

 |
|└TagKey|String|FinanceDept|镜像的标签键。

 |
|└TagValue|String|FinanceJoshua|镜像的标签值。

 |
|└Usage|String|none|有引用关系的资源类型，可能值：

 -   instance
-   none

 |
|PageNumber|Integer|1|当前页码

 |
|PageSize|Integer|10|当前分页包含多少条目

 |
|RegionId|String|cn-hangzhou|镜像所属地域ID

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID

 |
|TotalCount|Integer|24|镜像资源总数

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeImages
&RegionId=cn-hangzhou
&Usage=instance
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeImagesResponse>
  <Images>
    <Image>
      <Architecture>i386</Architecture>
      <CreationTime>2014-07-22T09:53:44Z</CreationTime>
      <Description/>
      <DiskDeviceMappings>
        <DiskDeviceMapping>
          <Device>/dev/xvda</Device>
          <Size>20</Size>
          <SnapshotId/>
        </DiskDeviceMapping>
      </DiskDeviceMappings>
      <ImageId>suse11sp3_64_20G_aliaegis_20150428.vhd</ImageId>
      <ImageName>suse11sp3_64_20G_aliaegis_20150428.vhd</ImageName>
      <ImageOwnerAlias>system</ImageOwnerAlias>
      <ImageVersion>1.0</ImageVersion>
      <IsCopied>false</IsCopied>
      <IsSubscribed>false</IsSubscribed>
      <OSName>SUSE Linux  Enterprise Server 11 SP3 64位</OSName>
      <ProductCode/>
      <OSType>linux</OSType>
      <Platform>SUSE</Platform>
      <Progress>100</Progress>
      <Size>20</Size>
      <Status>Available</Status>
      <Usage>instance</Usage>
    </Image>
  </Images>
  <PageNumber>1</PageNumber>
  <PageSize>2</PageSize>
  <RegionId>cn-hangzhou</RegionId>
  <TotalCount>24</TotalCount>
  <RequestId>7871BB26-3002-4950-B2E6-98D333077EA5</RequestId>
</DescribeImagesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":24,
	"PageSize":1,
	"RequestId":"49CBCED4-C9B9-4851-BEB5-8FB5E5169E30",
	"RegionId":"cn-hangzhou",
	"Images":{
		"Image":[
			{
				"ImageId":"suse11sp3_64_20G_aliaegis_20150428.vhd",
				"OSType":"linux",
				"Architecture":"x86_64",
				"OSName":"SUSE Linux  Enterprise Server 11 SP3 64位",
				"DiskDeviceMappings":{
					"DiskDeviceMapping":[
						{
							"Device":"/dev/xvda",
							"Size":"20"
						}
					]
				},
				"ImageOwnerAlias":"system",
				"Progress":"100%",
				"Usage":"instance",
				"CreationTime":"2015-05-06T09:01:32Z",
				"Status":"Available",
				"ImageVersion":"1",
				"ImageName":"suse11sp3_64_20G_aliaegis_20150428.vhd",
				"IsCopied":false,
				"IsSubscribed":false,
				"Platform":"SUSE",
				"Size":20
			}
		]
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidImageOwnerAlias.ValueNotSupported|The specified ImageOwnerAlias value is not supported.|无效的镜像所有者别名，请您检查该参数是否正确。|
|400|InvalidParamter|Invalid Parameter|指定的参数不合法。|
|404|InvalidFilterKey.NotFound| |指定的起始时间或到期时间参数错误。|
|404|InvalidFilterValue| |您输了的时间格式不合法。|
|404|InvalidUsage|The specifed Usage is not valid|指定有引用关系的资源类型（image、disk、image\_disk、none）不合法。|
|400|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|指定的 Tag.n.Key 和 Tag.n.Value 不匹配。|
|400|InvalidTagCount|The specified tags are beyond the permitted range.|指定的标记超出取值范围。|
|400|InvalidInstanceType.ValueNotSupported|The specified InstanceType does not exist or beyond the permitted range.|指定的实例规格不支持。|
|404|InvalidOSType|The specifed OSType is not valid|不支持指定的操作系统。|
|404|InvalidArchitecture|The specifed Architecture is not valid|指定的架构不存在。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

