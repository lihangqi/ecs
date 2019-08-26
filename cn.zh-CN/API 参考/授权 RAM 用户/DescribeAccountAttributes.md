# DescribeAccountAttributes {#DescribeAccountAttributes .reference}

查询您在一个阿里云地域下能创建的ECS资源上限。包括您能创建的安全组数量、弹性网卡数量、按量付费vCPU核数、抢占式实例vCPU核数、专用宿主机数量、地域网络类型以及账号是否已完成实名认证。

## 描述 {#section_awr_p1k_b2b .section}

[注册](https://account.aliyun.com/register/register.htm) 了阿里云账号后，您可以在不同的阿里云地域中创建一定数量的ECS资源，更多详情，请参阅 [使用限制](../../../../cn.zh-CN/用户指南/使用限制.md#)。您也可以根据自己的需求 [提交工单](https://selfservice.console.aliyun.com/ticket/createIndex.htm) 提高资源使用上限。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeAccountAttributes|
|RegionId|String|是|地域ID。您可以调用 [DescribeRegions](cn.zh-CN/API 参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|ZoneId|String|否|可用区ID。|
|AttributeName.N|String|否|查询某类资源的使用上限，`N`的取值范围为\[1, 8\]。取值范围：-   instance-network-type：当前地域可选择的网络类型。
-   max-security-groups：安全组数量。
-   max-elastic-network-interfaces：当前地域下弹性网卡的数量。
-   max-postpaid-instance-vcpu-count：当前地域下按量实例的vCPU核数。
-   max-spot-instance-vcpu-count：当前地域下抢占式实例vCPU核数。
-   max-delicated-hosts：当前地域下专用宿主机数量。
-   supported-postpaid-instance-types：当前地域下按量付费 I/O 优化实例规格。
-   real-name-authentication：账号是否完成了实名认证。

**说明：** 说明：您只有完成了[实名认证](https://help.aliyun.com/knowledge_list/37170.html) 才可以创建ECS实例。


默认值：空|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|AccountAttributeItem|Array of [AccountAttributeItems](#AccountAttributeItems)|指定地域下账号特权的信息集合|

 **AccountAttributeItems** 

|名称|类型|描述|
|:-|:-|:-|
|AttributeName|String|资源的使用上限分类。可能值:-   instance-network-type：当前地域可选择的网络类型。
-   max-security-groups：安全组数量。
-   max-elastic-network-interfaces：当前地域下弹性网卡的数量。
-   max-postpaid-instance-vcpu-count：当前地域下按量实例的vCPU核数。
-   max-spot-instance-vcpu-count：当前地域下抢占式实例vCPU核数。
-   max-delicated-hosts：当前地域下专用宿主机数量。
-   supported-postpay-instance-types：当前地域下按量付费I/O优化实例规格。
-   real-name-authentication：账号是否完成了实名认证。

|
|AttributeValues|[ValueItem](#ValueItem)|资源的使用上限具体数值。|

 **ValueItem** 

|名称|类型|描述|
|:-|:-|:-|
|Value|String|当前地域或全部地域下某类资源的使用上限具体数值。可能值:-   分类为 `max-security-groups`、`max-elastic-network-interfaces`、`max-postpaid-instance-vcpu-count`、`max-delicated-hosts`、`max-spot-instance-vcpu-count`时：返回0或正整数。
-   分类为 `supported-postpay-instance-types` 时：返回实例规格取值。参阅 [实例规格族](../../../../cn.zh-CN/产品简介/实例规格族.md#)。
-   分类为 `real-name-authentications`时：返回 yes | none | unnecessary
-   分类为 `为instance-network-type` 时：返回 vpc | classic

|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeAccountAttributes
&RegionId=cn-hangzhou&
&<公共请求参数>
```

**返回示例** 

**XML 格式** 

```
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

**JSON 格式** 

```
{
    "AccountAttributeItems": {
        "AccountAttributeItem": [
            {
                "AttributeValues": {
                    "ValueItem": [
                        {
                            "Value": "100"
                        }
                    ]
                },
                "AttributeName": "max-security-groups"
            },
            {
                "AttributeValues": {
                    "ValueItem": [
                        {
                            "Value": "2"
                        }
                    ]
                },
                "AttributeName": "max-dedicated-hosts"
            },
            {
                "AttributeValues": {
                    "ValueItem": [
                        {
                            "Value": "1000"
                        }
                    ]
                },
                "AttributeName": "max-postpaid-instance-vcpu-count"
            },
            {
                "AttributeValues": {
                    "ValueItem": [
                        {
                            "Value": "1000"
                        }
                    ]
                },
                "AttributeName": "max-spot-instance-vcpu-count"
            },
            {
                "AttributeValues": {
                    "ValueItem": [
                        {
                            "Value": "5000"
                        }
                    ]
                },
                "AttributeName": "max-elastic-network-interfaces"
            },
            {
                "AttributeValues": {
                    "ValueItem": [
                        {
                            "Value": "yes"
                        }
                    ]
                },
                "AttributeName": "real-name-authentication"
            },
            {
                "AttributeValues": {
                    "ValueItem": [
                        {
                            "Value": "vpc"
                        }
                    ]
                },
                "AttributeName": "instance-network-type"
            },
            {
                "AttributeValues": {
                    "ValueItem": [
                        {
                            "Value": "ecs.f3-c16f1.4xlarge"
                        },
                        {
                            "Value": "ecs.g5.2xlarge"
                        }
                    ]
                },
                "AttributeName": "supported-postpaid-instance-types"
            }
        ]
    },
    "RequestId": "8CE45CD5-31FB-47C2-959D-CA8144CE9F42"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的 `RegionId` 不存在。|

