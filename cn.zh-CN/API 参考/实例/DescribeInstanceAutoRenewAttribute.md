# DescribeInstanceAutoRenewAttribute {#DescribeInstanceAutoRenewAttribute .reference}

查询一台或多台预付费实例自动续费状态。

## 描述 {#section_nzt_pxs_xdb .section}

-   为了方便您了解自己的实例是否为自动续费状态，本接口支持实例续费状态的查询。

-   目前只支持 [包年包月](../../../../cn.zh-CN/产品定价/预付费（包年包月）.md#) 的实例，[按量付费](../../../../cn.zh-CN/产品定价/按量付费.md#) 的实例执行该接口会报错。


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeInstanceAutoRenewAttribute|
|RegionId|String|是|实例所属的地域 ID。您可以调用 [DescribeRegions](cn.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|InstanceId|String|是|实例 ID。支持最多 100 个包年包月实例批量查询，多个实例 ID 以英文逗号分隔。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|InstanceId|String|实例 ID，由系统生成，全局唯一。是访问实例的唯一标识。|
|Duration|Integer|自动续费时长。|
|AutoRenewEnabled|Boolean|是否自动续费。-   true：自动续费类型。
-   false：非自动续费类型。

|
|RenewalStatus|String|是否不再续费的返回信息-   AutoRenewal：自动续费
-   Normal：非自动续费，您需要自行续费 ECS 实例
-   NotRenewal：不再续费。返回该值后，系统不再发送到期提醒，只在到期前第三天发送不续费提醒。不再续费的 ECS 实例可以更改成待续费（`Noramal`） 后，再自行续费或设置为自动续费

|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeInstanceAutoRenewAttribute
&RegionId=cn-hangzhou
&InstanceId=i-instance1,i-instance2
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DescribeInstanceAutoRenewAttributeResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE73368</RequestId>
    <InstanceRenewAttributes>
        <InstanceRenewAttribute>
          <Instance>
            <InstanceId>i-instance1</InstanceId>
            <Duration>0</Duration>
            <AutoRenewEnalbed>false</AutoRenewEnalbed>
            <RenewalStatus>Normal</RenewalStatus>
          </Instance>
          <Instance>
            <InstanceId>i-instance2</InstanceId>
            <Duration>1</Duration>
            <AutoRenewEnalbed>true</AutoRenewEnalbed>
            <RenewalStatus>AutoRenewal</RenewalStatus>
          </Instance>
        </InstanceRenewAttribute>
    </InstanceRenewAttributes>
</DescribeInstanceAutoRenewAttributeResponse>
```

 **JSON 格式** 

```
{
    "InstanceRenewAttributes": {
        "InstanceRenewAttribute": [
            {
                "Duration": 0,
                "InstanceId": "i-instance1",
                "AutoRenewEnabled": false
                "RenewalStatus": "Normal"
            },
            {
                "Duration": 1,
                "InstanceId": "i-instance2",
                "AutoRenewEnabled": true
                "RenewalStatus": "AutoRenewal"
            }
        ]
    },
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE73368"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|Abs.MissingParamter.InstanceId|InstanceId should not be null.|403|`InstanceId` 不能为空。|
|ChargeTypeViolation|Pay-As-You-Go instances do not support this operation.|403|按量付费的实例不支持此操作。|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|由于实例已过期，不支持此操作。|
|InvalidParameter.InvalidInstanceId|The specified instanceId is not valid.|403|指定的 `InstanceId` 无效。|
|InvalidParameter.ToManyInstanceIds|No more than 100 InstanceIds can be specified.|403|指定的 `InstanceId` 数量不能大于 100。|

