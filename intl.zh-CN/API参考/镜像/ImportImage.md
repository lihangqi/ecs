# ImportImage {#doc_api_1062165 .reference}

导入您已有的镜像文件到云服务器ECS，并作为自定义镜像出现在相应地域中。

## 接口说明 {#description .section}

导入自定义镜像后，您可以使用创建的自定义镜像创建ECS实例（RunInstances）或者更换实例的系统盘（ReplaceSystemDisk）。调用该接口时，您需要注意：

-   您必须提前 [上传镜像文件到对象存储OSS](~~31886~~)。
-   导入镜像的地域必须跟镜像文件上传的OSS Bucket的地域相同。
-   参数`DiskDeviceMapping.n`中n的取值范围为1~17。n为1时表示系统盘，n为2~17时表示数据盘。
-   不能删除正在导入的镜像，只能取消导入镜像任务（[CancelTask](~~25624~~)）。
-   您需要预先通过 [访问控制RAM](~~28627~~) 服务为您授权ECS访问OSS。参阅以下步骤：

    1. 创建角色 `AliyunECSImageImportDefaultRole`。**必须是这个名称**，否则导入镜像会失败。角色的策略为：

    ```
    
            {
    			"Statement": [
    			{
    				"Action": "sts:AssumeRole",
    				"Effect": "Allow",
    				"Principal": {
    				"Service": [
    					"ecs.aliyuncs.com"
    				]
    				}
    			}
            ],
    			"Version": "1"
            }
            
    ```

    2. 在该角色下，添加权限策略`AliyunECSImageImportRolePolicy`。这个策略是ECS导入镜像功能的默认策略，更多详情，请参见[云资源访问授权](https://ram.console.aliyun.com/?spm=5176.2020520101.0.0.64c64df5dfpmdY#/role/authorize?request=%7B%22Requests%22:%20%7B%22request1%22:%20%7B%22RoleName%22:%20%22AliyunECSImageImportDefaultRole%22,%20%22TemplateId%22:%20%22ECSImportRole%22%7D,%20%22request2%22:%20%7B%22RoleName%22:%20%22AliyunECSImageExportDefaultRole%22,%20%22TemplateId%22:%20%22ECSExportRole%22%7D%7D,%20%22ReturnUrl%22:%20%22https:%2F%2Fecs.console.aliyun.com%2F%22,%20%22Service%22:%20%22ECS%22%7D)。或者您也可以创建自定义策略，权限需要包含：

    ```
    
            {
    			"Version": "1",
    			"Statement": [
    			{
    				"Action": [
            				"oss:GetObject",
            				"oss:GetBucketLocation",
            				"oss:GetBucketInfo"
    			],
            			"Resource": "*",
            			"Effect": "Allow"
            			}
    			]
            }
            
    ```


## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=ImportImage)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|源自定义镜像的地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|ImportImage|系统规定参数。取值：ImportImage

 |
|Architecture|String|否|x86\_64|系统架构。取值范围：

 -   i386
-   x86\_64（默认）

 |
|Description|String|否|FinanceDeptJoshua|镜像的描述信息。长度为 2~256 个英文或中文字符，不能以 http:// 和 https:// 开头。默认值：空。

 |
|DiskDeviceMapping.N.Device|String|否|/dev/xvda|指定 DiskDeviceMapping.N.在自定义镜像中的设备名。取值范围：/dev/xvda ~ /dev/xvdz

 |
|DiskDeviceMapping.N.DiskImSize|Integer|否|80|自定义镜像大小。

 **说明：** 该参数即将被弃用，为提高兼容性，请尽量使用 DiskDeviceMapping.N.DiskImageSize 参数。

 |
|DiskDeviceMapping.N.DiskImageSize|Integer|否|80|镜像大小。必须确保系统盘空间≥文件系统空间。取值范围：

 -   n = 1 时，即系统盘：5~500 GiB
-   n = 2~17 时，即数据盘：5~1000 GiB

 导入镜像时，系统自动检测镜像大小，以检测结果为准。

 |
|DiskDeviceMapping.N.Format|String|否|qcow2|镜像格式。取值范围：

 -   RAW
-   VHD
-   qcow2

 导入镜像时，系统自动检测镜像格式，以检测格式为准。

 |
|DiskDeviceMapping.N.OSSBucket|String|否|ecsimageos|镜像文件所在的OSS Bucket。

 |
|DiskDeviceMapping.N.OSSObject|String|否|CentOS\_5.4\_32.raw|镜像文件所在的OSS Object的文件名称（key）。

 |
|ImageName|String|否|FinanceJoshua|镜像名称。长度为 2~128 个英文或中文字符。必须以大小字母或中文开头，不能以 http:// 和 https:// 开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。默认值：空。

 |
|OSType|String|否|linux|操作系统平台类型。取值范围：

 -   windows
-   linux（默认）

 |
|Platform|String|否|Other Linux|操作系统发行版。取值范围：

 -   CentOS
-   Ubuntu
-   SUSE
-   OpenSUSE
-   Debian
-   CoreOS
-   Aliyun
-   Windows Server 2003
-   Windows Server 2008
-   Windows Server 2012
-   Others Linux（默认）
-   Customized Linux

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|ImageId|String|m-imageid2|镜像ID

 |
|RegionId|String|cn-hangzhou|地域ID

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID

 |
|TaskId|String|123-345-2332-22323|导入镜像任务ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=ImportImage
&RegionId=cn-hangzhou
&DiskDeviceMapping.1.Format=qcow2
&DiskDeviceMapping.1.OSSBucket=ecsimageos
&DiskDeviceMapping.1.OSSObject=CentOS_5.4_32.raw
&DiskDeviceMapping.1.DiskImageSize=80
&ImageName=FinanceJoshua
&Description=FinanceDeptJoshua
&Architecture=x86_64
&OSType=linux
&Platform=Other Linux
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ImportImageResponse>
  <RequestId>C8B26B44-0189-443E-9816-D951F59623A9</RequestId>
  <ImageId>Img-231234567</ImageId>
  <ImportTaskId>123-345-2332-22323</ImportTaskId>
</ImportImageResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"ImageId":"Img-231234567",
	"ImportTaskId":"123-345-2332-22323",
	"RequestId":"C8B26B44-0189-443E-9816-D951F59623A9"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|MissingParameter|An input parameter "RegionId" that is mandatory for processing the request is not supplied.|参数 RegionId 不得为空。|
|400|InvalidImageSize|The specified "DiskDeviceMapping.n.DiskImageSize" beyond the permitted range.|指定的镜像不存在。|
|400|InvalidImageFormat.Malformed|The specified Image Format is wrongly formed.|参数 AssociateInstanceType 格式错误。|
|400|InvalidRegionId.NotFound|The specified RegionId does not exist.|指定的 RegionId 不存在，请您检查此产品在该地域是否可用。|
|400|InvalidRegion.NotSupport|The specified region does not support image import or export.|指定的地域暂时不支持此操作。|
|403|ImageIsImporting|The specified Image is importing.|指定镜像正在导入，无法执行操作。|
|403|QuotaExceed.Image|The Image Quota exceeds.|自定义镜像额度已用完。|
|403|ImportImageFailed|Importing image is failed, Please contact the administrator.|导入镜像失败，请联系系统管理员排查。|
|403|InvalidParameter.Malformed|The specified parameter "DiskDeviceMapping.n.Device " is not valid.|指定的参数DiskDeviceMapping.n.Device无效。|
|400|InvalidOSSObject.NotFound|The specified OSS object does not exist in this region.|指定的object不存在。|
|400|InvalidOSSObject.NotFound|The specified OSS object cannot be retrieved.|无法读取指定的OSS object信息。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

