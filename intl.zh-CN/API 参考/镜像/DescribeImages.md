# DescribeImages {#DescribeImages .reference}

查询您可以使用的镜像资源。

## 描述 {#section_jgn_1fz_xdb .section}

-   您可以查询的镜像资源包括您的自定义镜像、阿里云提供的公共镜像、云市场镜像以及其他阿里云用户主动共享给您的共享镜像。

-   支持分页查询，查询结果包括可使用的镜像资源的总数和当前页的镜像资源。每页的数量默认为10条。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeImages|
|RegionId|String|是|实例所属的地域ID。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|ImageId|String|否|镜像ID。单次最多查询100条ID，ID之间用半角逗号（`,`）隔开。|
|Status|String|否|查询某种状态下的镜像。取值范围：-   Creating：镜像正在创建中。
-   Waiting：多任务排队中。
-   Available：您可以使用的镜像。
-   UnAvailable：您不能使用的镜像。
-   CreateFailed：创建失败的镜像。

默认值：Available支持同时取多个值，值之间以半角逗号（`,`）隔开。

|
|SnapshotId|String|否|根据某一快照ID创建的自定义镜像。|
|ImageName|String|否|镜像名称。|
|ImageOwnerAlias|string|否|镜像来源。取值范围：-   system：阿里云提供的公共镜像。
-   self：您创建的自定义镜像。
-   others：其他阿里云用户共享给您的镜像。
-   marketplace：[镜像市场](https://market.aliyun.com/)[云市场](https://marketplace.alibabacloud.com/) 提供的镜像。您查询到的云市场镜像可以直接使用，无需提前订阅。您需要自行留意云市场镜像的收费详情。

默认值：空，空表示返回取值为`system`、`self`以及`others`的结果。|
|Usage|String|否|镜像是否已经运行在ECS实例中。取值范围：-   instance：镜像处于运行状态，有ECS实例使用。
-   none：镜像处于闲置状态，暂无ECS实例使用。

|
|Tag.n.Key|String|否|镜像的标签键。n的取值范围：\[1, 20\]。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun、acs:、http://或者https://开头。|
|Tag.n.Value|String|否|镜像的标签值。n的取值范围：\[1, 20\]。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun、acs:、http://或者https://开头。|
|PageNumber|Integer|否|镜像资源列表的页码。起始值：1默认值：1

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
|RegionId|String|镜像所属地域ID|
|TotalCount|Integer|镜像资源总数|
|PageNumber|Integer|当前页码|
|PageSize|Integer|当前分页包含多少条目|
|Images|Array|镜像信息[ImageType](intl.zh-CN/API 参考/数据类型/ImageType.md#)组成的集合|

## 示例 { .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=DescribeImages
&RegionId=cn-hangzhou
&<公共请求参数>
```

**返回示例**

**XML格式**

```
<DescribeImagesResponse>
    <Images>
        <Image>
            <Architecture>i386</Architecture>
            <CreationTime>2014-07-22T09:53:44Z</CreationTime>
            <Description></Description>
            <DiskDeviceMappings>
                <DiskDeviceMapping>
                    <Device>/dev/xvda</Device>
                    <Size>20</Size>
                    <SnapshotId></SnapshotId>
                </DiskDeviceMapping>
            </DiskDeviceMappings>
            <ImageId>suse11sp3_64_20G_aliaegis_20150428.vhd</ImageId>            
            <ImageName>suse11sp3_64_20G_aliaegis_20150428.vhd</ImageName>
            <ImageOwnerAlias>system</ImageOwnerAlias>
            <ImageVersion>1.0</ImageVersion>
            <IsCopied>false</IsCopied>
            <IsSubscribed>false</IsSubscribed>
            <OSName>SUSE Linux  Enterprise Server 11 SP3 64位</OSName>
            <ProductCode></ProductCode>
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

**JSON格式**

```
{
  "Images": {
    "Image": [
      {
        "Architecture": "x86_64",
        "CreationTime": "2015-05-06T09:01:32Z",
        "DiskDeviceMappings": {
          "DiskDeviceMapping": [
            {
              "Device": "/dev/xvda",
              "Size": "20"
            }
          ]
        },
        "ImageId": "suse11sp3_64_20G_aliaegis_20150428.vhd",
        "ImageName": "suse11sp3_64_20G_aliaegis_20150428.vhd",
        "ImageOwnerAlias": "system",
        "ImageVersion": "1",
        "IsCopied": false,
        "IsSubscribed": false,
        "OSName": "SUSE Linux  Enterprise Server 11 SP3 64位",
        "OSType": "linux",
        "Platform": "SUSE",
        "Progress": "100%",
        "Size": 20,
        "Status": "Available",
        "Usage": "instance"
      }
    ]
  }
  "PageNumber": 1,
  "PageSize": 1,
  "RegionId": "cn-hangzhou",
  "RequestId": "49CBCED4-C9B9-4851-BEB5-8FB5E5169E30",
  "TotalCount": 24
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|InvalidImageOwnerAlias.ValueNotSupported|The specified ImageOwnerAlias value is not supported.|400|参数`ImageOwnerAlias`取值不合法。|
|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|400|指定的`Tag.n.Key`和`Tag.n.Value`必须键值匹配。|
|InvalidTagCount|The specified tags are beyond the permitted range.|400|指定的标签数不能超过五个。|
|DryRunOperation|Request validation has been passed with DryRun flag set.|400|此次DryRun预检请求合格。|
|InvalidUsage|The specifed Usage is not valid|404|指定的`Usage`不合法。|

