# 阿里云安装SharePoint 2016 {#concept_spr_fzt_2fb .concept}

## 系统环境 {#section_wgg_tzt_2fb .section}

-   基础配置

    Windows Server 2012

    4C 8G （请根据真实环境设计架构以及购买服务器配置）

-   软件环境

    SQL server 2012 express

    Sharepoint 2016

    AD

    DNS

    IIS

-   必备组件

    Net Framework 3.5 \(安装SQL server 需要.net Framework 3.5 支持\)

    **说明：** 

    -   使用 **添加角色和功能** 安装可能会安装失败，参考链接：[Windows Server 2012 R2 或 2016 无法安装 .NET Framework 3.5.1](https://help.aliyun.com/knowledge_detail/38203.html)
    -   Sharepoint 必备组件可以参考微软官方文档 Sharepoint 安装时会提示安装依赖组件，如果依赖组件安装和安装失败，会导致 Sharepoint 无法安装。

## 安装 {#section_nwh_c15_2fb .section}

1.  搭建AD参考链接：[阿里云ECS Windows Server 2012 搭建AD](https://help.aliyun.com/document_detail/52565.html)

    **说明：** 客户端加域前记得修改SID，此篇文章只是为了介绍 Sharepoint 如何安装，使用的是一台服务器，所以将所有角色和功能都安装在一台服务器上（生产环境中千万不要将 SQL 和 AD以及 sharepoint 应用服务器服务器搭建在一起）。

2.  安装SQL SERVER 2012 Express。

    SQL SERVER 采用默认安装即可，由于是测试环境我这里使用的是express版本

    **说明：** 

    -   express 版本访问默认不支持 tcp/ip 协议，需要手动开启。
    -   express 版本默认（可能）没有管理控制台，需要单独安装 SQL 管理工具。
    -   生成系统建议使用企业版数据库，express 版本相对企业版缺少部分功能。
3.  安装Sharepoint 2016。

    安装 SharePoint 必备组件。

    **说明：** 使用自动安装工具需要服务器能访问外网，如果访问不了，需要手动下载组件，然后使用命令安装，具体可以查看微软官方文档。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9788/154817568412385_zh-CN.png)

    必备组件安装成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9788/154817568412386_zh-CN.png)

    所有组件安装完成后，重启服务器，然后开始安装 Sharepoint。

    运行SharePoint2016安装向导，输入产品 Key。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9788/154817568412387_zh-CN.png)

    开始安装 ShrePoint 2016。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9788/154817568412388_zh-CN.png)

    运行 SharePoint 配置向导。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9788/154817568412389_zh-CN.png)

    选择创建新的服务器场。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9788/154817568412390_zh-CN.png)

    指定配置数据库设置。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9788/154817568412391_zh-CN.png)

    指定服务器角色。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9788/154817568412392_zh-CN.png)

    **说明：** 此处为单台服务器做测试，因此选择单一服务器场。

    指定 SharePoint 管理中心端口以及安全设置。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9788/154817568412393_zh-CN.png)

    完成配置向导并开始安装。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9788/154817568412394_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9788/154817568412395_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9788/154817568412396_zh-CN.png)

    到这里就全部安装完成，后面可以通过管理中心配置服务器场，配置服务器场时选择开启自己需要的服务，否则会造成不必要的内存开支。


