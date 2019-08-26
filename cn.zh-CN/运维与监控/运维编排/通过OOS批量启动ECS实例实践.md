# 通过OOS批量启动ECS实例实践 {#concept_l2l_jgn_xdb .task}

本文演示了如何在ECS管理控制台上，使用运维编排服务OOS的公共模板ACS-ECS-StartInstancesByTag实现批量启动多台ECS实例。

创建运维编排服务OOS运维任务前，请确保已满足以下要求：

-   您已经开通了运维编排服务OOS。详细步骤请参见[开通服务](https://help.aliyun.com/document_detail/123459.htm)。
-   您已经创建RAM角色，并为OOS服务角色添加AliyunECSFullAccess授权策略。本示例创建的RAM角色为OOSServiceRole-EcsDocGuideTest。详细步骤请参见[为OOS服务设置RAM权限](https://help.aliyun.com/document_detail/120810.htm)。
-   您已经为目标ECS实例绑定了标签，本示例创建的标签键值对为`KeyNode:LimitedAccess`。详细步骤请参见[绑定标签](../cn.zh-CN/标签与资源/标签/绑定标签.md#)。

运维编排服务OOS通过模板定义您需要编排的运维任务。模板内容支持YAML和JSON两种格式，模版分为公共模版和自定义模版两种类型。为了方便您快速使用OOS，OOS提供了公共模板供您直接使用和参考，如本文中的**ACS-ECS-StartInstancesByTag**公共模板。在使用模板前您需要仔细审查模板所要执行的运维任务，并优先在测试环境观察使用效果。

您也可以编写自定义模板来编写您所需要的运维任务。更多详情，请参见[模板结构](https://help.aliyun.com/document_detail/120665.htm)。

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。
2.  在左侧导航栏，选择**运维与监控** \> **运维编排**。
3.  在顶部状态栏处，选择地域。
4.  在**公共模板**中，选择**ACS-ECS-StartInstancesByTag**，并单击**创建执行**。 

    ![ACS-ECS-StartInstancesByTag](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/947877/156523235751707_zh-CN.png)

5.  在**基本信息**设置页面，自定义完成以下选项后单击**下一步：设置参数**。 

    -   **执行模式**：本示例选择**自动执行**，表示模板中的所有任务都会被自行执行，而不是单个拆分地执行。
    -   **风险确认模式**：本示例选择**客户了解风险，无需确认**。您也可以选择**高风险操作需要二次确认**，表示当模版执行到风险任务时会等待您二次确认后再继续执行。
    -   **模板类型**：本示例选择**公共模板**，并使用**ACS-ECS-StartInstancesByTag**模板，表示根据标签筛选实例后，OOS通过调用ECS API[StartInstance](../cn.zh-CN/API参考/实例/StartInstance.md#)批量启动ECS实例。当实例处于非**已停止**（Stopped）状态时，会报错。
    ![基本信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/947877/156523235851728_zh-CN.png)

6.  在**设置参数**页面，根据模板中设定的参数填写参数取值，完成后单击**下一步：确认创建**。 

    -   tagKey：填写您已经创建的标签键。
    -   tagValue：填写您已经创建的标签值。
    -   maxErrors：批量操作时的最大允许错误数，一旦超过您设置的取值，将不执行当前运维任务。maxErrors取值越小，表示该操作越谨慎。
    -   concurrency：批量操作时的并发控制。该参数主要实现并发数和批次的控制。
    ![设置参数](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/947877/156523235851744_zh-CN.png)

7.  在**确认创建**页面，预览和确认**基本信息**和**参数设置**，然后单击**创建执行**。

创建了运维任务后，您可以在**执行管理**页面查看运维任务的结果。

![执行管理](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/947877/156523235851768_zh-CN.png)

-   当**执行状态**显示**成功**，表示运维任务已完成。
-   当**执行状态**显示**失败**，您可以单击**操作**列下的**详情**查看**执行日志**，并根据日志信息分析和调整执行内容。

**相关文档**  


[模板概述](https://help.aliyun.com/document_detail/121329.htm)

[模板结构](https://help.aliyun.com/document_detail/120665.htm)

[执行概述](https://help.aliyun.com/document_detail/121317.htm)

[全自动执行](https://help.aliyun.com/document_detail/120701.htm)

[单步执行](https://help.aliyun.com/document_detail/120718.htm)

