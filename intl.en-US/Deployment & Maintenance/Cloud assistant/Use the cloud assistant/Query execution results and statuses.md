# Query execution results and statuses {#concept_jf4_btt_q2b .concept}

We recommend that you review the results and status of a command execution after running a command to ensure the target operation has completed properly. Note that there is no difference between running a cloud assistant command on the console and running a command while logged on to the instance.

## Prerequisites {#section_nmt_qyt_q2b .section}

The command has been run at least once.

## View command execution results {#ViewCommandResult .section}

To view command execution results in the ECS console, follow these steps:

1.  On the **Tasks** tab page, find the execution record of the target command and click **View Results** in the **Actions** column.
2.  In the displayed window, select an execution record and click ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17026/15662010518508_en-US.png) to unfold the command execution record.

You can also call the [DescribeInvocationResults](../intl.en-US/API Reference/Cloud assistant/DescribeInvocationResults.md#) API action to view command results.

## View command execution status {#ViewCommandStatus .section}

To view the execution status of a command in the ECS console, follow these steps:

1.  On the **Tasks** tab page, find the execution record of the target command, and view the status of the command execution in the **Status** column.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/17026/15662010518525_en-US.png)


You can also call the [DescribeInvocations](../intl.en-US/API Reference/Cloud assistant/DescribeInvocations.md#) API action to view command execution status.

