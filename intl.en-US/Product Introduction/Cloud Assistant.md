# Cloud Assistant {#concept_qg3_5dx_ydb .concept}

Cloud Assistant helps you execute daily maintenance commands in bulk automatically, run automated O&M scripts, poll the processes, install or uninstall software, update applications, install patches, and more. You can use the Cloud Assistant to manage your ECS instances in a safe and easy manner.

## Billing method {#section_v5p_5dx_ydb .section}

The Cloud Assistant is available free of charge. Note that it is a tool for convenient deployment and O&M of ECS instances. The actual running of ECS instances will incur fees. For more information, see [Pricing overview](../../../../reseller.en-US/Pricing/Pricing overview.md#).

## Details {#section_zfz_wdx_ydb .section}

By installing the Cloud Assistant client on ECS instances, you can run Bat/PowerShell \(for Windows instances\) scripts or Shell scripts \(for Linux instances\) on one or more running \(`Running`\) ECS instances through the ECS console or APIs. The selected instances do not impact each other. You can also set Timed Invocation to keep an ECS instance in a specific status, obtain its monitoring and log information, or run a daemon process. The Cloud Assistant does not initiate any operations. All the operations are under your control.

The following table describes the relevant concepts of the Cloud Assistant.

|Term|Common name|Description|
|:---|:----------|:----------|
|Cloud Assistant|Cloud Assistant|A convenient feature provided by Alibaba Cloud ECS for automated batch invocation of daily maintenance tasks.|
|Cloud Assistant client|Client|The client program that is installed in ECS instances. The task process is included in AliyunService. All operations on ECS instances are performed by using the client.|
|Command|Command|Specific commands to be invoked on ECS instances, such as a Shell script.|
|One-time invocation|Invocation|An occasion when a command is invoked on one or more instances only once \(`Invocation`\).|
|Periodical invocation|Timed Invocation|When you invoke a command on one or more instances, you can specify the invocation sequence/period to run the command periodically.|
|Invocation status|InvokeStatus|The relationship among command invocation status. For more information, see [Lifecycle of command execution](#).|

## Limitations {#section_n5p_5dx_ydb .section}

The Cloud Assistant has the following limitations:

-   You must install and manage the Cloud Assistant as the administrator. Specifically, the Linux instance administrator is root and the Windows instance administrator is administrator.
-   In each Alibaba Cloud region, you can create up to 100 Cloud Assistant commands.
-   In each Alibaba Cloud region, you can run up to 500 Cloud Assistant commands each day.
-   Currently, the Cloud Assistant service is available in all Alibaba Cloud regions except for UK \(London\).
-   For the Timed Invocation commands, the `Timed` interval cannot be less than 10 seconds.
-   The size of Base64-encoded Bat/PowerShell scripts or Shell scripts cannot be greater than 16 KB.
-   The target ECS instance must be in a **Running** \(`Running`\) status.
-   You can only run Cloud Assistant commands in Windows Server 2008/2012/2016, Ubuntu 12/14/16, CentOS 5/6/7, Debian 7/8/9, RedHat 5/6/7, SUSE Linux Enterprise Server 11/12, OpenSUSE, Aliyun Linux, and CoreOS.

## How to use the Cloud Assistant {#section_ivp_5dx_ydb .section}

You must install the [Cloud Assistant client](../../../../reseller.en-US/User Guide/Cloud assistant/Cloud assistant client.md#) on your ECS instance before using the Cloud Assistant.

You can use it through APIs. For more information, see [Automatically manage instances](../../../../reseller.en-US/Best Practices/Monitor/Automatically manage instances.md#).

## Lifecycle of command invocation {#InvocationStatus .section}

A command may have the following status when running on an instance.

|Command status|API status|Description|
|:-------------|:---------|:----------|
|Being executed|`Running`|The command is being executed.|
|Stopped|`Stopped`|You stop a command during its execution.|
|Execution finished|`Finished`|The command invocation is finished. However, this does not mean the invocation is successful. You can check whether the invocation is successful by checking the actual output \(`Output`\) of the command process.|
|Execution failed|`Failed`|The command invocation is not finished for some reason when the timeout time \(`Timeout`\) is reached.|

To facilitate the management of bulk or periodical execution, you can manage the lifecycle of command execution from the perspectives of **overall invocation status**, **instance invocation status**, and **invocation record status**. The relationships among various levels are shown in the following figure.

![](images/5245_en-US.png "Relationships among the invocation status")

|Status|Command invocation|Displayed status|
|:-----|:-----------------|:---------------|
|Overall invocation status|The invocation status of all instances are **Finished** \(`Finished`\).|Finished|
| The invocation status of some instances are **Finished** \(`Finished`\),

 while the status of other instances are **Stopped** \(`Stopped`\).

 |
|The invocation status of all instances are **Failed** \(`Failed`\).|Failed|
|The invocation status of all instances are **Stopped** \(`Stopped`\).|Stopped|
|The invocation status of all instances are **Running** \(`Running`\), or that of some instances is `Running` \(`Running`\).|Running|
|The invocation status of some instances are **Failed** \(`Failed`\).|Partially failed|
|Instance invocation status|One-time batched execution is a one-off operation, so the instance invocation status is the same as the invocation record status.|
|Invocation record status|See the table [The status of commands executed on an instance](#).|

Take three ECS instances for example. The following figure shows the relationships between the overall invocation status and the instance invocation status during a one-time execution on multiple instances.

![](images/5246_en-US.png "Lifecycle of one-time batched execution")

|Status|Description|
|:-----|:----------|
|Overall invocation status|The overall invocation status remains **Running** \(`Running`\) unless you stop the invocation on all instances.|
|Instance invocation status|The instance invocation status remains **Running** \(`Running`\) unless you stop the invocation.|
|Invocation record status|See the table [The status of commands executed on an instance](#).|

## References {#section_jvp_5dx_ydb .section}

[Cloud Assistant client](../../../../reseller.en-US/User Guide/Cloud assistant/Cloud assistant client.md#)

**Console operations:**

-   [Create commands.](../../../../reseller.en-US/User Guide/Cloud assistant/Create commands.md#)
-   [Run commands.](../../../../reseller.en-US/User Guide/Cloud assistant/Run commands.md#)
-   [Query the invocation results and status.](../../../../reseller.en-US/User Guide/Cloud assistant/Query execution results and status.md#)
-   [Manage commands.](../../../../reseller.en-US/User Guide/Cloud assistant/Manage commands.md#)

**API operations:**

-   [CreateCommand](../../../../reseller.en-US/API Reference/Cloud assistant/CreateCommand.md#): creates commands.
-   [InvokeCommand](../../../../reseller.en-US/API Reference/Cloud assistant/InvokeCommand.md#): executes created commands on the target ECS instance.
-   [DescribeInvocations](../../../../reseller.en-US/API Reference/Cloud assistant/DescribeInvocations.md#): queries the execution status of commands.
-   [DescribeInvocationResults](../../../../reseller.en-US/API Reference/Cloud assistant/DescribeInvocationResults.md#): queries the execution results of commands, that is, the actual output information in the specified ECS instance \(`Output`\).
-   [StopInvocation](../../../../reseller.en-US/API Reference/Cloud assistant/StopInvocation.md#): stops running command processes.
-   [ModifyCommand](../../../../reseller.en-US/API Reference/Cloud assistant/ModifyCommand.md#): modifies the contents of created commands.
-   [DescribeCommands](../../../../reseller.en-US/API Reference/Cloud assistant/DescribeCommands.md#): queries created commands.
-   [DeleteCommand](../../../../reseller.en-US/API Reference/Cloud assistant/DeleteCommand.md#): deletes created commands.

