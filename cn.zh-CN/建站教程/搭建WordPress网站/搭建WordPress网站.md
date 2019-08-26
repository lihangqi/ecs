# 搭建WordPress网站 {#concept_43244_zh .concept}

WordPress是使用PHP语言开发的博客平台，在支持PHP和MySQL数据库的服务器上，您可以用WordPress架设自己的网站，也可以用作内容管理系统（CMS）。建站时需要准备域名、空间和程序。使用WordPress镜像创建ECS实例，不需要部署Web环境，解决了空间和程序的问题，只要注册域名，完成备案，网站就可以直接上线，降低了建站的门槛，即买即用。

本文档介绍如何使用阿里云云市场的 [WordPress纯净版免费镜像](https://market.aliyun.com/products/52738005/cmjj027560.html) 或者 [WordPress商用主题镜像](https://market.aliyun.com/products/53616009/cmjj028448.html) 创建实例，并上线网站。

## 适用对象 {#section_ex5_zh2_2fb .section}

适用于刚开始使用阿里云建站的企业或个人用户。

## 基本流程 {#section_stw_132_2fb .section}

使用 [WordPress纯净版免费镜像](https://market.aliyun.com/products/52738005/cmjj027560.html) 或者 [WordPress商用主题镜像](https://market.aliyun.com/products/53616009/cmjj028448.html) 在ECS实例上搭建网站的步骤如下：

第1步：购买WordPress镜像

第2步：安装企业官网模板主题

第3步：修改主题元素

第4步：购买域名

第5步：备案

第6步：解析域名

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9753/153795944912060_zh-CN.png)

**第1步. 购买WordPress镜像**

假设您第一次使用阿里云ECS服务，按以下步骤创建一台基于 [WordPress纯净版免费镜像](https://market.aliyun.com/products/52738005/cmjj027560.html) 或者 [WordPress商用主题镜像](https://market.aliyun.com/products/53616009/cmjj028448.html) 的ECS实例。

1.  登录 [阿里云](https://account.aliyun.com/login/login.htm)。如果尚未注册，单击 [免费注册](https://account.aliyun.com/register/register.htm)。
2.  进入云市场，找到 [WordPress纯净版免费镜像](https://market.aliyun.com/products/52738005/cmjj027560.html) 或者 [WordPress商用主题镜像](https://market.aliyun.com/products/53616009/cmjj028448.html)，并单击 **立即购买**。
3.  在云服务器ECS 自定义购买 页面，完成如下 **基础配置**：
    1.  选择 **计费方式**：如果您需要备案网站，必须选择 **包年包月**，并在页面底部设置 **购买时长** 不少于3个月。如果不需要备案，您可以根据自己的需求选择计费方式。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9753/153795944912061_zh-CN.png)

    2.  选择 **地域**：目前支持该镜像的地域包括华北1、华北2、华北3、华北5、华东1、华东2、华南1。请根据网站用户的分布和您自己的地理位置选择合适的地域。如何选择地域与可用区，请参见 [地域与可用区](http://help.aliyun.com/document_detail/40654.html)。

        **说明：** 

        -   实例创建成功后，不能更改地域和可用区。
        -   不同地域提供的可用区数量、实例规格族、存储类型、实例价格等也会有所差异。请根据您的业务需求选择地域。
    3.  选择 **实例**：根据您网站的预期访问量选择实例规格（CPU、内存）。一般企业网站，通用或入门级的1核2 GiB或者2核4 GiB实例规格能满足需求。关于实例规格的详细介绍，请参见 [实例规格族](http://help.aliyun.com/document_detail/25378.html)。
    4.  选择 **镜像**：已经设置为 **镜像市场** 的 **WordPress纯净版免费镜像 WordPress4.9.4纯净版** 或者 **WordPress商用主题镜像 php-wordPress1.0.8**。您也可以根据需求，单击 **重新选择镜像** 从镜像市场选择其他WordPress镜像。
    5.  选择 **存储**：
        -   **系统盘**：必填项。您可以选择云盘类型和云盘容量。本示例中，系统盘类型选择 **高效云盘**，大小采用镜像文件大小，即46 GiB。
        -   **数据盘**：选填项。建议您创建一块50 GiB的高效云盘作为数据盘，不加密。
4.  单击 **下一步：网络和安全组**，并完成 **网络和安全组** 配置：
    1.  选择 **网络**：选择 **专有网络**。如果您未创建专有网络和交换机，选择 **默认专有网络** 和 **默认交换机**。

        **说明：** 如果您已经创建过经典网络类型的ECS实例，而且选择的实例类型也支持经典网络，那么，您可以选择 **经典网络**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9753/153795944912062_zh-CN.png)

    2.  设置 **公网带宽**：因为创建的实例需要访问公网，所以，您需要选择 **分配公网IP地址**，并根据预期的网站出网流量，选择 **按固定带宽** 或 **按使用流量** 计费，并设置带宽。建议选择 **固定带宽**，而且带宽值建议不低于2 Mbps。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9753/153795944912063_zh-CN.png)

    3.  选择 **安全组**：如果在当前地域内未创建过安全组，您可以使用默认安全组，并选择 **HTTP 80 端口**。

        **说明：** 如果您已经创建了安全组，必须在安全组中添加规则，放行入方向允许对HTTP 80端口的访问。详细信息，请参见 [添加安全组规则](http://help.aliyun.com/document_detail/25471.html)。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9753/153795944912064_zh-CN.png)

5.  单击 **下一步：系统配置**，完成系统配置：
    1.  设置 **登录凭证**：建议您在这里直接设置实例的登录密码。请务必牢记登录名和密码。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9753/153795944912065_zh-CN.png)

    2.  设置 **实例名称**、**描述** 和 **主机名**，为了便于以后管理。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9753/153795944912066_zh-CN.png)

6.  略过 **下一步：分组设置**，单击 **确认订单**：
    -   确认 **所选配置**。如果需要修改配置，单击 ![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/44543/cn_zh/1527648165582/edit_icon.png) 图标，重新选择配置。
    -   确认购买时长（比如本例中的3个月），并决定是否开启 **自动续费** 功能。
7.  阅读并确认《云服务器 ECS 服务条款》和《镜像商品使用条款》。
8.  单击 **确认下单**。
9.  确认订单并付款。

实例开通后，单击 **管理控制台** 回到ECS管理控制台查看新建的ECS实例。在相应地域的 **实例列表** 里，您能查看新建实例的实例名称、公网IP地址、内网IP地址或私有IP地址等信息。

**第2步. 安装企业官网模板主题**

为了满足企业官网展示的需求，您需要安装适合的主题模板。这部分主要介绍如何安装WordPress主题模板。

1.  [远程连接Windows实例](http://help.aliyun.com/document_detail/25435.html)。
2.  打开IE浏览器，使用 `http://实例公网IP地址/wp-admin` 进入WordPress登录页面。
3.  输入用户名 **admin** 和初始密码 **admin123**，并单击 **登录**。
4.  在 仪表盘 页面的左侧导航栏中，选择 **外观** \> **主题** 。
5.  在 **主题** 页面上选择已经安装的主题。

    **说明：** 登录后，建议您在 **编辑我的个人资料** 的 **账户管理** 中修改密码。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9753/153795944912070_zh-CN.png)


**第3步. 修改主题元素**

安装主题后，您可以修改主题元素，打造您自己的专属网站。具体操作，请参见镜像供应商飞色网络的 [帮助中心](http://help2.facecloud.net/wordpress)。

**第4步. 购买域名**

为了便于您的使用易记的域名访问您的网站，您可以给自己的网站设定一个单独的域名。您可以参考 [域名注册流程](http://help.aliyun.com/document_detail/54068.html) 完成操作。

**第5步. 备案**

假设您是第一次备案域名，具体操作流程，请参见 [首次备案流程图文引导](http://help.aliyun.com/document_detail/36922.html)。其他情况下，请参见 [备案导航](http://help.aliyun.com/document_detail/61819.html)。

**第6步. 解析域名**

域名解析是使用域名访问您的网站的必备环节。具体操作流程，请参见 [设置域名解析](http://help.aliyun.com/document_detail/29716.html)。

## 扩展服务容量 { .section}

随着业务的扩展，您还可以借助阿里云强大的产品平台，横向和纵向扩展服务容量，例如：

-   扩展单个ECS实例的vCPU和内存规格，增强服务器的处理能力。详细信息，请参见 [升降配概述](http://help.aliyun.com/document_detail/25437.html)。
-   增加多台ECS实例，并利用负载均衡，在多个实例中进行负载的均衡分配。详细信息，请参见 [购买相同配置实例](http://help.aliyun.com/document_detail/25432.html) 和 [什么是负载均衡](http://help.aliyun.com/document_detail/27539.html)。
-   利用弹性伸缩（Auto Scaling），根据业务量自动增加或减少ECS实例的数量。详细信息，请参见 [什么是弹性伸缩](http://help.aliyun.com/document_detail/25857.html)。
-   利用对象存储OSS（Object Storage Service），存储静态网页和海量图片、视频等。详细信息，请参见 [什么是OSS](http://help.aliyun.com/document_detail/31817.html)。

