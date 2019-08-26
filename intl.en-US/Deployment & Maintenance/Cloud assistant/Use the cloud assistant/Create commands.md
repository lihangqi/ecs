# Create commands {#concept_pbk_v1t_q2b .task}

You can use cloud assistance commands to perform routine tasks for ECS instances such as execution of automatic maintenance scripts, process polling, user password reset, software installation and removal, application updates, and patch installations. Command types can either be Bat or PowerShell for Windows, or Shell for Linux. You can also specify variable values as custom parameters.

-   Each Alibaba Cloud region can support up to 100 cloud assistant commands. The quantity of cloud assistant commands may increase with your ECS usage.

    **Note:** You can also call [DescribeAccountAttributes](../reseller.en-US/API Reference/Others/DescribeAccountAttributes.md#), with the AttributeName.N parameter set to max-axt-command-count, to query the maximum number of cloud assistant commands that can be executed in a region.

-   A script cannot exceed 16 KB in size after being encoded in Base64.
-   A maximum of 20 custom parameters can be specified in a cloud assistant command.

This topic describes how to create commands in the ECS console. You can also call [../DNA0011860945/EN-US\_TP\_9957.md\#](../reseller.en-US/API Reference/Cloud assistant/CreateCommand.md#) to perform the operation.

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Maintenance & Monitoring** \> **Cloud Assistant**.
3.  In the top navigation bar, select a region.
4.  Click **Create Script** and configure the parameters. 
    1.  Enter a **Script Name**, such as HelloECS.
    2.  Enter a **Script Description**, such as UserGuide.
    3.  Click the ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17007/15647271758334_en-US.png) icon, and select a script type from the drop-down list.

        For Windows instances, you can select either **Bat** or **Power Shell**. For Linux instances, you must select **Shell**.

    4.  In the **Script** box, enter or paste your command.

        You must check whether the syntax, logic, or algorithm of the command is correct. Assume that you have created the /backup directory by running the `mkdir /backup` command. The following example archives a file in this directory.

        ``` {#codeblock_jsv_tfh_p8m}
        #! /bin/bash 
        OF=/backup/my-backup-$(date +%Y%m%d).tgz
        tar -cf $OF {{file}}
        ```

        **Note:** In this example, `{{file}}` is a custom parameter. When running the command, you can set its value to a file to be archived, such as /app/usrcredential. You can also set a periodic execution plan to archive key files on regular basis. For more information, see [Run a script](reseller.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Run a script.md#).

    5.  Determine whether to turn on the **Use Parameters** switch.
        -   If you turn on the **Use Parameters** switch, you can specify custom parameters in the format of \{\{key\}\} in the **Script** parameter. Custom parameters can be used in scenarios of dynamic values and multi-purpose values. For data that is security sensitive or changes with the environment, such as AccessKey pairs, instance IDs, authorization codes, time parameters, and key system files, we recommend that you specify custom parameters.
        -   When running the command, you can set the value in the **Parameters** box. For more information, see [Run a script](reseller.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Run a script.md#).
    6.  Enter a **Execution Path**.

        The default execution path of Bat and Powershell commands is the directory where the cloud assistant client is stored. Example: `C:\ProgramData\aliyun\assist\$(version)`. The execution paths of Shell commands are the `/root` directory.

    7.  Set a timeout value. The default value is 3600 seconds.

        When a command you created cannot be executed, the command times out. When a command times out, the command process is forcibly terminated.

    8.  Click **Create**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17007/15647271758365_en-US.png)


[Run a script](reseller.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Run a script.md#)

