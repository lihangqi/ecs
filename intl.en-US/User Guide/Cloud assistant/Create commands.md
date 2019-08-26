# Create commands {#concept_pbk_v1t_q2b .concept}

You can use cloud assistance commands to perform routine tasks for ECS instances. These tasks include fast execution of automatic maintenance scripts, process polling, resetting of user password, installation and uninstallation of software, application update, and patch installation. Command types can either be Bat or PowerShell for Windows, or Shell for Linux.

## Limits {#section_r3m_zct_q2b .section}

-   Within an Alibaba Cloud region, you can create at most 100 cloud assistant commands.
-   A script cannot exceed 16 KB after Base64 encoding.

## Create commands {#CreateCommand .section}

To create a command on the ECS Console, take the following steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Cloud Assistant**.
3.  Select a region.
4.  Click **Create Command**, and in the right-side pop-up window.
    1.  Input a **Command Name**, such as HelloECS.
    2.  Input a **Command Description**, such as UserGuide.
    3.  Click the ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17007/15433858278334_en-US.png) icon, and select command type from the drop-down list. For Windows instances, you can select either **Bat** or **PowerShell**. For Linux instances, you must select **Shell**.
    4.  Modify or paste the contents of your command, such as:

        ```
        echo hello ECS!
        echo root:NewPasswd9! | chpasswd
        echo Remmember your password!
        ```

    5.  Determine the **Execution Path** of the command. The execution paths of Bat and PowerShell commands are by default set to the directory where the cloud assistant client is stored, such as `C:\ProgramData\aliyun\assist\$(version)`. Shell commands are by default in the `/root` directory.
    6.  Set the maximum timeout time \(in seconds\) for commands in an instance. The default value is set to 3600s. When a command you created cannot be run for some reason, the command times out. After the command times out, the command process will be forcibly terminated.
    7.  After confirming the command, click **Create**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17007/15433858278365_en-US.png)


You can also use the ESC API [CreateCommand](../reseller.en-US/API Reference/Cloud assistant/CreateCommand.md#) to create a cloud assistant command.

## What to do next {#section_gxh_53t_q2b .section}

[Invoke commands](reseller.en-US/User Guide/Cloud assistant/Run commands.md#)

