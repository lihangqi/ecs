# VPC内网迁云 {#ExpressConnectMigration .concept}

如果您能直接从自建机房（Integrated Data Center，IDC）、虚拟机环境或者云主机访问某一阿里云地域下的专有网络VPC，建议您使用源服务器与VPC内网互连的迁云方案。VPC内网迁云能获得比通过公网更快速更稳定的数据传输效果，提高迁云工作效率。

## 前提条件 {#section_cww_qz1_kfb .section}

VPC内网迁云要求您能从IDC、虚拟机环境或者云主机访问目标VPC。具体实现方案可以选择高速通道服务或者VPN网关服务，利用高速通道的 [专线接入](https://www.alibabacloud.com/help/doc-detail/54210.html)功能或者在目标VPC中 [搭建VPN网关](https://www.alibabacloud.com/help/doc-detail/54211.html)。

**说明：** 高速通道或者VPN网关为付费云服务，请根据您的实际需要使用。更多详情，请参阅 [物理专线连接计费说明](../../../../../intl.zh-CN/产品定价/物理专线连接计费说明.md#) 和 [按量计费](../../../../../intl.zh-CN/产品定价/按量计费.md#)。

## client\_data说明 {#section_eww_qz1_kfb .section}

VPC内网迁云需要您自行编辑client\_data文件。client\_data记录了迁云过程中的数据文件，包含了以下信息：

-   迁云中转实例的ID、名称、公网带宽和IP地址等属性。
-   迁移数据盘的进程信息。
-   生成的自定义镜像名称。
-   中转实例部署的地域和网络类型。
-   中转实例使用的VPC、虚拟交换机和安全组。

    更多详情，请参阅下载后迁云工具的client\_data文件。


**警告：** 为避免迁云失败，若您没有VPC内网迁云需求，请勿自行修改配置文件client\_data。否则会影响迁云工作，出现进程卡顿等现象。

[下载迁云工具](http://p2v-tools.oss-cn-hangzhou.aliyuncs.com/Alibaba_Cloud_Migration_Tool.zip?spm=a2c4g.11186623.2.8.6B6W0i&file=Alibaba_Cloud_Migration_Tool.zip) 并打开client\_data文件后，您需要修改如下参数：

|名称|类型|是否必填|描述|
|:-|:-|:---|:-|
|net\_mode|Integer|否|选择数据传输方式。取值范围：-   0（默认）：数据从公网传输，此时要求源服务器能访问公网，数据从公网传输。
-   1：数据从VPC内网传输，此时要求源服务器能访问指定VPC。
-   2：数据从VPC内网传输，此时要求源服务器同时能访问公网和指定VPC。

VPC内网迁云需要将`net_mode`设置为1或者2。|
|vpc|Array|否|已经配置了高速通道服务或者VPN网关的VPC ID。当`net_mode=1`或`net_mode=2`时为必填参数。由必填的`vpc_id`和选填的`vpc_name`和`description`三个字符串（String）参数构成一个JSON数组，分别表示VPC ID、VPC名称和VPC描述。|
|vswitch|Array|否|指定VPC下的一台虚拟交换机ID。当`net_mode=1`或`net_mode=2`时为必填参数。由必填的`vswitch_id`和选填的`vpc_name`和`description`三个String参数构成一个JSON数组，分别表示虚拟交换机ID、虚拟交换机名称和虚拟交换机描述。|
|securegroupid|String|否|指定VPC下的安全组ID。|

## 源服务器能访问指定VPC {#section_nww_qz1_kfb .section}

以下步骤适用于`net_mode=1`的情形。迁云工程会分成3个阶段，其中阶段1（`Stage 1`）和阶段3（`Stage 3`）在备用服务器中完成，需要备用服务器能访问公网；阶段2（`Stage 2`）数据传输在待迁移的源服务器中进行。

1.  登录一台您能够访问公网的服务器A。

2.  编辑迁云工具的client\_data文件：设置 `net_mode=1`，填入已经配置了高速通道服务或者VPN网关的 `vpc_id`、`vswitch_id` 和 `zone_id` 参数。

3.  （可选）在client\_data文件中配置 `security_group_id` 参数，但安全组入方向必须放行代理端口8080和8703。更多详情，请参阅 [添加安全组规则](../intl.zh-CN/用户指南/安全组/添加安全组规则.md#)。

4.  按照 [公网迁云](intl.zh-CN/最佳实践/P2V 迁云实践/使用迁云工具迁移服务器至阿里云.md#) 步骤在服务器A内运行迁云工具，直到提示`Stage 1 Is Done!`。

    [![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733783688/Stage1.png)](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733783688/Stage1.png)

5.  登录您需要迁移的源服务器，复制服务器A的迁云工具配置，包括user\_config.json、rsync和client\_data文件，保持配置文件内容一致。

6.  按照 [公网迁云](intl.zh-CN/最佳实践/P2V 迁云实践/使用迁云工具迁移服务器至阿里云.md#) 步骤在待迁移的源服务器内运行迁云工具，直到提示`Stage 2 Is Done!`。

    [![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733805431/Stage2.png)](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733805431/Stage2.png)

7.  登录服务器A，复制待迁移的源服务器的迁云工具配置，包括user\_config.json、rsync和client\_data文件，必须保持配置文件内容一致。

8.  按照 [公网迁云](intl.zh-CN/最佳实践/P2V 迁云实践/使用迁云工具迁移服务器至阿里云.md#) 步骤在服务器A内再次运行迁云工具，直到提示 `Stage 3 Is Done!`，表示VPC内网迁云顺利完成。

    [![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733837163/Stage3.png)](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733837163/Stage3.png)


## 源服务器能访问公网和指定VPC {#section_www_qz1_kfb .section}

以下步骤适用于 `net_mode=2` 的情形，操作过程与 `net_mode=0` 时，即公网迁云相同。`net_mode=2` 时，数据自动从VPC迁移上云，其他过程走公网，传输速度稍微慢于VPC内网迁云方式一（`net_mode=1`）。

1.  登录您能够访问公网的源服务器，按照 [公网迁云](intl.zh-CN/最佳实践/P2V 迁云实践/使用迁云工具迁移服务器至阿里云.md#) 步骤运行迁云工具。

2.  编辑迁云工具的client\_data文件。设置 `net_mode=2`，填入已经配置了高速通道服务或者VPN网关的 `vpc_id`、`vswitch_id` 和 `zone_id` 参数。

3.  （可选）在client\_data文件中配置 `security_group_id` 参数，但安全组入方向必须放行代理端口8080和8703。更多详情，请参阅 [添加安全组规则](../intl.zh-CN/用户指南/安全组/添加安全组规则.md#)。

4.  按照 [公网迁云](intl.zh-CN/最佳实践/P2V 迁云实践/使用迁云工具迁移服务器至阿里云.md#) 步骤运行迁云工具。


## FAQ {#section_zww_qz1_kfb .section}

当迁云工作中断后，您可以查看 [迁云工具FAQ](intl.zh-CN/最佳实践/P2V 迁云实践/迁云工具 FAQ.md#) 或者 [添加迁云工具客户反馈钉钉群](https://h5.dingtalk.com/invite-page/index.html?spm=a2c4g.11186623.2.31.FEg99s&code=ca190154ff) 联系ECS迁云技术支持。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9833/154408646713339_zh-CN.png)

