# 部署Linux主机管理系统WDCP {#concept_bxm_sb5_2fb .concept}

WDlinux Control Panel（简称 wdCP），是一套通过 Web 控制和管理服务器的 Linux 服务器管理系统以及虚拟主机管理系统。在 wdCP 的后台里，您可以更方便地使用 Linux 系统作为我们的网站服务器系统，并对 Linux 服务器进行管理。

阿里云的云市场提供了丰富的镜像资源。镜像集成了操作系统和应用程序。创建实例时，您可以选择包含了应用环境的镜像，创建后无需再部署环境。

**说明：** 云服务器 ECS 不支持虚拟化软件（如 KVM、Xen、VMware 等）的安装部署。

根据业务需要，您可以选择下列任意一种方式部署 ECS 实例：

-   镜像部署
-   手动部署

通常情况下，推荐您使用镜像部署。如果您需要个性化定制部署，建议使用手动部署。下表列出了两种部署方式的特点。

|对比项|镜像部署|手动部署|
|:--|:---|:---|
|部署所需时间|3-5 分钟快速部署上云。|1-2 天，选择适合的操作系统、中间件、数据库、各类软件、插件、脚本，再进行安装和配置。|
|专业性|由运维过万级用户的云市场优质服务商提供。|依赖开发人员的开发水平。|
|个性化|支持主流应用场景。|可满足个性化部署需求。|
|安全性|经过严格审核，集成最稳定安全的版本。|依赖开发人员水平。|
|售后服务|专业售后工程师团队支持。|依赖运维人员经验，或由外包团队支持。|

本文档只介绍通用的操作步骤。一般镜像软件安装包都包含了操作指南，请阅读 [镜像操作指南](https://market.aliyun.com/products/53398003/cmjj010827.html?spm=5176.730005.0.0.8j3Qb6%22%E9%95%9C%E5%83%8F%E6%93%8D%E4%BD%9C%E6%8C%87%E5%8D%97%22) 进行具体的安装和配置。阿里云市场提供了种类丰富的镜像软件，[点击查看](https://market.aliyun.com/software)。

## 操作步骤 {#section_uff_yb5_2fb .section}

本节介绍的方法适用于已经购买实例，但想使用镜像重新部署环境的用户。此外，您也可以在创建实例的时候就选择镜像，请参考 [创建实例](https://help.aliyun.com/document_detail/25424.html)。

如果您想使用镜像市场的镜像来替换当前实例的操作系统，可以通过本节介绍的更换系统盘的方法来实现。

更换系统盘的时候，数据盘的数据则不会受到影响。建议将系统盘的个人数据备份到数据盘中，或采用其他方式进行备份。更换系统盘后，IP 地址不会改变。

**已购买的实例部署镜像**

如果您购买的实例已经开始运行，但是您想使用镜像市场中的镜像重新部署环境，操作步骤如下：

1.  登录 [云服务器管理控制台](https://ecs.console.aliyun.com/#/home)。
2.  找到需要重新部署环境的实例。
3.  若实例已经运行了一段时间，您想保留其中的数据，请提前 [创建快照](https://help.aliyun.com/document_detail/25455.html?spm=5176.product25365.6.716.6Qk3xD)，将数据备份到数据盘中。若该实例刚刚创建，可以直接停止实例。

    **说明：** 更换镜像后，系统盘的数据会全部被清空，服务器自动备份的快照也可能会被删除（取决于您的设置，请参见 [自动快照随磁盘释放](https://help.aliyun.com/document_detail/31691.html)）。请务必提前做好数据备份工作，提前 [创建快照](https://help.aliyun.com/document_detail/25455.html?spm=5176.product25365.6.716.6Qk3xD)。

4.  在弹出的 停止实例 框中，选择 **停止**，单击 **确认**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9775/154817555812398_zh-CN.png)

5.  实例停止后，单击实例名称，或者在实例的右侧选择 **更多** \> **更换系统盘**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9775/154817555812399_zh-CN.png)

6.  在弹出的 更换系统盘 框中，单击 **确定，更换系统盘**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9775/154817555812400_zh-CN.png)

7.  单击 **镜像市场**，然后单击 **从镜像市场选择（含操作系统）**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9775/154817555812401_zh-CN.png)

8.  在镜像市场列表的左侧，根据分类选择待使用的镜像，并在镜像的右下方单击 **同意并使用**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9775/154817555812402_zh-CN.png)

9.  在弹出的 云服务器更换操作系统温馨提示 框中，单击 **确定**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9775/154817555812403_zh-CN.png)


**未购买的实例部署镜像**

如果您还未购买ECS实例，可以在创建实例的同时直接部署镜像。

1.  登录 [云服务器管理控制台](https://ecs.console.aliyun.com/#/home)。
2.  进入 创建实例 页面，根据您的需求选择 **计费方式**、**地域**、**网络**、**实例配置**、**带宽**、**存储**、**购买量**，并在镜像处选择 **镜像市场**。
3.  根据关键词的搜索结果，单击 **购买**。
4.  使用镜像部署了 WDCP 主机管理系统后，您可以启动并登录实例，开始使用您的环境。使用方法请参考服务商提供的 [使用手册](https://oss.aliyuncs.com/netmarket/8134bfb9-bf7b-46a7-a44f-cdbaeb88a9d1.pdf?spm=5176.730006-cmjj015205.102.9.5NJuLT&file=8134bfb9-bf7b-46a7-a44f-cdbaeb88a9d1.pdf)。

    **说明：** 详情请参考镜像链接 [PHP运行环境（WDCPv3.0面板 多引擎切换 免费版）](https://market.aliyun.com/products/53398003/cmjj015205.html) 。


