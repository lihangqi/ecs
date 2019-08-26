# Instance status table {#EcsApiInstanceStauts .reference}

|status|Description|
|:-----|:----------|
|Pending|The default status after you create an ECS instance in the console or by using [RunInstances](intl.en-US/API Reference/Instances/RunInstances.md#). The default state of the instance after the instance has been created.|
|Starting|The transient status of an ECS instance. When you start it in the console or by using [StartInstance](intl.en-US/API Reference/Instances/StartInstance.md#).|
|Running|The normal status of an ECS instance after you successfully start it in the console or by using StartInstance, you can operate, manage, or adjust your business or application in it.|
|Stopping|The transient status of an ECS instance when you stop it in the console or by using [StopInstance](intl.en-US/API Reference/Instances/StopInstance.md#). When you stop it in the console or by using StopInstance.|
|Stopped|An ECS instance is fully stopped.|

