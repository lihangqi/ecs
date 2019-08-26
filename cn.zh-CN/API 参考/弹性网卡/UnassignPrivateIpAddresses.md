# UnassignPrivateIpAddresses {#reference_lnv_bdd_n2b .reference}

从一块弹性网卡删除一个或多个辅助私有IP地址。

## 描述 {#section_phk_ddd_n2b .section}

-   只支持 **可用**（`Available`）或者 **已绑定**（`InUse`）状态下的弹性网卡。
-   操作主网卡时，网卡附加的实例必须处于 **运行中**（`Running`）或者 **已停止**（`Stopped`）状态。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：UnassignPrivateIpAddresses|
|NetworkInterfaceId|String|是|弹性网卡ID。|
|PrivateIpAddress.N|Array|是|一个或多个需要删除的辅助私有IP地址。`N` 的取值范围：-   弹性网卡处于 **可用**（`Available`）状态：\[1, 10\]
-   弹性网卡处于 **已绑定**（`InUse`）状态：受到实例规格限制。

|

## 返回参数 {#ResponseParameter .section}

全是公共返回参数。参阅 [公共返回参数](../cn.zh-CN/API 参考/快速入门/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=UnassignPrivateIpAddresses
&NetworkInterfaceId=eni-m5e709m1ytxc4wx7wXXX
&PrivateIpAddress.1=192.168.0.1
&PrivateIpAddress.2=192.168.10.1
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<UnassignPrivateIpAddressesResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE70008</RequestId>
</UnassignPrivateIpAddressesResponse>
```

**JSON 格式** 

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE70008"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.aliyun.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InValidParameter|the parameter\(s\) provided is\(are\) invalid.|400|指定的参数无效。|
|MissingParameter|The input parameter that is mandatory for processing this request is not supplied.|400|您必须指定必需参数。|
|InvalidOperation.InvalidEniState|The operation is not allowed in the current ENI state. Expecting status is ,while current status is.|400|只支持操作 **可用**（`Available`）或者 **已绑定**（`InUse`）状态下的弹性网卡。|
|InvalidIp.IpUnassigned|The specified IP is not assigned on this ENI.|403|未分配指定的辅助私有IP地址。|
|InvalidVSwitchId.IpInvalid|The specified IpAddress is not valid in VSwitch CIDR block.|403|必须从虚拟交换机的IP地址段中选择辅助私有IP地址。|
|Operation.Conflict|ecs task is conflicted.|403|指定的弹性网卡正在处理其他任务，请稍后再试。|
|InvalidEniId.NotFound|The specified EniId is not found.|404|指定的 `NetworkInterfaceId`不存在。|
|InvalidVSwitchId.NotFound|The specified VSwitchId is not found.|404|指定的虚拟交换机不存在。|

