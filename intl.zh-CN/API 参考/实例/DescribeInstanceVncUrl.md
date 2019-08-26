# DescribeInstanceVncUrl {#DescribeInstanceVncUrl .reference}

查询一台 ECS 实例的 [Web 管理终端](../intl.zh-CN/用户指南/连接实例/使用管理终端连接ECS实例.md#) 地址。

## 描述 {#section_nkr_mss_xdb .section}

调用该接口时，您需要注意：

-   管理终端地址的有效期为 15 秒，调用接口成功后如果 15 秒内不使用该链接，URL 地址自动失效，您需要重新查询。

-   单个管理终端链接的持久链接（KeepAlive）时间为 60 秒，60 秒内您管理终端窗口没有任何交互操作时，连接自动断开。

-   如果连接中断，每分钟内重新连接的次数不能超过 30 次。


**使用方法**

您需要在链接 [https://g.alicdn.com/aliyun/ecs-console-vnc/0.0.7/index.html?](https://g.alicdn.com/aliyun/ecs-console-vnc/0.0.7/index.html?) 末尾加上 `vncUrl=xxxx`、`instanceId=xxx` 和 `isWindows=true`、`isWindows=false` 和 `password=XXXXXX`，参数之间使用 `&` 连接。其中：

-   参数 vncUrl：调用接口成功后会返回的 VncUrl 的值。

-   参数 instanceId：您的实例 ID。

-   参数 isWindows：该实例的操作系统是否是 Windows 系统。取值为 true 表示是 Windows 系统，取值为 false 表示不是 Windows 系统。

-   （可选）参数 password：该实例的远程连接密码，由 6 位数字或大小写字母组成。使用该参数时，在连接管理终端处您不需要再输入密码。

    **示例**：

    ```
    https://g.alicdn.com/aliyun/ecs-console-vnc/0.0.7/index.html?vncUrl=ws%3A%2F%xxx&instanceId=i-wz9hhwq5a6tmxxxxxxx&isWindows=true
    ```

    或

    ```
    https://g.alicdn.com/aliyun/ecs-console-vnc/0.0.7/index.html?vncUrl=ws%3A%2F%xxx&instanceId=i-wz9hhwq5a6tmxxxxxxx&isWindows=true&Password=111111
    ```


## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeInstanceVncUrl|
|RegionId|String|是|实例所属的地域 ID。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|InstanceId|String|是|实例 ID。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|VncUrl|String|管理终端 Url|

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=DescribeInstanceVncUrl
&RegionId=cn-qingdao
&InstanceId=AY121018033933eaxxxxxxx
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<DescribeInstanceVncUrlResponse>
    <RequestId>1450F2D7-5435-4420-BBC9-49C5xxxxxxxx</RequestId>
    <VncUrl>ws%3A%2F%2Fhz01-vncproxy.aliyun.com%2Fwebsockify%2F%3Fs%3DDvh%252FIA%252BYc73gWO48cBx2gBxUDVzaAnSKr74pq30mzqUYgeUMcB%252FbkNixDxdEA996</VncUrl>
</DescribeInstanceVncUrlResponse>
```

**JSON 格式** 

```
{
    "RequestId": "1450F2D7-5435-4420-BBC9-49C514B0157E", 
    "VncUrl": "ws%3A%2F%2Fhz01-vncproxy.aliyun.com%2Fwebsockify%2F%3Fs%3DDvh%252FIA%252BYc73gWO48cBx2gBxUDVzaAnSKr74pq30mzqUYgeUMcB%252FbkNixDxdEA996"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|指定实例的状态需要处于 **运行中** （`Running`）。|
|InstanceNotReady|The specified instance is not ready for use|403|指定的实例正在创建中，请稍后再试。|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|指定的 InstanceId 不存在。|
|InvalidRegionId.NotFound|The specified RegionId does not exist.|404|指定的 RegionId 不存在。|

