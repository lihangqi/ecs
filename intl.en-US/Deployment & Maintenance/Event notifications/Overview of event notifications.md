# Overview of event notifications {#concept_189641 .concept}

This topic provides an overview of notifications for Elastic Compute Service \(ECS\) system events such as instance system events, block storage system events, preemptible instance interruption events, and snapshot creation result events.

**Note:** The event notifications shown in this topic are for reference only.

## Background information {#section_xml_lm9_cwp .section}

After you set notifications for ECS system events, you can receive the corresponding notifications if these system events occur. For more information, see [Set event notifications](reseller.en-US/Deployment & Maintenance/Event notifications/Set event notifications.md#) and [System events](reseller.en-US/Deployment & Maintenance/System events/System events.md#). The `name` field in a notification indicates the code name of the event. This field is in the following format: `<resource type>:<event type>:<status>`.

-   `<resource type>`: the name of the corresponding ECS resource. Valid values: Instance | Disk.
    -   Instance: your ECS instance.
    -   Disk: your block storage device.
-   `<event type>`: the name of the event. Example values: SystemMaintenance.Reboot | StateChange | Instance:PreemptibleInstanceInterruption | CreateSnapshotCompleted.
-   `<status>`: the status of the event. For information about valid values, see [System events](reseller.en-US/Deployment & Maintenance/System events/System events.md#).

    **Note:** The `<status>` attribute is available only for instance and block storage system events.


## Instance system events {#section_s29_sj0_xx5 .section}

After an instance system event occurs, CloudMonitor sends an initial notification of the event, and sends subsequent event notifications if the event status changes. The following is an example of the notifications for a `SystemMaintenance.Reboot` event:

-   The first notification that CloudMonitor sends to you indicates that the event is in the `Scheduled` state:

    ``` {#codeblock_bhg_ozl_n5i}
    {
      "ver": "1.0",
      "id": "2256A988-0B26-4E2B-820A-8A********E5",
      "product": "ECS",
      "resourceId": "acs:ecs:cn-hangzhou:169070********30:instance/i-bp1ecr********5go2go",
      "level": "CRITICAL",
      "name": "Instance:SystemMaintenance.Reboot:Scheduled",
      "userId": "169070********30",
      "eventTime": "20190409T121826.922+0800",
      "regionId": "cn-hangzhou",
      "content": {
        "eventId": "e-bp11trd********pqum2",
        "publishTime": "2019-04-09T04:18:26Z",    
        "notBefore": "2019-04-12T01:01:01Z",      
        "instanceId": "i-bp1ecr********5go2go",   
        "eventType": "SystemMaintenance.Reboot",  
        "eventStatus": "Scheduled"                
      }
    }
    ```

-   If you restart your ECS instance before the time specified by the `notBefore` attribute, this event is avoided. In this case, CloudMonitor sends the following notification to indicate that the event status is changed to `Avoided`:

    ``` {#codeblock_fzi_59q_yrh}
    {
      "ver": "1.0",
      "id": "2256A988-0B26-4E2B-820A-8A********E5",
      "product": "ECS",
      "resourceId": "acs:ecs:cn-hangzhou:169070********30:instance/i-bp1ecr********5go2go",
      "level": "CRITICAL",
      "name": "Instance:SystemMaintenance.Reboot:Scheduled",
      "userId": "169070********30",
      "eventTime": "20190410T160101.922+0800",
      "regionId": "cn-hangzhou",
      "content": {
        "eventId": "e-bp11trdr********qum2",
        "publishTime": "2019-04-09T04:18:26Z",
        "notBefore": "2019-04-12T01:01:01Z",
        "instanceId": "i-bp1ecr********5go2go",
        "eventType": "SystemMaintenance.Reboot",
        "eventStatus": "Avoided",
        "executeStartTime": "2019-04-10T08:01:01Z",  
        "executeFinishTime": "2019-04-10T08:01:01Z"  
      }
    }
    ```


The attributes in the `content` field are described as follows:

-   `eventId`: the ID of the event.
-   `publishTime`: the time when the event was published.
-   `notBefore`: the time when the event was scheduled to execute. This attribute is available only for system maintenance events.
-   `instanceId`: the ID of your ECS instance.
-   `eventType`: the type of the event. For information about valid values, see [System events](reseller.en-US/Deployment & Maintenance/System events/System events.md#).
-   `eventStatus`: the status of the event. For information about valid values, see [System events](reseller.en-US/Deployment & Maintenance/System events/System events.md#).
-   `executeStartTime`: the time when the event started. The valid time format is UTC+0.
-   `executeFinishTime`: the time when the event ended. The valid time format is UTC+0.

    **Note:** The executeStartTime and executeFinishTime attributes are available only for events in the `Executing`, `Executed`, `Canceled`, or `Avoided` state. You can obtain the time when an event was canceled or avoided from its `Canceled` or `Avoided` attribute.


## Block storage system events {#section_g53_g9w_6ev .section}

Block storage system events are caused only by faults. CloudMonitor sends two notifications: one at the start time of the event and one at the end time. The following are notifications for a `Stalled` event:

-   The initial notification that CloudMonitor sends to you contains the executeStartTime attribute:

    ``` {#codeblock_vxc_3pi_bk0}
    {
      "ver": "1.0",
      "id": "2256A988-0B26-4E2B-820A-8A********E5",
      "product": "ECS",
      "resourceId": "acs:ecs:cn-hangzhou:169070********30:disk/d-t4ndyqve********n4ds",
      "level": "CRITICAL",
      "name": "Disk:Stalled:Executing",
      "userId": "169070********30",
      "eventTime": "20190410T080101.922+0800",
      "regionId": "cn-hangzhou",
      "content": {
        "eventId": "e-t4navn7********6x5no",
        "diskId": "d-t4ndyqve********n4ds",
        "device": "/dev/xvdb",
        "eventType": "Stalled",
        "executeStartTime": "2019-04-10T01:01:01Z",
        "ecsInstanceId": "i-bp1ecr********5go2go",
        "ecsInstanceName": "ecs-instance-name"
      }
    }
    ```

-   The notification that CloudMonitor sends to you when the event ends contains the executeFinishTime attribute:

    **Note:** The executeFinishTime attribute is not included in the initial notification.

    ``` {#codeblock_sd4_cmh_a1u}
    {
      "ver": "1.0",
      "id": "2256A988-0B26-4E2B-820A-8A********E5",
      "product": "ECS",
      "resourceId": "acs:ecs:cn-hangzhou:169070********30:disk/d-t4ndyqve********n4ds",
      "level": "CRITICAL",
      "name": "Disk:Stalled:Executing",
      "userId": "169070********30",
      "eventTime": "20190410T080301.922+0800",
      "regionId": "cn-hangzhou",
      "content": {
        "eventId": "e-t4navn7********6x5no",   
        "diskId": "d-t4ndyqve********n4ds",    
        "device": "/dev/xvdb",                 
        "eventType": "Stalled",                
        "executeStartTime": "2019-04-10T01:01:01Z",   
        "executeFinishTime": "2019-04-10T01:03:01Z",  
        "ecsInstanceId": "i-bp1ecr********5go2go",    
        "ecsInstanceName": "ecs-instance-name"        
      }
    }
    ```


The attributes in the `content` field are described as follows:

-   `eventId`: the ID of the event.
-   `diskId`: the ID of the corresponding block storage device.
-   `device`: the mount point of the corresponding block storage device.
-   `eventType`: the type of the event. Valid values: Degraded | SeverelyDegraded | Stalled.
    -   Degraded: Indicates that the block storage performance is degraded.
    -   SeverelyDegraded: Indicates that the block storage performance is severely degraded.
    -   Stalled: Indicates that the block storage performance is stalled.
-   `executeStartTime`: the time when the event started. The valid time format is UTC+0.
-   `executeFinishTime`: the time when the event ended. The valid time format is UTC+0.
-   `ecsInstanceId`: the ID of the ECS instance to which the corresponding block storage device is mounted.
-   `ecsInstanceName`: the name of the ECS instance to which the corresponding block storage device is mounted.

## Instance status change events {#section_ukc_k1o_dsy .section}

When the status of your ECS instance changes, CloudMonitor sends you a notification. For more information, see [ECS instance life cycle](../../../../reseller.en-US/Instances/ECS instance life cycle.md#).

For example, CloudMonitor sends you the following notification when its status changes to `Running`:

``` {#codeblock_lf4_ls3_a5e}
{
  "ver": "1.0",
  "id": "2256A988-0B26-4E2B-820A-8A********E5",
  "product": "ECS",
  "resourceId": "acs:ecs:cn-hangzhou:169070********30:instance/i-bp1ecr********5go2go",
  "level": "INFO",
  "name": "Instance:StateChange",
  "userId": "169070********30",
  "eventTime": "20190409T121826.922+0800",
  "regionId": "cn-hangzhou",
  "content": {
    "resourceId": "i-bp1ecr********5go2go",  
    "resourceType": "ALIYUN::ECS::Instance", 
    "state": "Running"                       
  }
}
```

The attributes in the `content` field are described as follows:

-   `resourceId`: the ID of your ECS instance.
-   `resourceType`: the type of the corresponding resource. Valid value: ALIYUN::ECS::Instance.
-   `state`: the status of your ECS instance. Valid values: Pending | Starting | Running | Stopping | Stopped | Deleted.

## Preemptible instance interruption events {#section_5ge_o92_e74 .section}

Preemptible ECS instances may be released if the corresponding market prices or resource stock changes. Five minutes before a preemptible ECS instance is released, CloudMonitor sends you a notification. For more information, see [Preemptible instances](../../../../reseller.en-US/Instances/Instance purchasing options/Preemptible instances/Preemptible instances.md#).

Example:

``` {#codeblock_ax7_7pr_vrn}
{
  "ver": "1.0",
  "id": "2256A988-0B26-4E2B-820A-8A********E5",
  "product": "ECS",
  "resourceId": "acs:ecs:cn-hangzhou:169070********30:instance/i-bp1ecr********5go2go",
  "level": "INFO",
  "name": "Instance:PreemptibleInstanceInterruption",
  "userId": "169070********30",
  "eventTime": "20190409T121826.922+0800",
  "regionId": "cn-hangzhou",
  "content": {
    "instanceId": "i-bp1ecr********5go2go",  
    "action": "delete"                       
  }
}
```

The attributes in the `content` field are described as follows:

-   `instanceId`: the ID of the preemptible ECS instance.
-   `action`: the action on the preemptible ECS instance. Valid value: delete.

## Snapshot creation result events {#section_1aj_iz6_r0k .section}

After a snapshot is created for a disk, CloudMonitor sends you a notification to indicate whether the snapshot is created.

Example:

``` {#codeblock_tnt_9a3_azr}
{
  "ver": "1.0",
  "id": "2256A988-0B26-4E2B-820A-8A********E5",
  "product": "ECS",
  "resourceId": "acs:ecs:cn-hangzhou:169070********30:snapshot/s-bp1fis********b859b3",
  "level": "INFO",
  "name": "Snapshot:CreateSnapshotCompleted",
  "userId": "169070********30",
  "eventTime": "20190409T121826.922+0800",
  "regionId": "cn-hangzhou",
  "content": {
    "result": "accomplished",
    "snapshotId": "s-bp1fis********b859b3",
    "snapshotName": "test-snapshot",   
    "diskId": "d-bp1bwa********9ol4mi",      
    "startTime": "2019-04-22T08:36:09Z",     
    "endTime": "2019-04-22T08:37:11Z"        
  }
}
```

The attributes in the `content` field are described as follows:

-   `result`: the result of the snapshot creation task. Valid values: accomplished | failed.
-   `snapshotId`: the ID of the snapshot.
-   `snapshotName`: the name of the snapshot.
-   `diskId`: the ID of the disk.
-   `startTime`: the time when the creation of the snapshot started. The valid time format is UTC+0.
-   `endTime`: the time when the creation of the snapshot ended. The valid time format is UTC+0.

**Note:** If a snapshot is created automatically, CloudMonitor does not send a notification. In this case, you can log on to the ECS console or call the [DescibeSnapshots](../../../../reseller.en-US/API Reference/Snapshots/DescribeSnapshots.md#) API action to check whether the snapshot is created. For information about snapshot types, see [Snapshot overview](../../../../reseller.en-US/Snapshots/Snapshot overview.md#).

