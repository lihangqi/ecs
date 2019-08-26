# Instance states {#EcsApiInstanceStauts .reference}

This topic describes the possible states of ECS instances.

|State|Description|
|:----|:----------|
|Pending|The initial state of an ECS instance when you create the ECS instance through the ECS console or by calling [RunInstances](intl.en-US/API Reference/Instances/RunInstances.md#). Instances are only in the pending state during the creation process, and this state only lasts for a few seconds. **Note:** If the instance is being created by calling [EN-US\_TP\_9857.md\#](intl.en-US/API Reference/Instances/CreateInstance.md#), you must then call [StartInstance](intl.en-US/API Reference/Instances/StartInstance.md#) to manually change the instance state from pending to starting. If the instance is being created by calling [RunInstances](intl.en-US/API Reference/Instances/RunInstances.md#), the instance automatically enters the starting state.

 |
|Starting|The transient state when an instance is enabled through the ECS console or by calling [StartInstance](intl.en-US/API Reference/Instances/StartInstance.md#).|
|Running|The stable state after an instance is enabled through the ECS console or by calling [StartInstance](intl.en-US/API Reference/Instances/StartInstance.md#). The instance owner can use, manage, and modify business and applications on an instance when the instance is in this state.|
|Stopping|The transient state when an instance is stopped through the ECS console or by calling [StopInstance](intl.en-US/API Reference/Instances/StopInstance.md#).|
|Stopped|The stable state after an instance has been stopped.|

