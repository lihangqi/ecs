# 在ECS上部署数据库 {#concept_zr2_x5t_2fb .concept}

数据库是依照某种数据模型组织起来并存放二级存储器中的数据集合。这种数据集合具有如下特点：尽可能不重复，以最优方式为某个特定组织的多种应用服务，其数据结构独立于使用它的应用程序，对数据的增、删、改和检索由统一软件进行管理和控制。

阿里云有提供相应的高可用数据库架构RDS，但由于RDS具有一定的限制条件，可能无法满足部分生产环境的要求，例如需要使用Oracle数据库、需要使用SQL Server报表服务等，在这种情况下，我们需要考虑在ECS上搭建数据库的方式。

本文档介绍如何在云服务器ECS实例搭建常用数据库（Oracle、MySQL、SQL Server）。

## 常用数据库简介 {#section_dlv_pwt_2fb .section}

常用数据库包含以下三种：Oracle、MySQL、SQL Server。

**Oracle**

Oracle可以支持多种不同的硬件和操作系统平台，从台式机到大型和超级计算机，为各种硬件结构提供高度的可伸缩性，支持对称多处理器、群集多处理器、大规模处理器等，并提供广泛的国际语言支持。

Oracle是一个多用户系统，能自动从批处理或在线环境的系统故障中恢复运行。系统提供了一个完整的软件开发工具Developer2000，包括交互式应用程序生成器、报表打印软件、字处理软件以及集中式数据字典，用户可以利用这些工具生成自己的应用程序。

Oracle以二维表的形式表示数据，并提供了SQL\(结构式查询语言\)，可完成数据查询、操作、定义和控制等基本数据库管理功能。

Oracle具有很好的可移植性，通过它的通信功能，微型计算机上的程序可以同小型乃至大型计算机上的Oracle，并且能相互传递数据。

Oracle属于大型数据库系统，主要适用于大、中小型应用系统，或作为客户机/服务器系统中服务器端的数据库系统。

**MySQL**

MySQL是一种开放源代码的关系型数据库管理系统（RDBMS），MySQL数据库系统使用最常用的数据库管理语言—结构化查询语言（SQL）进行数据库管理。MySQL数据库也是可以跨平台使用的（如linux和Windows）。

**SQL Server**

SQL Server是美国Microsoft公司推出的一种关系型数据库系统，是一个可扩展的、高性能的、为分布式客户机/服务器计算所设计的数据库管理系统，实现了与WindowsNT的有机结合，提供了基于事务的企业级信息管理系统方案，SQL Server 2016以前的版本只支持在Windows上运行，不支持在Linux上运行。

## 在ECS（Windows系统）上部署Oracle数据库 {#section_ew5_twt_2fb .section}

企业中在Windows上部署Oracle数据库的方式是先部署一台Windows系统的机器，然后在Windows系统上安装Oracle软件。这种部署方式具有耗时长、部署复杂、易出错等缺陷。在阿里云平台上，可通过自带的镜像市场实现一键部署Windows系统的Oracle数据库，完美解决耗时长、部署易出错的缺陷。

**操作步骤**

1.  登录云服务器管理控制台。
2.  选择 **云服务器** \> **创建实例**。在创建实例的页面上，定位到镜像，单击 **镜像市场**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571212359_zh-CN.png)

3.  单击镜像市场的 **从镜像市场选择（含操作系统）**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571212360_zh-CN.png)

4.  在镜像市场的页面，选择 **数据库**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571212361_zh-CN.png)

5.  在操作系统选择，选择主流使用的Windows Server 2012，架构选择64位系统。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571212362_zh-CN.png)

6.  在下方查看到具有Windows2012 x64 oracle11g11.1.0.4企业版，单击购买。
7.  进入到购买页面，单击购买即可。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571212363_zh-CN.png)

8.  购买完成配置后，如需要正常使用，还需要在ECS所属的安全组配置入方向的开放1521、1158端口，安全组 [添加安全组规则](http://help.aliyun.com/document_detail/25471.html) 操作。

## 在ECS（Linux系统）上部署Oracle数据库 {#section_ip2_3xt_2fb .section}

在阿里云上自带的镜像市场还包含Linux系统的Oracle数据库，可通过购买实现一键部署Linux系统的Oracle数据库，节省大量的敲击代码的时间。

**操作步骤**

1.  登录云服务器管理控制台。
2.  选择 **云服务器** \> **创建实例**。在创建实例的页面上，定位到镜像，单击 **镜像市场**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571212364_zh-CN.jpg)

3.  单击镜像市场的 **从镜像市场选择（含操作系统）**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571212365_zh-CN.jpg)

