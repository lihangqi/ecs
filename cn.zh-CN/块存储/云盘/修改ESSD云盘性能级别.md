# 修改ESSD云盘性能级别 {#task_810820 .task}

您可以在使用ESSD云盘的过程中，在线升级性能级别。

您在创建ECS实例时可以选择ESSD云盘作为系统盘或者数据盘，也可以单独创建一块ESSD云盘。创建ESSD云盘的详细步骤请参见[使用向导创建实例](../cn.zh-CN/实例/创建实例/使用向导创建实例.md#)和[创建按量付费云盘](cn.zh-CN/块存储/云盘/创建云盘/创建按量付费云盘.md#)。更多有关ESSD云盘的信息，请参见[ESSD云盘](cn.zh-CN/块存储/云盘/ESSD云盘.md#)。

升级ESSD云盘性能级别时，您需要注意以下内容：

-   您的账号不能处于欠费状态。
-   若ESSD云盘已挂载到包年包月ECS实例上，则实例不能处于过期状态。
-   新创建的ESSD云盘请您等待云盘进入**待挂载**（Available）状态后再升级ESSD云盘性能级别。
-   升级ESSD云盘性能级别后，系统按照新性能级别单价计算消费账单。

本文描述如何在ECS管理控制台上升级ESSD云盘性能级别，您也可以调用API [ModifyDiskSpec](../cn.zh-CN/API参考/块存储/ModifyDiskSpec.md#)完成操作。

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。
2.  在左侧导航栏，单击**存储与快照** \> **云盘**。
3.  在顶部状态栏处，选择地域。
4.  找到目标ESSD云盘，在**操作**列，单击**更多** \> **修改性能级别**。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/655586/156644115850139_zh-CN.png)

5.  在修改性能级别窗口中，选择一个更高的**性能级别**，单击**确定**。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/655586/156644115850141_zh-CN.png)


由于ESSD云盘可以选择的性能级别与存储容量有关，如果您的ESSD云盘无法选择更高性能级别，可以先[扩容云盘](cn.zh-CN/块存储/云盘/扩容云盘/扩容概述.md#)，再修改ESSD云盘性能级别。

