# Run commands {#concept_e5q_x3t_q2b .concept}

You can run a cloud assistant command on one or more instances. The command execution status and corresponding results for cloud assistant commands run on each instance do not impact the execution results of other instances. You can also configure an execution interval for each cloud assistant command as required.

## Limits {#section_d5h_mkt_q2b .section}

-   You can run a maximum of 500 cloud assistant commands in each Alibaba Cloud region per day.
-   You can run a command on a maximum of 50 instances at a time.
-   The status of the target instance or instances must be **Running**.
-   The target instance or instances must have [cloud assistant client](../reseller.en-US/Deployment & Maintenance/Cloud assistant/Cloud assistant client.md#) installed.
-   The target instance or instances network type must be [VPC-Connected](../../../../../../reseller.en-US/Product Introduction/What is VPC?.md#).
-   The period for running cloud assistant commands cannot be less than 10 seconds.
-   The scheduled time for periodic command execution is set to China Standard Time \(UTC +08:00\) based on the system time obtained from the ECS instances. Make sure that the time or time zone of your ECS instance is consistent with your requirements.

## Run commands {#InvokeCommand .section}

To run a cloud assistant command on the ECS console, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Cloud Assistant**.
3.  Select the target region.
4.  Search for the Cloud Assistant command you want to run, and then select **Execute** from the **Operation** column. In the pop-up window that is displayed, configure the following parameters:
    1.  Click **View command content** to confirm the command contents.
    2.  Click **Select Instance** and perform the following actions:
        1.  Select one or more instances.
        2.  Click ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17010/15530531768440_en-US.png) to add the selected instance or instances.

            **Note:** For Windows instances, you can select Bat or PowerShell commands. For Linux instances, you can only select Shell commands. All instances must have the cloud assistant client **installed**. Otherwise, it cannot be selected.

        3.  Click **OK**.
    3.  Select **Immediate Execution** or **Scheduled Execution**:

        -   **Immediate Execution**: The cloud assistant will run the command immediately on the instances once.
        -   **Scheduled Execution**: The cron expression will be used to run the command periodically. Enter the required **Execution Time**. For more information, see [Cron expression value description](https://partners-intl.aliyun.com/help/faq-detail/64769.htm).
        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17010/15530531768439_en-US.png)

5.  Click **Execute**.

You can also use the ECS API [InvokeCommand](../reseller.en-US/API Reference/Cloud assistant/InvokeCommand.md#) to execute a cloud assistant command.

## Stop command execution {#StopCommand .section}

**Prerequisite**: The command must be a periodic command, or the command must be in **Running** status.

To stop a command on the ECS console, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Cloud Assistant**.
3.  Select the target region.
4.  In the **Execution Record** area, search for the command you want to stop, and select **Stop Command** from the **Operation** column.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17010/15530531768527_en-US.png)


## What to do next {#section_crb_4st_q2b .section}

[Query execution results and status](reseller.en-US/Deployment & Maintenance/Cloud assistant/Use the cloud assistant/Query execution results and statuses.md#).

