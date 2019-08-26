# Cloud assistant overview {#concept_qg3_5dx_ydb .concept}

The cloud assistant allows you to manage your ECS instances in a safe and secure manner. Specifically, the cloud assistant allows you to automatically execute one or more daily maintenance commands, run automated O&M scripts, poll the processes, install or uninstall software, update applications, install patches, and more.

## Application scenarios {#section_0nd_kcu_s9x .section}

The cloud assistant helps you perform deployment and operation tasks on an ECS instance, including but not limited to:

-   Run automated O&M scripts.
-   Run existing scripts on an instance.
-   Manage software lifecycles.
-   Deploy code or applications.
-   Poll processes.
-   Install patches.
-   Obtain updates from OSS or yum sources.
-   Modify the host name or login password.

## Billing method {#section_v5p_5dx_ydb .section}

The cloud assistant is provided free of charge. However, the running of your ECS instances will incur fees. For more information, see [Pricing overview](../../../../reseller.en-US/Pricing/Pricing overview.md#).

## Details {#section_zfz_wdx_ydb .section}

By installing the cloud assistant client on ECS instances, you can run BAT or PowerShell scripts \(for Windows instances\) or Shell scripts \(for Linux instances\) on one or more running \(`Running`\) ECS instances through the ECS console or by calling the relevant API. The selected instances do not impact each other. You can also set Timed Invocation to keep an ECS instance in a specific status, obtain its monitoring and log information, or run a daemon process. The cloud assistant does not initiate any operations. That is, only a user can execute specific operations as required.

The following table describes relevant concepts of the cloud assistant.

|Common name|Description|
|:----------|:----------|
|Cloud assistant|A convenient tool provided by Alibaba Cloud ECS for automated batch invocation of daily maintenance tasks on an ECS instance or [ECS Bare Metal Instance \(X-Dragon\)](../../../../reseller.en-US/Instances/Instance type families/ECS bare metal instance type family/EBM Instance overview.md#). The cloud assistant service is available in all Alibaba Cloud regions.|
|Cloud assistant client|A client program that is installed on an ECS instance to run all the commands for the instance. The task process name is `AliyunService` for a Windows instance and `aliyun.service` for a Linux instance.|
|Command|Specific commands to be invoked on an ECS instance, such as a Shell script or a PowerShell script.|
|Custom parameter|The variable you set in a command, which is expressed as \{\{key\}\}. You can set the value of a custom parameter as \{\{"key":"value"\}\} when you invoke a command. There is an upper limit on the number of cloud assistant commands you can invoke in each Alibaba Cloud region. Configuring custom parameters increases the flexibility and applicability of cloud assistant commands.|
|One-time invocation|One-time invocation occurs when you invoke a command on one or more instances \(`Invocation`\).|
|Periodical invocation|You can specify a period of time to run a command periodically on one or more instances.|
|Invocation status|The command invocation status. For more information, see [Lifecycle of command execution](#).|

## Limits {#section_n5p_5dx_ydb .section}

-   You must install and manage the cloud assistant as the administrator. Specifically, the Linux instance administrator is `root` and the Windows instance administrator is `administrator`.
-   In each Alibaba Cloud region, you can have up to 100 cloud assistant commands.
-   In each Alibaba Cloud region, you can run up to 5000 cloud assistant commands per day.
-   For Timed Invocation commands, the `Timed` interval cannot be less than 10 seconds.
-   The size of a Base64-encoded BAT, PowerShell, or Shell script together with custom parameters, cannot be greater than 16 KB.
-   A single command can contain a maximum of 20 custom parameters.
-   The target ECS instance must be in a **Running** \(`Running`\) status.
-   Currently, the cloud assistant is supported by the following operating systems only: Windows Server 2008/2012/2016, Ubuntu 12/14/16, CentOS 5/6/7, Debian 7/8/9, RedHat 5/6/7, SUSE Linux Enterprise Server 11/12, OpenSUSE, Aliyun Linux, and CoreOS.

## How to use the cloud assistant {#section_ivp_5dx_ydb .section}

You must install the [cloud assistant client](../../../../reseller.en-US/Deployment & Maintenance/Cloud assistant/Configure the cloud assistant client.md#) on your ECS instance before using the cloud assistant.

You can use it through APIs. For more information, see [Automatically manage instances](../../../../reseller.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant for automatic O&M.md#).

## Lifecycle of command invocation {#InvocationStatus .section}

A command may have the following status when running on an instance.

|Command status|API status|Description|
|:-------------|:---------|:----------|
|Being executed|`Running`|The command is being executed.|
|Stopped|`Stopped`|A command was stopped during its invocation.|
|Execution finished|`Finished`|The command invocation is finished. However, this does not indicate the invocation is successful. You can check whether the invocation is successful by checking the actual output \(`Output`\) of the command process.|
|Execution failed|`Failed`|The command invocation did not finish when the timeout time \(`Timeout`\) was reached.|

To facilitate the management of bulk or periodical execution, you can manage the lifecycle of command execution from the perspectives of **overall invocation status**, **instance invocation status**, and **invocation record status**. The relationships among various levels are shown in the following figure.

![](images/5245_en-US.png "Relationships among the invocation status")

|Status|Command invocation|Displayed status|
|:-----|:-----------------|:---------------|
|Overall invocation status|The invocation status of all instances is **Finished** \(`Finished`\).|Finished|
| The invocation status of some instances is **Finished** \(`Finished`\),

 while the status of other instances is **Stopped** \(`Stopped`\).

 |
|The invocation status of all instances is **Failed** \(`Failed`\).|Failed|
|The invocation status of all instances is **Stopped** \(`Stopped`\).|Stopped|
|The invocation status of all instances is **Running** \(`Running`\), or that of some instances is `Running` \(`Running`\).|Running|
|The invocation status of some instances is **Failed** \(`Failed`\).|Partially failed|
|Instance invocation status|One-time batched execution is a one-off operation and the instance invocation status is the same as the invocation record status.|
|Invocation record status|See the table [Status of commands executed on an instance](reseller.en-US/Deployment & Maintenance/Cloud assistant/Cloud assistant overview.md#).|

Take three ECS instances for example. The following figure shows the relationships between the overall invocation status and the instance invocation status during a one-time execution on multiple instances.

![](images/5246_en-US.png "Lifecycle of one-time batched execution")

|Status|Description|
|:-----|:----------|
|Overall invocation status|The overall invocation status remains **Running** \(`Running`\) unless you stop the invocation on all instances.|
|Instance invocation status|The instance invocation status remains **Running** \(`Running`\) unless you stop the invocation.|
|Invocation record status|See the table [Status of commands executed on an instance](reseller.en-US/Deployment & Maintenance/Cloud assistant/Cloud assistant overview.md#).|

## References {#section_jvp_5dx_ydb .section}

[Cloud assistant client](../../../../reseller.en-US/Deployment & Maintenance/Cloud assistant/Configure the cloud assistant client.md#)

**Operations on the ECS console:** 

-   [Create commands](../../../../reseller.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Create a script.md#)
-   [Run commands](../../../../reseller.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Run a script.md#)
-   [Query the invocation results and status](../../../../reseller.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Query execution results and statuses.md#)
-   [Manage commands](../../../../reseller.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Manage commands.md#)

**API actions:**

-   [CreateCommand](../../../../reseller.en-US/API Reference/Cloud assistant/CreateCommand.md#)
-   [InvokeCommand](../../../../reseller.en-US/API Reference/Cloud assistant/InvokeCommand.md#)
-   [DescribeInvocations](../../../../reseller.en-US/API Reference/Cloud assistant/DescribeInvocations.md#)
-   [DescribeInvocationResults](../../../../reseller.en-US/API Reference/Cloud assistant/DescribeInvocationResults.md#)
-   [StopInvocation](../../../../reseller.en-US/API Reference/Cloud assistant/StopInvocation.md#)
-   [DescribeCommands](../../../../reseller.en-US/API Reference/Cloud assistant/DescribeCommands.md#)
-   [DeleteCommand](../../../../reseller.en-US/API Reference/Cloud assistant/DeleteCommand.md#)

