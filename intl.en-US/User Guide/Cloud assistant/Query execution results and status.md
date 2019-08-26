# Query execution results and status {#concept_jf4_btt_q2b .concept}

There is no difference between running a cloud assistant command on the console and running a command while logged into the instance. In both cases, a command can be run successfully only after all of the command's conditions are satisfied. Cloud assistant commands executed at the same time can provide different command execution results and statuses if the following errors occur: lack of relevant dependencies, network disruptions, command semantic errors, script debugging errors, or abnormal instance statuses. We recommend that you review the command execution results and status after running a command to ensure the target operation has completed properly.

## Prerequisite {#section_nmt_qyt_q2b .section}

The command must be run at least once.

## Check the results of the command execution {#ViewCommandResult .section}

To view command execution result on the ECS Console, you must take the following steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Cloud Assistant**.
3.  Select a region.
4.  In the **Execution Record** area, search for the execution record of the necessary command execution, and select **View Results** from the **Operation** column.
5.  In the pop-up window, select an execution record and click ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17026/15433875498508_en-US.png) to expand the command execution record.

You can also use the ECS API [DescribeInvocationResults](../reseller.en-US/API Reference/Cloud assistant/DescribeInvocationResults.md#) to view command results.

## View command execution status {#ViewCommandStatus .section}

To view command execution status in the ECS Console, you must take the following steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Cloud Assistant**.
3.  Select a region.
4.  In the **Execution Record** area, search for the execution record of the necessary command execution, and then in the **Execution Status** bar view the command execution status.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17026/15433875498525_en-US.png)


You can also use the ECS API [DescribeInvocations](../reseller.en-US/API Reference/Cloud assistant/DescribeInvocations.md#) to view command execution status.

## Invocation status {#section_fdv_rzt_q2b .section}

-   Specifically, the invocation status of a command consists of `Running`, `Stopped`, `Finished`, and `Failed`.

-   Generally, the invocation status of a command includes **overall invocation status** , **instance invocation status** , and **invocation-record status**. The relationships among various levels are shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9581/15433875495245_en-US.png)


**For one-time invocations**

-   **Overall invocation status**:
    -   When the invocation status of all instances are `Finished`, the overall invocation status is displayed as `Finished`.
    -   When the invocation status of some instances are `Finished` and those of some others are `Stopped`, the overall invocation status is displayed as. `Finished`
    -   When the invocation status of all instances are `Failed`, the overall invocation status is displayed as `Failed`.
    -   When the invocation status of all instances are `Stopped`, the overall invocation status is displayed as `Stopped`.
    -   When the invocation statuses of all or some instances are `Running`, the overall invocation status is displayed as `Running`.
    -   When the invocation statuses of some instances are `Failed`, the overall invocation status is displayed as `PartialFailed`.

        Take three ECS instances as an example. The following picture shows the relationships between the overall invocation status and the instance invocation status during a one-time invocation on multiple instances.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9581/15433875495246_en-US.png)

-   **Instance invocation status**: The command is invoked only once in a one-time invocation, so the instance invocation status and the invocation-record status are identical.
-   **Invocation-record status**:
    -   `Running`: Indicates that the command is being executed.
    -   `Stopped`: Indicates that the command invocation has been manually stopped by the user.
    -   `Finished`: Indicates that the command invocation has been completed smoothly. But invocation completion does not indicate invocation success. You can confirm whether the invocation is successful based on the actual `Output`of the command process.
    -   `Failed`: Indicates that the command process has timed out \(`Timeout`\) and failed.

**For periodical invocations**

-   **Overall invocation status**: The overall invocation status is always `Running` unless you stop all the scheduled invocation for all instances.
-   **Instance invocation status**: The instance invocation status is always `Running` unless you stop the current invocation.
-   **Invocation-record status**:
    -   `Running`: The command is being executed.
    -   `Stopped`: You have stopped the command invocation.
    -   `Finished`: The command invocation is complete. However, invocation completion does not guarantee invocation success. You can confirm whether the invocation is successful or not based on the actual `Output` of the command process.
    -   `Failed`: The command process is timed out \(`Timeout`\) and fails.

