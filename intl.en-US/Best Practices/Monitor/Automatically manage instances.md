# Automatically manage instances {#task7631 .task}

ECS instances maintenance aims to keep ECS instances in the best state and guarantee the troubleshooting efficiency. However, manual maintenance involves a huge amount of time and effort. To address this issue, you can use cloud assistant for automation and batch processing of daily maintenance tasks. This topic illustrates how to automatically maintain ECS instances by invoking cloud assistant commands on ECS instances.

Cloud assistant supports the following three command types.

|Command type|Parameter|Description|
|:-----------|:--------|:----------|
|Shell script|RunShellScript|A shell script that is running on running Linux instances.|
|PowerShell script|RunPowerShellScript|A PowerShell script that is running on running Windows instances.|
|Bat script|RunBatScript|A Bat script that is running on running Windows instances.|

Prerequisites

-   You must make sure that the network type of the target ECS instances is [VPC](../../../../intl.en-US/Product Introduction/What is VPC?.md#).
-   The target ECS instances must be in the **Running** \(`Running`\) status.
-   The target ECS instances must have the Cloud Assistant client installed in advance. For more information, see [Cloud Assistant Client](../../../../intl.en-US/Product Introduction/Cloud assistant/Cloud Assistant Client.md#).
-   To perform a PowerShell command, you must make sure that the target Windows instances has the PowerShell feature configured.
-   You can get the latest version of Alibaba Cloud CLI from [GitHub](https://github.com/aliyun/aliyun-cli/releases) .
-   You must make sure that you have installed [Alibaba Cloud CLI \(Command-Line Interface\)](https://www.alibabacloud.com/help/doc-detail/66653.htm) .
-   You must [have your SDK upgraded](https://develop.aliyun.com/tools/sdk).

The following example illustrates how to use APIs in Alibaba Cloud CLI to use Cloud Assistant. For example, we want to run the `echo 123` command on Linux instances.

1.  In the CMD, PowerShell, or Shell of a local computer, run `aliyuncli ecs CreateCommand --CommandContent ZWNobyAxMjM= --Type RunShellScript --Name test --Description test` to [create a shell script](../../../../intl.en-US/API Reference/Cloud assistant/CreateCommand.md#) \(`CreateCommand`\). The Command ID information is returned after successful creation. 

    **Note:** 

    -   The `ZWNobyAxMjM=` in `CommandContent` is the Base64 code of the `echo 123` command. For more information about Base64 encoding or decoding, see [Wikipedia - Base64](https://en.wikipedia.org/wiki/Base64).
    -   If the operating system of the target ECS instances are Windows, change `type` to `RunBatScript` or `RunPowershellScript`.
    -   After the script is created, `CommandId` is returned.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9821/154155354111647_en-US.png)

2.  Run `aliyuncli ecs InvokeCommand --InstanceId.1 your-vm-instance-id1 --InstanceId.2 your-vm-instance-id2 --CommandId your-command-id --Timed false` to [run the command](../../../../intl.en-US/API Reference/Cloud assistant/InvokeCommand.md#) \(`InvokeCommand`\). 

    **Note:** 

    -   The `InstanceIds` indicates your ECS instances IDs. Up to 100 ECS instances are supported each time.
    -   The `Timed` indicates whether the task is a periodical one or not. `--Timed True` indicates that the task is a periodical one, while `--Timed False` indicates the opposite.
    -   When your task is a periodical one and the `Timed` parameter value is `True`, you must specify the interval value in the `Frequency` parameter. For example, `0 */20 * * * *` indicates that the interval value is 20 minutes. For more information, see [expressions](https://www.alibabacloud.com/help/doc-detail/64769.html).
    -   A shared `InvokeId` is returned for all target ECS instances. You can use the `InvokeId` to check the invocation status of the command.
3.  Optional. Run `aliyuncli ecs DescribeInvocations --InstanceId your-vm-instance-id --InvokeId your-invoke-id` to [query the invocation status](../../../../intl.en-US/API Reference/Cloud assistant/DescribeInvocations.md#) \(`DescribeInvocations`\). Specifically, the `InvokeId` is the invocation ID returned in [step 2](#) during command invocation on the ECS instances. 

    When the returned `InvokeStatus` value is `Finished`, it indicates that the command process is complete, but not necessarily as effective as expected. You must check the `Output` parameter in [DescribeInvocationResults](../../../../intl.en-US/API Reference/Cloud assistant/DescribeInvocationResults.md#) to get the specific invocation result.

4.     

    \(Optional\). Run `aliyuncli ecs DescribeInvocationResults --InstanceId your-vm-instance-id --InvokeId your-invoke-id` to [check the results of the invocation](../../../../intl.en-US/API Reference/Cloud assistant/DescribeInvocationResults.md#) \(`DescribeInvocationResults`\). Specifically, the `InvokeId` is the invocation ID returned in [step 2](#) during command invocation on the ECS instances.


When [creating a command](../../../../intl.en-US/API Reference/Cloud assistant/CreateCommand.md#) \(`CreateCommand`\), you can set the following request parameters for the command.

|Command Property|Parameter|Description|
|----------------|---------|-----------|
|Execution directory|WorkingDir|Specifies the path in an ECS instance where the command is performed. Default value: -   For Linux instances: /root.
-   For Windows instances: In the path where the cloud assistant client process is located, such as C:\\ProgramData\\aliyun\\assist\\$\(version\).

 |
|Timeout period|TimeOut| Modifies the invocation timeout value of a command on ECS instances. The unit is seconds.

 When your command fails for some reason, the invocation may time out, and the cloud assistant client forces to terminate the command process afterwards.

 The parameter value must be greater than or equal to 60. If the value is smaller than 60, the timeout value is 60 seconds by default.

 Default value: 3600

 -   **One-time invocation**:
    -   After invocation timeout, the command invocation status \([DescribeInvocationResults](../../../../intl.en-US/API Reference/Cloud assistant/DescribeInvocationResults.md#)\) for the specified ECS instances becomes Failed.
-   **Periodical invocation**:
    -   The timeout value of periodical invocation is effective for every invocation record.
    -   After one invocation operation timed out, the status for the invocation record \([DescribeInvocationResults](../../../../intl.en-US/API Reference/Cloud assistant/DescribeInvocationResults.md#)\) becomes Failed.
    -   The timeout status of last invocation does not affect the next invocation.

 |

Sample of Python SDK to use cloud assistant

You can also use the cloud assistant by using the [Alibaba Cloud SDK](https://develop.aliyun.com/tools/sdk#/python). For more information about how to configure Alibaba Cloud SDK, see [for Alibaba Cloud users](https://www.alibabacloud.com/help/doc-detail/43039.html). The following is the Python SDK code to use cloud assistant.

```language-shell
# coding=utf-8
# if the python sdk is not install using 'sudo pip install aliyun-python-sdk-ecs'
# if the python sdk is install using 'sudo pip install --upgrade aliyun-python-sdk-ecs'
# make sure the sdk version is 2.1.2, you can use command 'pip show aliyun-python-sdk-ecs' to check
import json
import logging
import os
import time
import datetime
import base64
from aliyunsdkcore import client

from aliyunsdkecs.request.v20140526. CreateCommandRequest import CreateCommandRequest
from aliyunsdkecs.request.v20140526. InvokeCommandRequest import InvokeCommandRequest
from aliyunsdkecs.request.v20140526. DescribeInvocationResultsRequest import DescribeInvocationResultsRequest

# configuration the log output formatter, if you want to save the output to file,
# append ",filename='ecs_invoke.log'" after datefmt.
logging.basicConfig(level=logging.INFO,
                    format='%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s',
                    datefmt='%a, %d %b %Y %H:%M:%S',filename='aliyun_assist_openapi_test.log', filemode='w')
#access_key = 'Your Access Key Id'
#acess_key_secrect = 'Your Access Key Secrect'
#region_name = 'cn-shanghai'
#zone_id = 'cn-shanghai-b'

access_key = 'LTAIXXXXXXXXXXXX'
acess_key_secrect = '4dZXXXXXXXXXXXXXXXXXXXXXXXX'
region_name = 'cn-hangzhou'
zone_id = 'cn-hangzhou-f'

clt = client.AcsClient(access_key, acess_key_secrect, region_name)

def create_command(command_content, type, name, description):
    request = CreateCommandRequest()
    request.set_CommandContent(command_content)
    request.set_Type(type)
    request.set_Name(name)
    request.set_Description(description)
    response = _send_request(request)
    if response is None:
        return None
    command_id = response.get('CommandId')
    return command_id;

def invoke_command(instance_id, command_id, timed, cronat):
    request = InvokeCommandRequest()
    request.set_Timed(timed)
    InstanceIds = [instance_id]
    request.set_InstanceIds(InstanceIds)
    request.set_CommandId(command_id)
    request.set_Frequency(cronat)
    response = _send_request(request)
    invoke_id = response.get('InvokeId')
    return invoke_id;

def get_task_output_by_id(instance_id, invoke_id):
    logging.info("Check instance %s invoke_id is %s", instance_id, invoke_id)
    request = DescribeInvocationResultsRequest()
    request.set_InstanceId(instance_id)
    request.set_InvokeId(invoke_id)
    response = _send_request(request)
    invoke_detail = None
    output = None
    if response is not None:
        result_list = response.get('Invocation').get('InvocationResults').get('InvocationResult')
        for item in result_list:
            invoke_detail = item
            output = base64.b64decode(item.get('Output'))
            break;
        return output;

def execute_command(instance_id):
    command_str = 'yum check-update'
    command_id = create_command(base64.b64encode(command_str), 'RunShellScript', 'test', 'test')
    if(command_id is None):
        logging.info('create command failed')
        return

    invoke_id = invoke_command(instance_id, command_id, 'false', '')
    if(invoke_id is None):
        logging.info('invoke command failed')
        return

    time.sleep(15)

    output = get_task_output_by_id(instance_id, invoke_id)
    if(output is None):
        logging.info('get result failed')
        return

    logging.info("output: %s is \n", output)

# send open api request
def _send_request(request):
    request.set_accept_format('json')
    try:
        response_str = clt.do_action(request)
        logging.info(response_str)
        response_detail = json.loads(response_str)
        return response_detail
    except Exception as e:
        logging.error(e)

if __name__ == '__main__':
    execute_command('i-bp17zhpbXXXXXXXXXXXXX')

```

References

The preceding examples demonstrate how to auto manage ECS instances maintenance by using Alibaba Cloud CLI and cloud assistant APIs [CreateCommand](../../../../intl.en-US/API Reference/Cloud assistant/CreateCommand.md#), [InvokeCommand](../../../../intl.en-US/API Reference/Cloud assistant/InvokeCommand.md#), [DescribeInvocations](../../../../intl.en-US/API Reference/Cloud assistant/DescribeInvocations.md#), and [DescribeInvocationResults](../../../../intl.en-US/API Reference/Cloud assistant/DescribeInvocationResults.md#). You can also use other APIs of the cloud assistant:

-    [StopInvocation](../../../../intl.en-US/API Reference/Cloud assistant/StopInvocation.md#): Stops a scheduled command process.
-    [ModifyCommand](../../../../intl.en-US/API Reference/Cloud assistant/ModifyCommand.md#): Modifies the content of a command.
-    [DescribeCommands](../../../../intl.en-US/API Reference/Cloud assistant/DescribeCommands.md#): Queries the available commands.
-    [DeleteCommand](../../../../intl.en-US/API Reference/Cloud assistant/DeleteCommand.md#): Deletes a command.

