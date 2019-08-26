# DescribeCommands {#doc_api_1030541 .reference}

Views the cloud assistant commands that you have created. If you only specify the Action and RegionId parameters, the system queries all available commands by default.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeCommands) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|Action|String|No|DescribeCommands| The operation that you want to perform. Set the value to DescribeCommands.

 |
|CommandId|String|No|c-7d2a745b412b4601b2d47f6a768d3a14| The ID of the command.

 |
|Description|String|No|test| The description of the command.

 |
|Name|String|No|Test1| The name of the command. Partial command names are not supported.

 |
|PageNumber|Long|No|1| The current page number. Starting value: 1.

 Default value: 1.

 |
|PageSize|Long|No|10| The number of entries per page. Maximum value: 50.

 Default value: 10

 |
|Type|String|No|RunShellScript| The type of the command. Valid values:

 -   RunBatScript: Bat script for Windows-based instances
-   RunPowerShellScript: PowerShell script for Windows-based instances
-   RunShellScript: Shell script for Linux-based instances

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|Commands| | | An array of CommandSetType data.

 |
|└ CommandContent|String|Y2QgL3Jvb3Q=| The content of the command, which is Base64-encoded.

 |
|└CommandId|String|c-7d2a745b412b4601b2d47f6a768d3a14| The ID of the command.

 |
|└Description|String|test| The description of the command.

 |
|└Name|String|Test1| The name of the command.

 |
|└Timeout|Long|3600| The timeout period.

 |
|└Type|String|RunShellScript| The type of the command.

 |
|└WorkingDir|String|/home/| The directory path for command invocation.

 |
|PageNumber|Long|1| The page number of the command list.

 |
|PageSize|Long|10| The number of entries per page.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |
|TotalCount|Long|5| The total number of commands.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeCommands
&RegionId=cn-hangzhou 
&CommandId=c-7d2a745b412b4601b2d47f6a768d3a14
&Name=Test1
&Description=test 
&Type=RunShellScript
&PageNumber=1 
&PageSize=10 
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeCommandsResponse>
    <TotalCount>5</TotalCount>
    <Commands>
        <Command>
                <Name>Test</Name>
                <WorkingDir></WorkingDir>
                <CommandContent>ZWNobyAxMjM=</CommandContent>
                <Timeout>3600</Timeout>
                <Type>RunShellScript</Type>
                <CommandId>c-7d2a745b412b4601b2d47f6a768d3a14</CommandId>
                <Description>test</Description> 
        </Command>
        <Command>
                <Name>Test1</Name>
                <WorkingDir></WorkingDir>
                <CommandContent>Y2QgL3Jvb3Q=</CommandContent>
                <Timeout>3600</Timeout>
                <Type>RunShellScript</Type>
                <CommandId>c-7d2a745b412b4601b2d47f6a768d3a15</CommandId>
                <Description>test1</Description>
        </Command>
        <Command>
                <Name>Test2</Name>
                <WorkingDir></WorkingDir>
                <CommandContent>eXVtIHVwZGF0ZQ==</CommandContent>
                <Timeout>3600</Timeout>
                <Type>RunShellScript</Type>
                <CommandId>c-7d2a745b412b4601b2d47f6a768d3a16</CommandId>
                <Description>test2</Description>
        </Command>
        <Command>
                <Name>Test3</Name>
                <WorkingDir></WorkingDir>
                <CommandContent>c2VydmljZSBuZ2lueCByZWxvYWQ=</CommandContent>
                <Timeout>3600</Timeout>
                <Type>RunShellScript</Type>
                <CommandId>c-7d2a745b412b4601b2d47f6a768d3a17</CommandId>
                <Description>test3</Description>
        </Command>
        <Command>
                <Name>Test4</Name>
                <WorkingDir></WorkingDir>
                <CommandContent>bHM=</CommandContent>
                <Timeout>120</Timeout>
                <Type>RunShellScript</Type>
                <CommandId>c-7d2a745b412b4601b2d47f6a768d3a18</CommandId>
                <Description>test4</Description>
        </Command>
    <PageNumber>1</PageNumber> 
    <RequestId>E69EF3CC-94CD-42E7-8926-F133B86387C0</RequestId> 
    <PageSize>10</PageSize> 
</DescribeCommandsResponse>
```

`JSON` format

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
				"CommandContent": "ZWNobyAxMjM=",
				"Type":"RunShellScript",
				"CommandId":"c-7d2a745b412b4601b2d47f6a768d3a14",
				"WorkingDir":""
			},
			{
				"Name":"Test1",
				"Description":"test1",
				"Timeout":3600,
				"CommandContent":"Y2QgL3Jvb3Q=",
				"Type":"RunShellScript",
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
				"CommandId":"c-7d2a745b412b4601b2d47f6a768d3a17",
				"WorkingDir":""
			},
			{
				"Name":"Test4",
				"Description":"test4",
				"Timeout":3600,
				"CommandContent":"bHM=",
				"Type":"RunShellScript",
				"CommandId":"c-7d2a745b412b4601b2d47f6a768d3a18",
				"WorkingDir":""
			}
		]
	}
}
```

## Error codes {#section_uv0_fp7_o5w .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|500|InternalError.Dispatch|An error occurred when you dispatched the request.|The error message returned when an unknown error occurs.|
|403|InvalidParam.PageNumber|The specified parameter is invalid.|The error message returned when the specified parameter is invalid.|
|403|InvalidParam.PageSize|The specified parameter is invalid.|The error message returned when the specified parameter is invalid.|
|403|InvalidRegionId.CloudAssistant|Current region is not available.|The error message returned when the specified region is unavailable.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

