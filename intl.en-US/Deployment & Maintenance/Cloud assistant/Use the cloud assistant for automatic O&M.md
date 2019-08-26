# Use the cloud assistant for automatic O&M {#concept_tqb_3gf_5gb .concept}

This topic describes how to run the echo 123 command on multiple ECS instances by using the cloud assistant. With the cloud assistant, you can implement automatic processing of routine maintenance tasks in batches. In this way, you can keep your ECS instances in good condition and guarantee high troubleshooting efficiency.

## Prerequisites {#section_l1h_zjf_5gb .section}

Before you run the echo 123 command, the following conditions must be met:

-   The cloud assistant client is installed on the target instance. For more information, see [Configure the cloud assistant client](intl.en-US/Deployment & Maintenance/Cloud assistant/Configure the cloud assistant client.md#).
-   The instance is in the **Running** state.
-   The network type of the instance is Virtual Private Cloud \(VPC\). For more information, see [What is VPC?](../../../../intl.en-US/Product Introduction/What is VPC?.md#)
-   If the instance is a Windows instance, it must be configured with the PowerShell module before you run PowerShell commands. For more information, see [Installing Windows PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-windows-powershell).

## Method 1: Call API actions in Alibaba Cloud CLI to use the cloud assistant {#section_ikq_wjf_5gb .section}

**Prerequisites**

-   Alibaba Cloud CLI is installed. For more information, see [What is Alibaba Cloud CLI?](https://www.alibabacloud.com/help/doc-detail/66653.htm)
-   The region ID is obtained. For more information, see [Regions and zones](../../../../intl.en-US/General Reference/Regions and zones.md#).

**Procedure**

In this example, only the required parameters are set to their respective default values to call APIs. You can customize commands as needed. For example, you can customize WorkingDir and TimeOut when you create a command.

1.  Optional. Check the instance state. If the instance is not in the **Running** state, call the [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9858.md\#](../../../../intl.en-US/API Reference/Instances/StartInstance.md#) API action to run the target instance.

    ``` {#codeblock_zd6_1fh_pqm}
    aliyun ecs StartInstance --InstanceId i-bp1g6zv0ce8ogXXXXXXp
    ```

2.  Optional. Call the [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_16011.md\#](../../../../intl.en-US/API Reference/Cloud assistant/DescribeCloudAssistantStatus.md#) API action to check whether the cloud assistant client is installed on the target instance.

    ``` {#codeblock_u8d_o8i_g4v}
    aliyun ecs DescribeCloudAssistantStatus --RegionId TheRegionId --InstanceId.1 i-bp1g6zv0ce8ogXXXXXXp --output cols=CloudAssistantStatus
    ```

    If the `CloudAssistantStatus=true` message is returned, it means that the cloud assistant client is installed on the target instance. If this message is not returned, call the [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_16040.md\#](../../../../intl.en-US/API Reference/Cloud assistant/InstallCloudAssistant.md#) API action to install the cloud assistant client.

3.  Call the [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9957.md\#](../../../../intl.en-US/API Reference/Cloud assistant/CreateCommand.md#) API action to create a cloud assistant command named `test`. The script content is `echo 123` and is in Base64-coded plain text.

    ``` {#codeblock_5b9_qbf_ob2}
    aliyun ecs CreateCommand --RegionId TheRegionId --CommandContent ZWNobyAxMjM= --Type RunShellScript --Name test --Description test --Output cols=CommandId
    ```

    The cloud assistant supports the following three command types:

    -   Shell script \(RunShellScript\): supports Linux instances.
    -   PowerShell script \(RunPowerShellScript\): supports Windows instances.
    -   Bat script \(RunBatScript\): supports Windows instances.
    If the target instance is a Windows instance, change the Type parameter to RunBatScript or RunPowershellScript.

    .

4.  Call the [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9958.md\#](../../../../intl.en-US/API Reference/Cloud assistant/InvokeCommand.md#) API action to run the created cloud assistant command for one or more instances.

    ``` {#codeblock_wgb_ke7_bih}
    aliyun ecs InvokeCommand --RegionId TheRegionId --InstanceId.1 i-bp1g6zv0ce8ogXXXXXXp --InstanceId.2 i-bp1g6zv0ce8ogXXXXXXp --CommandId your-command-id --Timed false --Output cols=InvokeId
    ```

    -   Timed indicates whether the command is a periodical task. True means that it is a periodical task, while False means that it is not a periodical task.
    -   If the command is a periodical task, you can set the Frequency. For example, 0 \*/20 \* \* \* \* means that the command is run every 20 minutes. For information about Cron expressions, see [Cron expressions](https://www.alibabacloud.com/help/doc-detail/64769.html).
5.  Call the [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9962.md\#](../../../../intl.en-US/API Reference/Cloud assistant/DescribeInvocations.md#) API action to view the command result. The InvokeId parameter is the ID returned when the command is run.

    ``` {#codeblock_d1y_7ii_ted}
    aliyun ecs DescribeInvocations --RegionId TheRegionId --InvokeId your-invoke-id
    ```

    **Note:** If the response parameter InvokeStatus is Finished, it means that the command process is completed, but the expected result may not be the actual result. You need to check the Output parameter in [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9963.md\#](../../../../intl.en-US/API Reference/Cloud assistant/DescribeInvocationResults.md#) to view the actual command result.

6.  Call the [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9963.md\#](../../../../intl.en-US/API Reference/Cloud assistant/DescribeInvocationResults.md#) API action to view the actual command result of the specified instance.

    ``` {#codeblock_f5k_wkt_xgs}
    aliyun ecs DescribeInvocationResults --RegionId TheRegionId --InstanceId i-bp1g6zv0ce8ogXXXXXXp --InvokeId your-invoke-id
    ```


## Method 2: Call API actions in ECS Python SDK to use the cloud assistant {#section_p5v_zmf_5gb .section}

**Prerequisites**

-   Python SDK v2.1.2 or a later version is installed. For the latest ECS SDK version, visit [GitHub Repo Alibaba Cloud](https://develop.aliyun.com/tools/sdk).
-   The AccessKeyId, AccessKeySecret, and region ID are obtained. For more information, see [Create an AccessKey](../../../../intl.en-US/General Reference/Create an AccessKey.md#) and [Regions and zones](../../../../intl.en-US/General Reference/Regions and zones.md#).

**Example code**

``` {#codeblock_3d0_uhd_bc6 .language-shell}
# coding=utf-8
# If the python sdk is not installed, run 'sudo pip install aliyun-python-sdk-ecs'.
# Make sure you're using the latest sdk version. Run 'sudo pip install --upgrade aliyun-python-sdk-ecs' to upgrade.

import json
import logging
import os
import time
import datetime
import base64
from aliyunsdkcore import client

from aliyunsdkecs.request.v20140526.CreateCommandRequest import CreateCommandRequest
from aliyunsdkecs.request.v20140526.InvokeCommandRequest import InvokeCommandRequest
from aliyunsdkecs.request.v20140526.DescribeInvocationResultsRequest import DescribeInvocationResultsRequest

# configuration the log output formatter, if you want to save the output to file,
# append ",filename='ecs_invoke.log'" after datefmt.
logging.basicConfig(level=logging.INFO,
                    format='%(asctime)s %(filename)s[line:%(lineno)d] %(levelname)s %(message)s',
                    datefmt='%a, %d %b %Y %H:%M:%S',filename='aliyun_assist_openapi_test.log', filemode='w')
#access_key = 'Your Access Key Id'
#acess_key_secrect = 'Your Access Key Secrect'
#region_name = 'cn-shanghai'
#zone_id = 'cn-shanghai-b'

access_key = 'LTAIXXXXXXXXXXXX'  # Enter the actual AccessKey.
acess_key_secrect = '4dZXXXXXXXXXXXXXXXXXXXXXXXX'  # Enter the actual AccessKey Secret.
region_name = 'cn-hangzhou'  # Enter the actual region name.
zone_id = 'cn-hangzhou-f'  # Enter the actual zone ID.

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

## Method 3: Use the cloud assistant in the ECS console {#section_wl1_d3w_vgb .section}

For information on how to use the cloud assistant in the ECS console, see [Create a script](intl.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Create a script.md#).

## Related APIs {#section_ktn_fbj_5gb .section}

The cloud assistant provides the following APIs:

-   [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9957.md\#](../../../../intl.en-US/API Reference/Cloud assistant/CreateCommand.md#): creates a cloud assistant command.
-   [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9958.md\#](../../../../intl.en-US/API Reference/Cloud assistant/InvokeCommand.md#): runs a cloud assistant command on one or more instances.
-   [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9962.md\#](../../../../intl.en-US/API Reference/Cloud assistant/DescribeInvocations.md#): queries the command status.
-   [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9963.md\#](../../../../intl.en-US/API Reference/Cloud assistant/DescribeInvocationResults.md#): queries the command result.
-   [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9959.md\#](../../../../intl.en-US/API Reference/Cloud assistant/StopInvocation.md#): stops a running command process.
-   [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9961.md\#](../../../../intl.en-US/API Reference/Cloud assistant/DescribeCommands.md#): queries a created command.
-   [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_9960.md\#](../../../../intl.en-US/API Reference/Cloud assistant/DeleteCommand.md#): deletes a created command.
-   [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_16011.md\#](../../../../intl.en-US/API Reference/Cloud assistant/DescribeCloudAssistantStatus.md#): checks whether the cloud assistant client is installed on the target instance.
-   [../../../../dita-oss-bucket/SP\_2/DNA0011860945/EN-US\_TP\_16040.md\#](../../../../intl.en-US/API Reference/Cloud assistant/InstallCloudAssistant.md#): installs the cloud assistant client on the target instance.

