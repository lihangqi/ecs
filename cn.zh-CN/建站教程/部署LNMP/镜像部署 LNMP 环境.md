# 镜像部署 LNMP 环境 {#concept_25427_zh .concept}

LNMP分别代表Linux、Nginx、MySQL、PHP。本文介绍如何在ECS实例上使用镜像部署LNMP环境。

您可选用以下几种方式在ECS实例上部署LNMP环境：

-   镜像部署LNMP环境。
-   [一键部署LNMP环境](cn.zh-CN/建站教程/部署LNMP/一键部署LNMP环境.md#)。
-   [手动部署LNMP环境](cn.zh-CN/建站教程/部署LNMP/搭建LNMP环境（CentOS 6）.md#)。

下表列出了镜像部署和手动部署两种方式的特点。一般推荐镜像部署。如果您需要个性化定制部署，建议使用手动部署。

|对比项|镜像部署|手动部署|
|:--|:---|:---|
|部署所需时间|3-5分钟，快速部署上云|1-2天。选择适合的操作系统、中间件、数据库、各类软件、插件、脚本，再进行安装和配置|
|专业性 IOPS|由运维过万级用户的优质服务商提供|依赖开发人员的开发水平|
|个性化|支持主流应用场景|可满足个性化的部署要求|
|安全性|经过严格安全审核，集成最稳定安全的版本|依赖开发人员的开发水平|
|售后服务|专业售后工程师团队支持|依赖运维人员的经验，或由外包团队支持|

**说明：** 

-   本文档只介绍通用的操作步骤。一般镜像软件安装包都包含了操作指南，请阅读镜像操作指南进行具体的安装和配置。
-   阿里云的 [云市场](http://market.aliyun.com/) 提供了丰富的镜像资源。镜像集成了操作系统和应用程序。在创建实例时，您可以选择包含了应用环境的镜像，创建后无需再部署环境。
-   云服务器 ECS 不支持虚拟化软件（如 KVM、Xen、VMware 等）的安装部署。

## 操作步骤 {#section_sxr_352_2fb .section}

**说明：** 

-   本节介绍的方法适用于已经购买实例、但想使用镜像重新部署环境的用户。此外，您也可以在创建实例的时候就选择镜像，请参考 [创建实例](../../../../cn.zh-CN/个人版快速入门/步骤 2：创建ECS实例.md#)。
-   如果您想使用镜像市场的镜像来替换当前实例的操作系统，可以通过本节介绍的更换系统盘的方法来实现。
-   更换系统盘的时候，**数据盘** 的数据则不会受到影响。因此建议您将系统盘的个人数据备份到数据盘中，或采用其他方式进行备份。
-   更换系统盘后，IP 地址不会改变。

如果您购买的实例已经开始运行，但是您想使用镜像市场中的镜像重新部署环境，操作步骤如下：

1.  登录 [ECS管理控制台](https://ecs.console.aliyun.com/#/home)。
2.  单**我的资源**部分下的**云服务器**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9762/154391304114386_zh-CN.png)

3.  在**实例列表**里找到需要重新部署环境的实例，单击实例ID或右边的**管理**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9762/154391304121022_zh-CN.png)

4.  如果该实例刚刚创建，可以在**实例详情**页面单击**停止**。如果实例已经运行了一段时间，您想保留其中的数据，请在操作前将数据备份到数据盘中。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9762/154391304114390_zh-CN.png)

    **说明：** 在更换镜像后，系统盘的数据会全部被清空，服务器的自动备份的快照也可能会被删除（取决于您的设置，请参见[设置自动快照随云盘释放](../../../../cn.zh-CN/用户指南/快照/设置自动快照随云盘释放.md#)）。因此务必做好数据备份工作。

5.  击单**提醒**窗口的**确定**按钮。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9762/154391304114393_zh-CN.png)

6.  选择**停止方式**，设置**停止模式**，然后单击**确定**停止实例。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9762/154391304114395_zh-CN.png)

    **说明：** 如果您停止实例是为了更换系统盘、重新初始化磁盘、更改实例规格、修改私网IP等操作，建议您勾选**停止后仍旧保留实例并继续收费**选项，避免启动失败。

7.  在 **配置信息**部分，单击 **更多**选择**更换系统盘**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9762/154391304214397_zh-CN.png)

8.  在提示消息中，单击 **确定，更换系统盘**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9762/154391304214398_zh-CN.png)

9.  单击 **镜像市场**，然后单击 **从镜像市场选择（含操作系统）**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9762/154391304221021_zh-CN.png)

10. 镜像市场列表的左侧是镜像的分类。您可以根据分类，选择想使用的镜像,。也可以在搜索栏里输入想使用的镜像，然后单击**搜索**。找到需要的镜像后，单击 **使用**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9762/154391304221036_zh-CN.png)

11. 输入登录密码，然后在**确认密码**中再输入一次。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9762/154391304221042_zh-CN.png)

12. 在页面的右下角， 勾选**《云服务器ECS服务条款》**和**《镜像商品使用条款》**，然后单击**确定更换**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9762/154391304221043_zh-CN.png)

13. 窗口提示系统盘更换成功。单击**返回实例列表**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9762/154391304221046_zh-CN.png)


您成功使用镜像部署了环境。现在可以启动、登录实例，开始使用您的环境了。

