# AllocateDedicatedHosts {#AllocateDedicatedHosts .reference}

创建一台或多台按量付费或者预付费专有宿主机。专有宿主机是由单租户独享的物理机资源，您可以在专有宿主机上自行创建 ECS 实例和获取物理服务器属性信息等。

## 描述 {#Details .section}

创建专有宿主机前，您可以调用 [DescribeAvailableResource](cn.zh-CN/API 参考/地域/DescribeAvailableResource.md#) 查看指定地域或者可用区内的资源供给情况。创建专有宿主机前会涉及到资源计费，建议您提前了解计费方式。更多详情，请参阅 [计费概述](../../../../../cn.zh-CN/产品定价/计费概述.md#)。

-   单次最多能创建 100 台预付费或者按量付费专有宿主机。

-   创建成功后，您可以通过返回的专有宿主机 ID 列表和 [DescribeDedicatedHosts](cn.zh-CN/API 参考/专有宿主机/DescribeDedicatedHosts.md#) 查询新建专有宿主机状态。

-   当新建专有宿主机状态为 **可用**（`Available`）后，您可以在宿主机上开始创建 ECS 实例。关于专有宿主机的生命周期状态，请参阅[生命周期](../../../../../cn.zh-CN/产品简介/生命周期.md#)。
-   提交创建任务后，参数不合规或者库存不足的情况下会报错，具体的报错原因参阅 [错误码](#)。

-   创建专有宿主机后，您可以通过 [ModifyInstanceDeployment](cn.zh-CN/API 参考/部署集/ModifyInstanceDeployment.md#) 将ECS实例从共享宿主机迁移到专有宿主机，也可以在两台专有宿主机上调整实例部署。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值 ：AllocateDedicatedHosts|
|RegionId|String|是|专有宿主机所属的地域 ID。您可以调用[DescribeRegions](../cn.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|DedicatedHostType|String|是|专有宿主机规格。您可以调用 [DescribeDedicatedHostTypes](cn.zh-CN/API 参考/专有宿主机/DescribeDedicatedHostTypes.md#) 接口获得最新的专有宿主机规格表 。|
|Quantity|Integer|否|本次创建的专有宿主机的数量。取值范围：\[1, 100\]默认值：1

|
|ZoneId|String|否|专有宿主机所属的可用区编号。默认值：空，表示由系统选择。

|
|DedicatedHostName|String|否|专有宿主机的名称。 长度为\[2, 128\]个英文或中文字符。必须以大小字母或中文开头，不能以http://和https://开头。可以包含数字、半角冒号（:）、下划线（\_）或者连字符（-）。|
|Description|String|否|专有宿主机的描述。长度为\[2, 256\]个英文或中文字符，不能以http://和https://开头。|
|ChargeType|String|否|专有宿主机的计费方式。取值范围：-   PrePaid：预付费，即包年包月。选择预付费时，请确认您的支付方式支持余额或者信用额度支付，否则会提示 `InvalidPayMethod`。
-   PostPaid（默认）：按量付费。

|
|Period|Integer|否|设置订阅专有宿主机的预付费时长，单位：月。取值范围：\[1, 9\] | 12 | 24 | 36**说明：** 当参数 ChargeType 取值为 PrePaid 时，Period 参数方可生效并为必填参数。

|
|AutoRenew|Boolean|否|是否自动续费预付费的专有宿主机。默认值：False**说明：** 当参数 ChargeType 取值 PrePaid 时，AutoRenew 参数方可生效。

|
|AutoRenewPeriod|Integer|否|单次自动续费的周期，单位：月。取值范围：1 | 2 | 3 | 6 | 12**说明：** 当参数 AutoRenew 为 True 时，AutoRenewPeriod 参数方可生效并为必填参数。

|
|AutoReleaseTime|String|否|设置按量付费专有宿主机的自动释放时间。按照[ISO8601](../cn.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。|
|ActionOnMaintenance|String|否|当专有宿主机发生故障或者在线修复时，为其所宿实例设置迁移方案。取值范围：-   Migrate：迁移实例到其他物理机并重新启动实例。

专有宿主机上挂载的是云盘存储时，Migrate 为默认值。

-   Stop：在当前专有宿主机上停止实例，确认无法修复专有宿主机后，迁移实例到其他物理机并重新启动实例。

专有宿主机上挂载的是本地盘存储时，Stop 为默认值。


|
|NetworkAttributes.SlbUdpTimeout|Integer|否|负载均衡连接的 UDP 会话超时时间，单位：秒。取值范围：\[15, 310\]|
|NetworkAttributes.UdpTimeout|Integer|否|为专有宿主机上运行的云服务设置用户访问的 UDP 会话超时时间，单位：秒。取值范围：\[15, 310\]|
|Tag.n.Key|String|否|专有宿主机的标签键。n的取值范围：\[1, 20\]。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun、acs:、http://或者https://开头。|
|Tag.n.Value|String|否|专有宿主机的标签值。n的取值范围：\[1, 20\]。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun、acs:、http://或者https://开头。|
|ClientToken|String|否|保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参阅[如何保证幂等性](../cn.zh-CN/API 参考/附录/如何保证幂等性.md#)。

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|DedicatedHostIdSets|Array of DedicatedHostId|专有宿主机 ID（DedicatedHostId）组成的列表。|

## 示例 {#Samples .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=AllocateDedicatedHosts
&RegionId=cn-hangzhou
&DedicatedHostType=ddh.sn1ne
&Quantity=2
&<公共请求参数>
```

**返回示例**

**XML 格式**

```
<AllocateDedicatedHostsResponse>
  <RequestId>192C4203-ED9E-4BCD-847D-482995C01728</RequestId>
  <DedicatedHostIdSets>
    <DedicatedHostId>dh-dedicatedhost1</DedicatedHostId>
    <DedicatedHostId>dh-dedicatedhost2</DedicatedHostId>
  </DedicatedHostIdSets>
</AllocateDedicatedHostsResponse>
```

**JSON 格式**

```
{
    "RequestId":"E2A664A6-2933-4C64-88AE-5033D003EADF",
    "DedicatedHostIdSets":{
        "DedicatedHostId":[
            "dh-dedicatedhost1",
            "dh-dedicatedhost2"
        ]
    }
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|Account.Arrearage|Your account has an outstanding payment.|400|账号已经欠费。|
|InvalidChargeType.ValueNotSupported|ChargeType is not valid.|400|指定的参数 ChargeType 无效。|
|InvalidDedicatedHostName.Malformed|The specified parameter DedicatedHostName is not valid.|400|指定的 DedicatedHostName 格式无效。|
|InvalidDescription.Malformed|The specified parameter Description is not valid.|400|指定的Description 格式无效。|
|MissingParamter|The specified parameter Period can’t be null|400|当参数 ChargeType 取值为 PrePaid 时，Period 为必填参数。|
|OperationDenied|Sales of this resource are temporarily suspended in the specified region; please try again later.|400|指定地域暂时停售专有宿主机。|
|OperationDenied.NoStock|Sales of this resource are temporarily suspended in the specified region; please try again later.|400|专有宿主机库存不足，请尝试其它资源类型或者切换可用区。|
|QuotaExceed.AfterpayDedicatedHost|Living afterpay dedicated host quota exceeded.|400|您已超过专有宿主机的使用配额。|
|Zone.NotOnSale|The specified zone is not available for purchase.|400|指定可用区无法创建专有宿主机。|
|Forbbiden|User not authorized to operate on the specified resource.|403|您未被授权创建专有宿主机。|
|RegionUnauthorized|User has no authority to create instance in the specified region.|403|您未被授权使用指定地域。|
|Zone.NotOpen|The specified zone is not granted to you to buy resources yet.|403|您未被授权在指定可用区内创建专有宿主机。|
|InvalidDedicatedHostChargeType.NotFound|The DedicatedHostChargeType does not exist in our records.|404|指定的 ChargeType 不存在。|

