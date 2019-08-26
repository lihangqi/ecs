# 管理ECS实例自建数据库 {#task_wyv_z3g_chb .task}

ECS实例自建数据库，是指在ECS实例上安装并配置的数据库。您可以使用数据管理服务DMS来管理ECS实例自建数据库。本文以MySQL为例，介绍如何使用DMS添加并管理ECS实例自建数据库。

1.  开通数据管理服务，详情请参见[开通数据管理服务](https://help.aliyun.com/document_detail/47558.html)。
2.  创建ECS实例。具体步骤，请参见[使用向导创建实例](../../../../cn.zh-CN/实例/创建实例/使用向导创建实例.md#)。
3.  在ECS实例安全组的入方向添加规则，放行MySQL监听的端口号。MySQL默认监听的端口号为3306。
4.  在ECS实例上安装MySQL数据库。
5.  为ECS实例上的MySQL数据库创建非root账号。

    **说明：** MySQL默认情况下不允许root账号远程登录。若您已设置允许root账号远程登录，可跳过此步骤。

    本示例中，请运行以下命令为MySQL数据库创建名为dms、密码为123456的账号。

    ``` {#codeblock_y0q_ww8_aez}
    grant all on *.* to 'dms'@'%'IDENTIFIED BY '123456';
    ```


数据管理服务DMS（Data Management Service）是由阿里云提供的数据库管理Web终端，为您管理Windows系统和Linux系统下的ECS实例自建数据库。您只需在数据管理控制台上添加实例自建数据库即可使用数据管理功能，如新建数据库、新建表等。DMS支持的自建数据库类型有MySQL、SQLServer、PostgreSQL、MongoDB、Redis。更多详情，请参见[DMS产品文档](https://help.aliyun.com/document_detail/47550.html)。

1.  登录[数据管理控制台](https://dms.console.aliyun.com/#/dms/cloud/login)。
2.  在左侧导航栏中，选择**自建库（ECS、公网）**。
3.  单击**新建数据库**。
4.  配置自建数据库信息。 

    参数解释如下表所示。

    |参数|描述|
    |:-|:-|
    |数据库类型|ECS实例自建数据库的类型。本示例中选择MySQL。|
    |实例来源|ECS自建。|
    |地域|ECS实例所在地域。|
    |ECS实例ID|ECS实例ID。|
    |端口|ECS实例数据库监听的端口号。本示例中MySQL的端口号配置为3306。|
    |数据库 用户名|ECS实例自建数据库的账号。本示例中MySQL的账号为dms。 **说明：** 建议您使用非root账号。

 |
    |密码|ECS自建数据库账号对应的密码。本示例中，dms的密码为123456。|

5.  单击**登录**。 登录成功后，进入数据管理页面。通过数据管理页面提供的导航栏菜单，您可以管理数据库。

通过数据管理页面的顶部导航栏菜单，您可以对数据库进行下列操作：

-   **创建**：创建数据库、表、数据库用户、存储过程、函数、视图、触发器、事件。详细信息，请参见[数据库开发](https://help.aliyun.com/document_detail/47645.html)。
-   **SQL操作**：进入SQL操作界面，执行数据库的各种增删改查命令，包含执行结果集的快捷编辑与变更的提交。详细信息，请参见[SQL操作](https://help.aliyun.com/document_detail/47673.html)。
-   **数据方案**：导入导出数据、自动生成测试数据、数据库克隆、表结构对比、数据追踪、数据备份、数据恢复等操作。详细信息，请参见[数据管理](https://help.aliyun.com/document_detail/47661.html)。
-   **实例管理**：管理数据库的binlog日志文件、表数据量的统计。
-   **监控告警、诊断优化**：通过页面导航栏的**性能**菜单入口，管理数据库的一键诊断、慢SQL分析、空间诊断、实例会话管理、实时性能、诊断报告等信息。详细信息，请参见[数据库性能](https://help.aliyun.com/document_detail/57778.html)。
-   **工具**：数据库管理、用户管理、E-R图、批量操作表、生成文档（Word、Excel、PDF）。详细信息，请参见[扩展工具](https://help.aliyun.com/document_detail/63787.html)。