4.  在镜像市场的页面，在搜索框中输入Oracle。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571212366_zh-CN.png)

5.  列出了相应的Oracel数据库的版本，选择相应的版本进行购买。
6.  进入到购买页面，单击购买即可。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571312367_zh-CN.png)

7.  购买完成配置后，如需要正常使用，还需要在ecs的所属的安全组配置入方向的开放1521、1158端口，安全组 [添加安全组规则](http://help.aliyun.com/document_detail/25471.html) 操作。

## 在ECS（Windows系统）上部署SQL Server数据库 {#section_uvr_qxt_2fb .section}

企业中还会用到微软SQL Server数据库，因目前SQL Server 2016之前的版本只支持在Windows上运行安装，所以本文档只介绍在Windows系统的ECS实例上部署SQL Server数据库的方法。

**操作步骤**

1.  登录云服务器管理控制台。
2.  单击左侧导航中的 **云服务器** \> **创建实例**。在创建实例的页面上，定位到镜像，单击 **镜像市场**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571312368_zh-CN.jpg)

3.  单击镜像市场的 **从镜像市场选择（含操作系统）**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571312369_zh-CN.jpg)

4.  在镜像市场的页面，在搜索镜像框中输入SQL Server。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571312370_zh-CN.png)

5.  选择需要的相应版本，单击购买，进入到购买页面，单击购买即可。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571312371_zh-CN.png)

6.  购买完成配置后，如需要正常使用，还需要在ecs的所属的安全组配置入方向的开放1433、1434端口，安全组 [添加安全组规则](http://help.aliyun.com/document_detail/25471.html) 操作。

## 在ECS（Linux系统）上部署MySQL数据库 {#section_tqs_1yt_2fb .section}

MySQL数据库在企业中经常被用到，阿里云除了有RDS云数据库产品支持MySQL外，在云镜像市场中还有已完成安装MySQL数据库的Linux系统，可借助云镜像市场实现便捷、快速地部署MySQL数据库。

**操作步骤**

1.  登录云服务器管理控制台。
2.  单击左侧导航中的 **云服务器** \> **创建实例**。在创建实例的页面上，定位到镜像，单击 **镜像市场**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571312372_zh-CN.jpg)

3.  单击镜像市场的 **从镜像市场选择（含操作系统）**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571312373_zh-CN.jpg)

4.  在镜像市场的页面，选择数据库，在搜索框中输入MySQL。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571312374_zh-CN.png)

5.  选中相应的版本及规格，单击购买，进入到购买页面，单击购买即可。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571312375_zh-CN.png)

6.  安装后，如需要正常使用，还需要在ecs的所属的安全组配置入方向的开放3306端口，安全组 [添加安全组规则](http://help.aliyun.com/document_detail/25471.html) 操作。

## 在ECS（Windows系统）上部署MySQL数据库 {#section_uwn_3yt_2fb .section}

目前在云市场上暂未包含有Windows系统的MySQL数据库的镜像，所以需要手动部署MySQL数据库。

**操作步骤**

1.  登录云服务器管理控制台，购买相应的Windows Server实例，可参考 [购买Windows实例](http://help.aliyun.com/document_detail/25424.html)。
2.  购买成功后，进行相应的系统层面配置，远程登录ECS实例。
3.  进入 [MySQL官网](https://www.mysql.com/) 下载MySQL的安装包。
4.  安装MySQL之前，需要先下载插件vcredist\_x86.exe。
5.  安装vcredist\_x86.exe插件。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571312376_zh-CN.png)

6.  下载完成后，打开 **mysql-installer-community-5.6.15.0.msi** 进行MySQL安装。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571312377_zh-CN.png)

7.  选择第一项 **Install MySQL Products**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571312378_zh-CN.png)

8.  勾选接受协议和跳过检测更新，进入下一步，单击 **Custom**，也就是自定义安装，右边是选择MySQL的安装位置和数据库位置，下图操作案例选择的是默认路径，单击 **NEXT**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571312379_zh-CN.png)

9.  保持默认点解 **NEXT**， 单击 **Execute**，开始执行安装。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571312380_zh-CN.png)

10. 单击 **NEXT** 至配置页面，选择 **Server Machine**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571412381_zh-CN.png)

11. 保持默认 **NEXT** 输入管理员root的密码，直至最后完成安装；安装完成后会在页面出现MySQL的管理命令控制台。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9783/154817571412382_zh-CN.png)

12. 安装后，如需要正常使用，还需要在ECS的所属的安全组配置入方向的开放3306端口，安全组 [添加安全组规则](http://help.aliyun.com/document_detail/25471.html) 操作。

