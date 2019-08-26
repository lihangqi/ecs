# 创建实例时配置IPv6地址 {#concept_dnn_jh4_yfb .concept}

创建实例时，您可以配置一个IPv6地址。

## 前提条件 {#section_h4r_4k4_yfb .section}

-   ECS实例的IPv6功能目前处于公测阶段，您需要先 [申请公测](https://page.aliyun.com/form/act608662110/index.htm)。

-   实例所在的VPC和交换机已经开通IPv6网段。


## 操作步骤 {#section_dyh_4k4_yfb .section}

您可以按照 [使用向导创建实例](cn.zh-CN/用户指南/实例/创建实例/使用向导创建实例.md#) 的描述创建实例。在选择配置时，您需要注意以下几点：

-   在 基础配置 页面，筛选出 **支持IPv6** 的实例规格，并选择一个实例规格。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65336/154390843133467_zh-CN.png)

-   在 网络和安全组 页面，选择已开通IPv6的专有网络和交换机，并勾选 **免费分配 IPv6 地址**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65336/154390843133531_zh-CN.png)

-   在 确认订单 页面，确认已选择IPv6地址。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65336/154390843133488_zh-CN.png)


## 查看IPv6地址 {#section_vhx_1s4_yfb .section}

您可以通过以下步骤查看ECS实例配置的IPv6地址：

1.  登录 [云服务器ECS管理控制台](https://ecs.console.aliyun.com/#/home)。

2.  在左侧导航栏中，单击 **实例**。

3.  找到已创建的ECS实例，在 **操作** 列，单击 **管理**。

4.  在 **配置信息** 区域中，可以查看实例分配的 IPv6地址。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/65336/154390843133532_zh-CN.png)


