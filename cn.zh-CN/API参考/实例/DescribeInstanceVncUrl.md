# DescribeInstanceVncUrl {#doc_api_Ecs_DescribeInstanceVncUrl .reference}

查询一台ECS实例的Web管理终端地址。

## 接口说明 {#description .section}

调用该接口时，您需要注意：

-   管理终端地址的有效期为15秒，调用接口成功后如果15秒内不使用该链接，URL地址自动失效，您需要重新查询。
-   单个管理终端链接的**持久链接**（KeepAlive）时间为60秒，60秒内您管理终端窗口没有任何交互操作时，连接自动断开。
-   如果连接中断，每分钟内重新连接的次数不能超过30次。
-   您需要在链接[https://g.alicdn.com/aliyun/ecs-console-vnc2/0.0.5/index.html?](https://g.alicdn.com/aliyun/ecs-console-vnc2/0.0.5/index.html?)末尾加上`vncUrl=xxxx`、`instanceId=xxx`和`isWindows=True`、`isWindows=False`和`password=XXXXXX`，参数之间使用`&`连接。其中：
    -   参数`vncUrl`：调用接口成功后会返回的`VncUrl`的值。
    -   参数`instanceId`：您的实例ID。
    -   参数`isWindows`：该实例的操作系统是否是Windows系统。取值为`true`表示是Windows系统，取值为`false`表示不是Windows系统。
    -   （可选）参数`password`：该实例的远程连接密码，由六位数字或大小写字母组成。使用该参数时，在连接管理终端处您不需要再输入密码。

        示例：

        ```
        
               https://g.alicdn.com/aliyun/ecs-console-vnc2/0.0.5/index.html?vncUrl=ws%3A%2F%xxx&instanceId=i-wz9hhwq5a6tmxxxxxxx&isWindows=true
               
        ```

        或

        ```
        
               https://g.alicdn.com/aliyun/ecs-console-vnc2/0.0.5/index.html?vncUrl=ws%3A%2F%xxx&instanceId=i-wz9hhwq5a6tmxxxxxxx&isWindows=true&password=111111
               
        ```


## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeInstanceVncUrl)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|InstanceId|String|是|i-AY121018033933eaxxxxxxx|实例ID。

 |
|RegionId|String|是|cn-hangzhou|实例所属的地域ID。您可以调用[DescribeRegions](~~25609~~)查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeInstanceVncUrl|系统规定参数。取值：DescribeInstanceVncUrl

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求ID。

 |
|VncUrl|String|ws%3A%2F%2Fhz01-vncproxy.aliyun.com%2Fwebsockify%2F%3Fs%3DDvh%252FIA%252BYc73gWO48cBx2gBxUDVzaAnSKr74pq30mzqUYgeUMcB%252FbkNixDxdEA996|管理终端Url。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeInstanceVncUrl
&InstanceId=i-AY121018033933eaxxxxxxx
&RegionId=cn-hangzhou
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeInstanceVncUrlResponse>
  <RequestId>1450F2D7-5435-4420-BBC9-49C5xxxxxxxx</RequestId>
  <VncUrl>ws%3A%2F%2Fhz01-vncproxy.aliyun.com%2Fwebsockify%2F%3Fs%3DDvh%252FIA%252BYc73gWO48cBx2gBxUDVzaAnSKr74pq30mzqUYgeUMcB%252FbkNixDxdEA996</VncUrl>
</DescribeInstanceVncUrlResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"VncUrl":"ws%3A%2F%2Fhz01-vncproxy.aliyun.com%2Fwebsockify%2F%3Fs%3DDvh%252FIA%252BYc73gWO48cBx2gBxUDVzaAnSKr74pq30mzqUYgeUMcB%252FbkNixDxdEA996",
	"RequestId":"1450F2D7-5435-4420-BBC9-49C5xxxxxxxx"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidRegionId.NotFound|The specified RegionId does not exist.|指定的 RegionId 不存在，请您检查此产品在该地域是否可用。|
|404|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|指定的实例不存在，请您检查实例ID是否正确。|
|403|IncorrectInstanceStatus|The current status of the resource does not support this operation.|该资源目前的状态不支持此操作。|
|500|InternalError|The request processing has failed due to some unknown error.|内部错误，请重试。如果多次尝试失败，请提交工单|
|403|InstanceNotReady|The specified instance is not ready for use|该资源目前的状态不支持此操作，请您等待一段时间再进行操作，并确认实例目前状态与操作是否冲突。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

