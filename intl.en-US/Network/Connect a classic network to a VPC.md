# Connect a classic network to a VPC {#concept_rww_lcx_wgb .concept}

This topic describes how to connect a classic network to a VPC. You can set up a ClassicLink connection so that ECS instances of the classic network type can access cloud resources in a VPC network through the intranet.

## Prerequisites {#section_k5c_pjs_ngb .section}

Make sure that you are aware of the limitations of ClassicLink. For more information, see [ClassicLink overview](../../../../reseller.en-US/User Guide/Network connection/ClassicLink/ClassicLink overview.md#).

## Procedure {#section_fgy_qjs_ngb .section}

1.  Log on to the [VPC console](https://partners-intl.console.aliyun.com/#/vpc).
2.  Select the region of the target VPC, and click the ID of the target VPC.
3.  On the VPC Details page, click **Enable ClassicLink**. In the displayed dialog box, click **OK**.
4.  Log on to the [ECS console](https://partners-intl.aliyun.com/login-required#/ecs).
5.  In the left-side navigation pane, click **Instances**.
6.  Choose **More** \> **Network and Security Group** \> **Connect to VPC**.
7.  In the displayed dialog box, select the target VPC and click **OK**. Then click the security group configuration link.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/130424/155721377545018_en-US.png)

8.  Click **Add ClassicLink Rules** and configure the security rule according to the following information. Then, click **OK**.

    |Configuration|Description|
    |:------------|:----------|
    |**Classic Security Group**|Display the classic network security group.|
    |**Select VPC Security Group**|Select a security group to use. Up to five security groups can be selected.|
    |**Mode**|Select one of the following modes:     -   Classic <=\> VPC: The connected resources can access each other \(recommended\).
    -   Classic =\> VPC: Authorize the classic ECS instance to access cloud resources in the connected VPC.
    -   VPC =\> Classic: Authorize the cloud resources in the connected VPC to access the classic ECS instance.
 |
    |**Protocol Type and Port Range**|Select the protocol and port used for the communication. The port must be in the form of xx/xx. For example, if port 80 is used, enter 80/80.|
    |**Priority**|Set the priority for the rule. A smaller number represents a higher priority, for example, 1.|
    |**Description**|Enter a description for the security rule.|

9.  Return to the [ECS console](https://partners-intl.aliyun.com/login-required#/ecs). On the **Instance List** page, click the Column Filter icon on the upper-right corner, and then select the **Connection Status** check box. Then, click **OK**.

    If **Connection Status** is **Connected**, ECS instances of the classic network are connected to the VPC network.


