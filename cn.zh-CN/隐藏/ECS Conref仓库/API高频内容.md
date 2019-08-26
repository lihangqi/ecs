# API高频内容 {#EcsApiConrefWarehouse .reference}

## 外链 {#External .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

全是公共错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

[ECS管理控制台](https://ecs.console.aliyun.com/)

[提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex)

## 内链 {#Internal .section}

全是公共返回参数。参阅[公共返回参数](../../../../intl.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

被[安全控制](intl.zh-CN/API 参考/附录/安全锁定时的 API 行为.md#)的ECS实例的`OperationLocks`不能标记为`"LockReason" : "security"`。

[实例规格族](../../../../intl.zh-CN/产品简介/实例规格族.md#)

[已停售的实例规格](https://www.alibabacloud.com/help/faq-detail/55263.htm)

您可以调用[DescribeRegions](../../../../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。

保证请求幂等性。从您的客户端生成一个参数值，确保不同请求间该参数值唯一。只支持ASCII字符，且不能超过64个字符。更多详情，请参阅[如何保证幂等性](intl.zh-CN/API 参考/附录/如何保证幂等性.md#)。

按照[ISO8601](intl.zh-CN/API 参考/附录/时间格式.md#)标准表示，并需要使用UTC时间，格式为yyyy-MM-ddTHH:mm:ssZ。

您使用的RAM用户账号暂不具有`PassRole`的权限，请联系主账号拥有者[授权](../../../../intl.zh-CN/快速入门/为 RAM 用户授权.md#)PassRole权限。

是否只预检此次请求。

-   true：发送检查请求，不会查询资源状况。检查项包括AccessKey是否有效、RAM用户的授权情况和是否填写了必需参数。如果检查不通过，则返回对应错误。如果检查通过，会返回错误码`DryRunOperation`。
-   false：发送正常请求，通过检查后返回2XX HTTP状态码并直接查询资源状况。

默认值：false

