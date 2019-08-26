# Manage commands {#concept_hy5_y35_q2b .concept}

After creating cloud assistant commands, you can set the command name and description, clone commands, or delete unnecessary commands to guarantee a sufficient command quota.

## Modify the name and description of a command {#ModifyCommand .section}

To set the command name and description in the ECS console, perform the following steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Cloud Assistant**.
3.  Select a region.
4.  Move the mouse cursor to the command you want to edit, and click the ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9709/15433856307167_en-US.png) icon that appears in the prompted window.
    -   **Command Name**: Input the new command name.
    -   **Command Description**: Input the new command description.
5.  Click **OK**.

You can also use the ECS API [ModifyCommand](../reseller.en-US/API Reference/Cloud assistant/ModifyCommand.md#) to modify command information.

## Clone a command {#CopyCommands .section}

The clone command is equivalent to add a new version for an existing cloud assistant command. You can retain all the information of the cloned command as it was previously. Alternatively, you can set a new name, description, type, content, execution path, or timeout time for it. To clone a command in the ECS console, perform the following steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Cloud Assistant**.
3.  Select a region.
4.  Find the cloud assistant command you want to clone, and from the **Operation** list, click **Clone**.
5.  In the Clone Command dialogue box, complete the following optional steps:
    1.  Enter a new **Command Name**, such as HelloECS.
    2.  Enter a new **Command Description**, such as UserGuide.
    3.  Click the icon ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17007/15433856308334_en-US.png) to replace the command type from the drop-down list. For Windows instances, you can select **Bat** or **Power Shell**. For Linux instances, you can select **Shell**.
    4.  Edit or paste new command content.
    5.  Determine a new command **Execution Path**. The default execution path for Bat or PowerShell commands is the directory where the cloud assistant client is installed, such as `C:\ProgramData\aliyun\assist\$(version)`. The default execution path for Shell commands is the `/root` directory.
    6.  Configure the timeout time in seconds for the command. The default value is set to 3600. When a command you created cannot be executed for the amount of time set by this parameter, the command times out. When the timeout time of the command expires, the command process will be forcibly terminated.
    7.  After you confirm the modification, click **Create**.

## Delete commands {#DeleteCommand .section}

Within an Alibaba Cloud region, you can create a maximum of 100 cloud assistant commands. We suggest that you regularly clean your commands to guarantee a sufficient command quota. To delete a command on the ECS console, perform the following steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Cloud Assistant**.
3.  Select a region.
4.  Locate the cloud assistant command you want to delete:
    -   To delete a single command, from the **Operation** list, select **Delete**.
    -   To delete multiple commands, select the target instances, and click **Delete Command**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17035/15433856308634_en-US.png)

5.  In the Delete Command dialogue box, click **OK**.

You can also use the ECS API [DeleteCommand](../reseller.en-US/API Reference/Cloud assistant/DeleteCommand.md#) to delete commands.

