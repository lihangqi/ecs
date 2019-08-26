# 使用ROS部署LNMP环境 {#concept_53077_zh .task}

LNMP分别代表Linux、Nginx、MySQL和PHP。本文介绍如何使用阿里云资源编排服务（ROS）一键部署LNMP环境。

-   使用本教程进行操作前，请确保您已经注册了阿里云账号。如还未注册，请先完成[账号注册](https://account.aliyun.com/register/register.htm?)。
-   账号余额不能低于100.00元，可以是现金、可用信用额度或者可用于开通产品的代金券。

ROS是阿里云官网提供的免费服务，无需下载安装。您可以使用ROS创建JSON格式的资源栈模板文件，或者使用ROS控制台提供的模板样例创建一组阿里云资源，详情请参见[模板样例](https://ros.console.aliyun.com/#/template/list)。在本教程中，我们使用ROS控制台提供的**LNMP\_basic**模板，自动创建一台ECS实例，并在实例上部署LNMP环境。

您还可以使用ROS提供的其他模板样例搭建环境，例如Java Web测试环境、Node.js测试开发环境、Ruby Web开发测试环境或Hadoop/Spark分布式系统。

更多ROS信息，请参见[ROS文档](../../../../../cn.zh-CN/产品简介/什么是资源编排服务？.md#)和[ROS云栖博客](https://yq.aliyun.com/articles/57553)。

1.  登录[ROS管理控制台](https://ros.console.aliyun.com/)。 

    **说明：** 如果您是首次使用ROS，必须先开通ROS服务。ROS服务免费，开通服务不会产生任何费用。

2.  在左侧导航栏中，单击**关键帮助** \> **ECS实例相关信息**，获取您需要的ECS实例规格、可用区ID（ZoneId）和镜像ID（ImageId）。
3.  在左侧导航栏中，单击**模板样例**。
4.  从模板样例中，找到**LNMP\_basic**。 

    ![查找模板](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9761/156560600612071_zh-CN.png)

5.  单击**预览**查看模板的JSON文件。JSON文件各个顶级字段的解释如下表所示。 

    |顶级字段|解释|
    |:---|:-|
    |`"ROSTemplateFormatVersion" : "2015-09-01"`|定义模板版本。|
    |     ``` {#codeblock_c7s_g3y_5i6}
"Description": "Deploy LNMP(Linux+Nginx+MySQL+PHP) stack on 1 ECS instance. ***
              WARNING *** Only support CentOS-7."
    ```

 |解释说明模板。|
    |`"Parameters" : { }`|定义模板的一些参数。本示例中，模板定义的参数包括：镜像ID、实例规格等，并指定了默认值。|
    |`"Resources" : { }`|定义这个模板将要创建的阿里云资源。本示例中，申明将要创建一个ECS实例和一个安全组，这里申明的资源属性可以引用`Parameters`中定义的参数。|
    |`"Outputs": { }`|定义资源创建完成后，栈需要输出的资源信息。本示例中，资源创建完成后将输出ECS实例ID、公网IP地址和安全组ID。|

    **说明：** 关于ROS资源栈模板的更多信息，请参见资源编排的[模板结构说明](../../../../../cn.zh-CN/用户指南/模板语法/模板结构说明.md#)。

6.  单击**创建栈**。
7.  从**选择地域（region）**列表，选择具体地域。本示例中，选择**华东1（杭州）**。然后单击**下一步**。
8.  设置栈的相关参数，然后单击**创建**。 

    -   **栈名**：设置一个栈名，不可重复，而且创建之后不能修改。
    -   **创建超时（分钟）**：设置一个时间。如果在设置的时间段内资源未创建成功，则判断为创建超时。您可以选择是否**失败回滚**。如果选择失败回滚，那么创建过程中发生任何失败操作（包括创建超时），ROS都会删除已经创建成功的资源。
    -   **Nginx Download Url**：使用默认的Nginx下载地址。
    -   **DB Password**和**\(Please Confirm\) DB Password**：设置并确认访问MySQL数据库的密码。根据模板定义，密码只能包括英文字母和数字。
    -   **The ECS Available Zone ID**：填写您需要创建资源的可用区ID。详见第2步。
    -   **ECS Image Id**：填写创建ECS实例时使用的镜像ID。详见第2步。
    -   **DB Name**：填写MySQL数据库名。
    -   **DB Username**：填写MySQL数据库的用户名。
    -   **DB Root Password**和**\(Please Confirm\) DB Root Password**：设置并确认MySQL root账号的密码。根据模板定义，密码只能包括英文字母和数字。
    -   **ECS Instance Type**：填写您需要的ECS实例规格。详见第2步。
    -   **System Disk Category**：选择系统盘的云盘类型。
    -   **Instance Password**和**\(Please Confirm\) Instance Password**：设置并确认实例的登录密码。根据模板定义，密码只能包括大写或小写英文字母和数字。
    ![设置参数](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9761/156560600612072_zh-CN.png)

9.  在左侧导航栏中，单击**资源栈管理**查看新创建的栈的状态。 

    ![资源栈管理](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9761/156560600614331_zh-CN.png)

10. 单击新创建的栈的名称。在栈概况页面的**输出**区域查看`NginxWebsiteURL`的值。您能通过这个地址访问已创建的LNMP环境。 

    ![查看栈概况](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9761/156560600714341_zh-CN.png)

    **说明：** 

    -   在资源列表页面查看栈中所有资源。
    -   在事件列表页面查看ROS创建这个资源栈过程中产生的操作记录。任何涉及资源栈的操作失败后，列表中均会显示操作失败的原因。
    -   在栈模板页面查看资源栈的原始模板。

