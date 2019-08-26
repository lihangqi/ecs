# CreateLaunchTemplate {#CreateLaunchTemplate .reference}

创建一个实例启动模板，简称模板。实例启动模板能免除您每次创建实例时都需要填入大量配置参数。

## 描述 {#section_whw_2sn_12b .section}

实例启动模板中包含用于创建实例的相关配置，例如实例所属地域、镜像ID、实例规格、安全组ID和公网带宽等。如果模板中没有指定某一实例配置，您需要在创建实例时为实例指定该配置。创建模板（CreateLaunchTemplate）后，模板的初始版本为1，您可以后续基于该版本创建多个模板版本（CreateLaunchTemplateVersion），版本号从1开始顺序递增。如果您在创建实例（[RunInstances](intl.zh-CN/API 参考/实例/RunInstances.md#)）时不指定模板版本号，会采用默认版本。

调用该接口时，您需要注意：

-   您最多能在一个地域内创建30个实例启动模板，且每个模板最多能有30 个版本。

-   实例启动模板的参数大多数为可选参数。创建模板时，我们不会验证模板中参数取值的存在性和有效性。只会在真正创建实例时校验参数取值的有效性。

-   如果实例启动模板中设置了某一配置，创建实例（[RunInstances](intl.zh-CN/API 参考/实例/RunInstances.md#)）时就无法过滤掉该配置。例如，如果模板设置了`HostName=LocalHost`，RunInstances中`HostName`取值为空时，实例的主机名依然是`LocalHost`。如果您想覆盖`HostName=LocalHost`这一配置，可以在RunInstances中取`HostName=MyHost`或其他参数值。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：CreateLaunchTemplate|
|RegionId|String|是|地域ID。您可以调用 [DescribeRegions](intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|LaunchTemplateName|String|是|实例启动模板名称。长度为\[2, 128\]个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。|
|VersionDescription|String|否|实例启动模板版本1描述。长度为\[2, 256\]个英文或中文字符，不能以http://和https://开头。|
|ImageId|String|否|镜像ID。|
|InstanceType|String|否|实例类型。更多详情，请调用[DescribeInstanceTypes](intl.zh-CN/API 参考/实例/DescribeInstanceTypes.md#)接口获得最新的规格表。|
|SecurityGroupId|String|否|安全组ID。|
|NetworkType|String|否|实例网络类型。取值范围：classic | vpc|
|VSwitchId|String|否|创建VPC类型实例时需要指定虚拟交换机ID。|
|InstanceName|String|否|实例名称。长度为\[2, 128\]个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。|
|Description|String|否|实例描述。长度为\[2, 256\]个英文或中文字符，不能以http://和https://开头。|
|InternetMaxBandwidthIn|String|否|公网入带宽最大值，单位为Mbit/s。取值范围：\[1,200\]|
|InternetMaxBandwidthOut|String|否|公网出带宽最大值，单位为Mbit/s。取值范围：\[0, 100\]|
|HostName|String|否|实例主机名。-   点号（.）和短横线（-）不能作为首尾字符，更不能连续使用。
-   Windows实例：字符长度为\[2, 15\]，不支持点号（.），不能全是数字。允许大小写英文字母、数字和短横线（-）。
-   其他类型实例（Linux等）：字符长度为\[2, 64\]，支持多个点号（.），点之间为一段，每段允许大小写英文字母、数字和短横线（-）。

|
|ZoneId|String|否|实例所属的可用区ID。|
|SystemDisk.Category|String|否|系统盘的磁盘种类。取值范围：-   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   ephemeral\_ssd：本地SSD盘

|
|SystemDisk.Size|Integer|否|系统盘大小，单位为GiB。取值范围：\[20, 500\]|
|SystemDisk.DiskName|String|否|系统盘名称。长度为\[2, 128\]个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。|
|SystemDisk.Description|String|否|系统盘描述。长度为\[2, 256\]个英文或中文字符，不能以http://和https://开头。|
|DataDisk.n.Category|String|否|数据盘的磁盘种类，`n`的取值范围为 \[1, 16\]。取值范围：-   cloud：普通云盘
-   cloud\_efficiency：高效云盘
-   cloud\_ssd：SSD云盘
-   ephemeral\_ssd：本地SSD盘

|
|DataDisk.n.Size|Integer|否|数据盘的容量大小，`n`的取值范围为 \[1, 16\]。取值范围：-   cloud：\[5, 2000\]
-   cloud\_efficiency：\[20, 32768\]
-   cloud\_ssd：\[20, 32768\]
-   ephemeral\_ssd：\[5, 800\]

|
|DataDisk.n.SnapshotId|String|否|创建数据盘使用的快照，`n`的取值范围为\[1, 16\]。|
|DataDisk.n.Encrypted|Boolean|否|是否加密数据盘，`n`的取值范围为\[1, 16\]。|
|DataDisk.n.DiskName|String|否|数据盘名称，`n`的取值范围为\[1, 16\]。长度为\[2, 128\]个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。|
|DataDisk.n.Description|String|否|数据盘描述，`n`的取值范围为\[1, 16\]。长度为\[2, 256\]个英文或中文字符，不能以http://和https://开头。|
|DataDisk.n.DeleteWithInstance|Boolean|否|数据盘是否随实例释放而释放，`n`的取值范围为 \[1, 16\]。|
|IoOptimized|String|否|是否为I/O优化实例。取值范围：-   none：非I/O优化
-   optimized：I/O优化

|
|NetworkInterface.n.PrimaryIpAddress|String|否|弹性网卡的主私有IP地址。|
|NetworkInterface.n.VSwitchId|String|否|第`n` 个弹性网卡所属的虚拟交换机ID。实例与弹性网卡必须在同一VPC的同一可用区中，可以分属于不同交换机。`n`的取值范围参见实例规格族。|
|NetworkInterface.n.SecurityGroupId|String|否|所属的安全组ID必须是同一个VPC下的安全组。`n`的取值范围参见[实例规格族](../intl.zh-CN/产品简介/实例规格族.md#)。|
|NetworkInterface.n.NetworkInterfaceName|String|否|弹性网卡名称。`n`的取值范围参见[实例规格族](../intl.zh-CN/产品简介/实例规格族.md#)。|
|NetworkInterface.n.Description|String|否|弹性网卡描述信息。长度为\[2, 256\]个英文或中文字符，不能以http://和https://开头。|
|InternetChargeType|String|否|公网带宽计费类型。取值范围：PayByTraffic|
|UserData|String|否|实例自定义数据，需要以Base64方式编码，原始数据最多为16 KB。|
|KeyPairName|String|否|密钥对名称。-   Windows实例，忽略该参数。默认为空。即使填写了该参数，仍旧只执行`Password`的内容。
-   Linux实例的密码登录方式会被初始化成禁止。

|
|RamRoleName|String|否|实例RAM角色名称。您可以使用*RAM* API [ListRoles](../../../../../intl.zh-CN/API参考/API 参考（RAM）/角色管理接口/ListRoles.md#)查询实例RAM角色名称。|
|AutoReleaseTime|String|否|实例自动释放时间。按照[ISO8601](../intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|
|SpotStrategy|String|否|后付费实例的抢占策略。当创建实例接口中的`InstanceChargeType`参数取值为`PostPaid`时为生效。取值范围：-   NoSpot：正常按量付费实例。
-   SpotWithPriceLimit：设置上限价格的抢占式实例。
-   SpotAsPriceGo：系统自动出价，最高按量付费价格。

|
|SpotPriceLimit|Float|否|设置实例的每小时最高价格。支持最多3位小数。|
|SecurityEnhancementStrategy|String|否|是否开启安全加固。取值范围：Active | Deactive|
|Tag.n.Key|String|否|实例、安全组、磁盘和网卡的标签键。n的取值范围：\[1, 20\]。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun、acs:、http://或者https://开头。|
|Tag.n.Value|String|否|实例、安全组、磁盘和网卡的标签值。n的取值范围：\[1, 20\]。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun、acs:、http://或者https://开头。|
|TemplateTag.n.Key|String|否|启动模板的标签键。n的取值范围：\[1, 20\]。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun、acs:、http://或者https://开头。|
|TemplateTag.n.Value|String|否|启动模板的标签值。n的取值范围：\[1, 20\]。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun、acs:、http://或者https://开头。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|LaunchTemplateId|String|实例启动模板ID|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=CreateLaunchTemplate
&RegionId=cn-hangzhou
&LaunchTemplateName=lt-name1
&InstanceType=ecs.cm4.6xlarge
&SecurityGroupId=sg-securitygroupid
&<公共请求参数>
```

**返回示例**

**XML格式**

```
<CreateLaunchTemplateResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FExxxxx</RequestId>
    <LaunchTemplateId>lt-m5eiaupmvm2op9dxxxxx</LaunchTemplateId>
</CreateLaunchTemplateResponse>
```

**JSON格式**

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FExxxxx",
    "LaunchTemplateId": "lt-m5eiaupmvm2op9dxxxxx"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|MissingParameter|The input parameter that is mandatory for processing this request is not supplied.|400|必需参数缺失。|
|InvalidParameter|the parameter\(s\) provided is\(are\) invalid.|400|指定的参数不合法。|
|InvalidLaunchTemplateName.Malformed|The specified parameter LaunchTemplateName is not valid.|400|指定的`LaunchTemplateName`不合法。|
|InvalidDescription.Malformed|The specified parameter “VersionDescription” is not valid.|400|指定的`VersionDescription`不合法。|
|InvalidUserData.SizeExceeded|The specified parameter UserData exceeds the size.|400|`UserData`原始数据最多为16 KB。|
|InvalidUserData.Base64FormatInvalid|The specified parameter UserData must be base64 encoded.|400|`UserData`必须经过Base64编码。|
|LaunchTemplateLimitExceed|The maximum number of templates is exceeded.|403|您最多能在一个地域内创建30个实例启动模板。|
|LaunchTemplateName.Duplicated|The specified LaunchTemplateName “\{0\}” already exist.|403|指定的`LaunchTemplateName`已存在。|
|InnerServiceFailed|call inner service failed|403|服务器内部错误。|

