# Run commands {#concept_e5q_x3t_q2b .concept}

After creating a cloud assistant command, you can run the command on one or more instances. The command execution status and results for each instance are not influenced by the same command being run on other instances. You can also configure the execution interval for the command.

## Limits {#section_d5h_mkt_q2b .section}

-   In one Alibaba Cloud region, you can run a maximum of 500 cloud assistant commands in a single day.
-   You can run a command on a maximum of 50 instances at once.
-   The status of the target instance must be **Running**.
-   The target instance must have [cloud assistant client](../reseller.en-US/User Guide/Cloud assistant/Cloud Assistant Client.md#) installed.
-   The target instance must be [VPC-Connected](../../../../../reseller.en-US/Product Introduction/What is VPC?.md#).
-   The period for running cloud assistant commands cannot be less than 10 seconds.
-   The scheduled time for periodic command execution is set to China Standard Time \(UTC +08:00\) based on the system time obtained from the ECS instances. Make sure that the time or time zone of your ECS instance is consistent with your own expectations.

## Run commands {#InvokeCommand .section}

To execute a command on the ECS console, take the following steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Cloud Assistant**.
3.  Select a region.
4.  Search for the Cloud Assistant command you want to run. Select **Execute** from the **Operation** column. In the pop-up window:
    1.  Click **View command content** to confirm the command contents.
    2.  Click **Select Instance**. In the pop-up window:
        1.  Select one or more instances.
        2.  Click ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17010/15433866078440_en-US.png) to select an instance.

            **Note:** Bat or PowerShell commands can only be selected for Windows instances, and Shell commands can only be selected for Linux instances. All instances must have the Cloud Assistant Client **installed**. Otherwise, the instance cannot be selected even after you click the ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17010/15433866078440_en-US.png) icon.

        3.  Click **OK**.
    3.  Select **Immediate Execution** or **Scheduled Execution**:

        -   **Immediate Execution**: The cloud assistant will run the command immediately on the instances once.
        -   **Scheduled Execution**: Use the cron expression to run the command periodically. Fill in the **Execution Time**. For more information, see [Cron expression value description](https://partners-intl.aliyun.com/help/faq-detail/64769.htm).
        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17010/15433866078439_en-US.png)

5.  Click **Execute**.

You can also use the ECS API [InvokeCommand](../reseller.en-US/API Reference/Cloud assistant/InvokeCommand.md#) to execute a cloud assistant command.

## Stop command execution {#StopCommand .section}

**Prerequisite**: Either it must be a periodic command, or the command must have a command execution status of **Running**.

To stop a command on the management console, take the following steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Cloud Assistant**.
3.  Select a region.
4.  In the **Execution Record** area, search for the command you need to stop, and select **Stop Command** from the **Operation** column.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17010/15433866088527_en-US.png)


## What to do next {#section_crb_4st_q2b .section}

[Query execution results and status](reseller.en-US/User Guide/Cloud assistant/Query execution results and status.md#).

