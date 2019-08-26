# DescribeCommands {#doc_api_Ecs_DescribeCommands .reference}

查询您已经创建的云助手命令。只输入参数 Action 和 RegionId，不输入其他任何请求参数，则默认查询您所有可用的命令（CommandId）。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeCommands)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|地域 ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeCommands|系统规定参数。取值：DescribeCommands

 |
|CommandId|String|否|c-7d2a745b412b4601b2d47f6a768d3a14|命令 ID。

 |
|Description|String|否|test|命令描述。

 |
|Name|String|否|Test1|命令的名称，暂不支持模糊查询。

 |
|PageNumber|Long|否|1|当前页码，起始值：1

 默认值：1

 |
|PageSize|Long|否|10|分页查询时设置的每页行数，最大值：50

 默认值：10

 |
|Type|String|否|RunShellScript|命令的类型。取值范围：

 -   RunBatScript：命令为在 Windows 实例中运行的 Bat 脚本
-   RunPowerShellScript：命令为在 Windows 实例中运行的 PowerShell 脚本
-   RunShellScript：命令为在 Linux 实例中运行的 Shell 脚本

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Commands| | |命令数据集类型（CommandSetType）

 |
|└CommandContent|String|Y2QgL3Jvb3Q=|命令内容，以 Base64 编码后传输。

 |
|└CommandId|String|c-7d2a745b412b4601b2d47f6a768d3a14|命令 ID。

 |
|└CreationTime|String|2018-01-05T15:45:02Z|命令创建时间。

 |
|└Description|String|test|命令描述。

 |
|└EnableParameter|Boolean|true|该命令是否启用自定义参数。

 |
|└Name|String|Test1|命令名称。

 |
|└ParameterNames| |\['parameter1','parameter2'\]|通过创建命令时的CommandContent解析出的自定义参数名列表，以列表（List）的形式返回。如未使用自定义参数功能，则返回空值列表。

 |
|└Timeout|Long|3600|超时时间。

 |
|└Type|String|RunShellScript|命令类型。

 |
|└WorkingDir|String|/home/|执行路径。

 |
|PageNumber|Long|1|命令列表页码。

 |
|PageSize|Long|10|每页行数。

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID。

 |
|TotalCount|Long|5|命令总个数。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeCommands
&RegionId=cn-hangzhou
&CommandId=c-7d2a745b412b4601b2d47f6a768d3a14
&Name=Test1
&Description=test
&Type=RunShellScript
&PageNumber=1
&PageSize=10
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeCommandsResponse>
  <TotalCount>5</TotalCount>
  <Commands>
    <Command>
      <Name>Test</Name>
      <WorkingDir/>
      <CommandContent>ZWNobyAxMjM=</CommandContent>
      <Timeout>3600</Timeout>
      <Type>RunShellScript</Type>
      <CommandId>c-7d2a745b412b4601b2d47f6a768d3a14</CommandId>
      <Description>test</Description>
      <EnableParameter>false</EnableParameter>
      <ParameterNames>[]</ParameterNames>
    </Command>
    <Command>
      <Name>Test1</Name>
      <WorkingDir/>
      <CommandContent>Y2QgL3Jvb3Q=</CommandContent>
      <Timeout>3600</Timeout>
      <Type>RunShellScript</Type>
      <CommandId>c-7d2a745b412b4601b2d47f6a768d3a15</CommandId>
      <Description>test1</Description>
      <EnableParameter>false</EnableParameter>
      <ParameterNames>[]</ParameterNames>
    </Command>
    <Command>
      <Name>Test2</Name>
      <WorkingDir/>
      <CommandContent>eXVtIHVwZGF0ZQ==</CommandContent>
      <Timeout>3600</Timeout>
      <Type>RunShellScript</Type>
      <CommandId>c-7d2a745b412b4601b2d47f6a768d3a16</CommandId>
      <Description>test2</Description>
      <EnableParameter>false</EnableParameter>
      <ParameterNames>[]</ParameterNames>
    </Command>
    <Command>
      <Name>Test3</Name>
      <WorkingDir/>
      <CommandContent>c2VydmljZSBuZ2lueCByZWxvYWQ=</CommandContent>
      <Timeout>3600</Timeout>
      <Type>RunShellScript</Type>
      <CommandId>c-7d2a745b412b4601b2d47f6a768d3a17</CommandId>
      <Description>test3</Description>
    </Command>
    <Command>
      <Name>Test4</Name>
      <WorkingDir/>
      <CommandContent>ZWNobyB7e25hbWV9fSA=</CommandContent>
      <Timeout>120</Timeout>
      <Type>RunShellScript</Type>
      <CommandId>c-7d2a745b412b4601b2d47f6a768d3a18</CommandId>
      <Description>test4</Description>
      <EnableParameter>true</EnableParameter>
      <ParameterNames>["name"]</ParameterNames>
    </Command>
  </Commands>
  <PageNumber>1</PageNumber>
  <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId>
  <PageSize>10</PageSize>
</DescribeCommandsResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":5,
	"PageSize":10,
	"RequestId":"E69EF3CC-94CD-42E7-8926-F133B86387C0",
	"Commands":{
		"Command":[
			{
				"Name":"Test",
				"Description":"test",
				"Timeout":3600,
				"CommandContent":"ZWNobyAxMjM=",
				"Type":"RunShellScript",
				"EnableParameter":false,
				"ParameterNames":[],
				"CommandId":"c-7d2a745b412b4601b2d47f6a768d3a14",
				"WorkingDir":""
			},
			{
				"Name":"Test1",
				"Description":"test1",
				"Timeout":3600,
				"CommandContent":"Y2QgL3Jvb3Q=",
				"Type":"RunShellScript",
				"EnableParameter":false,
				"ParameterNames":[],
				"CommandId":"c-7d2a745b412b4601b2d47f6a768d3a15",
				"WorkingDir":""
			},
			{
				"Name":"Test2",
				"Description":"test2",
				"Timeout":3600,
				"CommandContent":"eXVtIHVwZGF0ZQ==",
				"Type":"RunShellScript",
				"CommandId":"c-7d2a745b412b4601b2d47f6a768d3a16",
				"WorkingDir":""
			},
			{
				"Name":"Test3",
				"Description":"test3",
				"Timeout":3600,
				"CommandContent":"c2VydmljZSBuZ2lueCByZWxvYWQ=",
				"Type":"RunShellScript",
				"EnableParameter":false,
				"ParameterNames":[],
				"CommandId":"c-7d2a745b412b4601b2d47f6a768d3a17",
				"WorkingDir":""
			},
			{
				"Name":"Test4",
				"Description":"test4",
				"Timeout":3600,
				"CommandContent":"ZWNobyB7e25hbWV9fSA=",
				"Type":"RunShellScript",
				"EnableParameter":true,
				"ParameterNames":[
					"name"
				],
				"CommandId":"c-7d2a745b412b4601b2d47f6a768d3a18",
				"WorkingDir":""
			}
		]
	}
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|发生未知错误。|
|403|InvalidParam.PageNumber|The specified parameter is invalid.|指定的参数无效。|
|403|InvalidParam.PageSize|The specified parameter is invalid.|指定的参数无效。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

