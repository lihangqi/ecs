# 为已有实例分配IPv6地址 {#task_iqm_nt4_yfb .task}

如果您已经创建了实例，您可以为已有的实例分配IPv6地址。

-   实例支持IPv6。支持的实例规格请参见 [实例规格族](cn.zh-CN/产品简介/实例规格族.md#)。
-   实例网络类型为专有网络。
-   实例的状态为 **运行中** 或 **已停止**。

默认情况下，您创建的实例只分配私有IPv4地址，不分配IPv6地址。

1.  登录 [云服务器ECS管理控制台](https://ecs.console.aliyun.com/#/home)。 
2.  在左侧导航栏中，单击 **实例**。 
3.  选择已创建的ECS实例，单击 **操作** 列下的 **管理**。 
4.   在 配置信息 区域， 单击 **更多** \> **管理辅助私网IP** 。![管理辅助私网IP地址](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65345/154769552933569_zh-CN.png)

 
5.  单击 **分配IPv6地址**。 

    ![分配IPv6地址](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65345/154769552933570_zh-CN.png)

6.  选择IPv6地址分配方式。 

    -   **自动分配**：系统自动分配一个新的IPv6地址。
    -   **指定地址**：需要您补全IPv6地址。
    ![自配方式](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65345/154769552933571_zh-CN.png)

    ![手动分配](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65345/154769552933572_zh-CN.png)

7.  单击 **修改**。 

-   （可选）您可以 [查看分配的IPv6地址](cn.zh-CN/.md#)。
-   为已创建实例分配的IPv6地址默认是VPC内网通信，如果您需要使用IPv6地址进行公网通信，您可以 [开通IPv6公网带宽](../../../../../cn.zh-CN/用户指南/管理IPv6公网带宽/开通IPv6公网带宽.md#)。

