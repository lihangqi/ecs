# VPC内网迁云 {#ExpressConnectMigration .concept}

如果您能直接从自建机房（Integrated Data Center，IDC）、虚拟机环境或者云主机访问某一阿里云地域下的专有网络VPC，建议您使用源服务器与VPC内网互连的迁云方案。

## 前提条件 {#section_cww_qz1_kfb .section}

VPC内网迁云要求您能从IDC、虚拟机环境或者云主机访问目标VPC。具体实现方案可以选择高速通道服务或者VPN网关服务，利用高速通道的[专线接入](https://help.aliyun.com/document_detail/54210.html)功能或者在目标VPC中[搭建VPN网关](https://help.aliyun.com/document_detail/54211.html)。

**说明：** 高速通道或者VPN网关为付费云服务，请根据您的实际需要使用。更多详情，请参见[物理专线连接计费说明](../../../../cn.zh-CN/产品定价/物理专线连接计费说明.md#)和[预付费](../../../../cn.zh-CN/产品定价/预付费.md#)。

## client\_data说明 {#section_eww_qz1_kfb .section}

**警告：** 为避免迁云失败，若您没有VPC内网迁云需求，请勿自行修改配置文件client\_data。否则会影响迁云工作，出现进程卡顿等现象。

VPC内网迁云需要您自行编辑client\_data文件。client\_data记录了迁云过程中的数据，主要包含了以下信息：

-   迁云源系统信息：系统平台架构等。
-   迁云中转VPC信息：VPC ID、虚拟交换机 ID、安全组ID等。
-   迁云中转实例信息：实例ID、实例规格、IP地址，中转磁盘等信息。
-   迁移目标信息：目标镜像ID等。
-   迁云工具配置信息：传输配置、网络配置、API服务配置等。

VPC内网迁移client\_data相关配置参数如下：

|名称|类型|是否必填|描述|
|:-|:-|:---|:-|
|extra.net.net\_mode|Integer|否|选择数据传输方式。取值范围： -   0（默认）：数据从公网传输，此时要求源服务器能访问公网，数据从公网传输。
-   1：数据从VPC内网传输，此时要求源服务器能访问指定VPC。
-   2：数据从VPC内网传输，此时要求源服务器同时能访问公网和指定VPC。

 VPC内网迁云需要将`net_mode`设置为1或者2。|
|transition.vpc.vpc\_id|String|否|已经配置了高速通道服务或者VPN网关的VPC ID。当`net_mode=1`或`net_mode=2`时为必填参数。|
|transition.vswitch.vswitch\_id|String|否|指定VPC下的一台虚拟交换机ID。当`net_mode=1`或`net_mode=2`时为必填参数。|
|transition.security\_group.security\_group\_id|String|否|指定VPC下的安全组ID。|
|extra.net.proxy.ip\_port|String|否|指定网络代理服务IP及端口。格式为IP:Port，如“10.0.0.100:1080”。|
|extra.net.proxy.user\_pwd|String|否|指定网络代理服务用户名及密码。格式为User:Password，如“admin:123456”。|

更多详情，您可以[下载迁云工具](http://p2v-tools.oss-cn-hangzhou.aliyuncs.com/Alibaba_Cloud_Migration_Tool.zip?spm=a2c4g.11186623.2.8.6B6W0i&file=Alibaba_Cloud_Migration_Tool.zip)并查看client\_data文件。

## 源服务器不能访问公网方案 {#section_nww_qz1_kfb .section}

以下步骤适用于`net_mode=1`的情形。迁云工作会分成3个阶段，其中阶段1（`Stage 1`）和阶段3（`Stage 3`）在备用服务器中完成，需要备用服务器能访问公网；阶段2（`Stage 2`）数据传输在待迁移的源服务器中进行。

1.  登录一台您能够访问公网的服务器A，进行下列操作：
    1.  下载并安装迁云工具。详情请参见[步骤1：下载和安装迁云工具](cn.zh-CN/迁移服务/P2V 迁云工具/使用迁云工具迁移服务器至阿里云.md#section_twq_sxz_jfb)。
    2.  编辑迁云工具的client\_data文件：设置`net_mode=1`，填入已经配置了高速通道服务或者VPN网关的`vpc_id`、`vswitch_id`。
    3.  （可选）在client\_data文件中配置`security_group_id`参数，但安全组入方向必须放行代理端口8080和8703。更多详情，请参见[添加安全组规则](../../../../cn.zh-CN/安全/安全组/添加安全组规则.md#)。
    4.  按照[公网迁云](cn.zh-CN/迁移服务/P2V 迁云工具/使用迁云工具迁移服务器至阿里云.md#)步骤在服务器A内运行迁云工具，直到提示`Stage 1 Is Done!`。

        [![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733783688/Stage1.png)](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733783688/Stage1.png)

2.  登录您需要迁移的源服务器，并进行下列操作：
    1.  复制服务器A的迁云工具配置，包括user\_config.json、Rsync目录和client\_data文件，保持配置文件内容一致。
    2.  按照[公网迁云](cn.zh-CN/迁移服务/P2V 迁云工具/使用迁云工具迁移服务器至阿里云.md#)步骤在待迁移的源服务器内运行迁云工具，直到提示`Stage 2 Is Done!`。

        [![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733805431/Stage2.png)](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733805431/Stage2.png)

3.  重新登录服务器A，进行下列操作：
    1.  复制待迁移的源服务器的迁云工具配置，包括user\_config.json、Rsync目录和client\_data文件，必须保持配置文件内容一致。
    2.  按照[公网迁云](cn.zh-CN/迁移服务/P2V 迁云工具/使用迁云工具迁移服务器至阿里云.md#)步骤在服务器A内再次运行迁云工具，直到提示`Stage 3 Is Done!`，表示VPC内网迁云顺利完成。

        [![](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733837163/Stage3.png)](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/pic/74090/cn_zh/1531733837163/Stage3.png)


## 源服务器能访问公网方案 {#section_www_qz1_kfb .section}

以下步骤适用于`net_mode=2`的情形，操作过程与`net_mode=0`时，即公网迁云相同。`net_mode=2`时，数据自动从VPC迁移上云，其他过程走公网。

1.  登录到源服务器。
2.  下载并安装迁云工具。详情请参见[步骤1：下载和安装迁云工具](cn.zh-CN/迁移服务/P2V 迁云工具/使用迁云工具迁移服务器至阿里云.md#section_twq_sxz_jfb)。
3.  编辑迁云工具的client\_data文件。设置`net_mode=2`，填入已经配置了高速通道服务或者VPN网关的`vpc_id`、`vswitch_id`。
4.  （可选）在client\_data文件中配置`security_group_id`参数，但安全组入方向必须放行代理端口8080和8703。更多详情，请参见[添加安全组规则](../../../../cn.zh-CN/安全/安全组/添加安全组规则.md#)。
5.  按照[公网迁云](cn.zh-CN/迁移服务/P2V 迁云工具/使用迁云工具迁移服务器至阿里云.md#)步骤运行迁云工具。

## 源服务器能访问网络代理方案 {#section_c1f_ah3_mrn .section}

以下步骤适用于`net_mode=2`的情形，操作过程与`net_mode=0`时，即公网迁云相同。`net_mode=2`时，数据自动从VPC迁移上云，其他过程走局域网网络代理服务访问公网。

1.  登录到源服务器。
2.  下载并安装迁云工具。详情请参见[步骤1：下载和安装迁云工具](cn.zh-CN/迁移服务/P2V 迁云工具/使用迁云工具迁移服务器至阿里云.md#section_twq_sxz_jfb)。
3.  编辑迁云工具的client\_data文件，进行下列配置：
    1.  设置`net_mode=2`，填入已经配置了高速通道服务或者VPN网关的`vpc_id`、`vswitch_id`。
    2.  配置网络代理服务。在源服务器局域网中准备网络代理服务器，并填写下列配置信息：

        1.  将网络代理服务IP和端口填入`extra.net.proxy.ip_port`。
        2.  如果有用户名及密码则填入`extra.net.proxy.user_pwd`，没有则可以不填。
        **说明：** 参数值的具体格式请参见上文表格中`extra.net.proxy.ip_port`和`extra.net.proxy.user_pwd`的描述。

4.  （可选）在client\_data文件中配置`security_group_id`参数，但安全组入方向必须放行代理端口8080和8703。更多详情，请参见[添加安全组规则](../../../../cn.zh-CN/安全/安全组/添加安全组规则.md#)。
5.  按照[公网迁云](cn.zh-CN/迁移服务/P2V 迁云工具/使用迁云工具迁移服务器至阿里云.md#)步骤运行迁云工具。

如果迁云工作中断，您可以查看[迁云工具FAQ](cn.zh-CN/迁移服务/P2V 迁云工具/迁云工具FAQ.md#)，或者[添加迁云工具客户反馈钉钉群](https://h5.dingtalk.com/invite-page/index.html?spm=a2c4g.11186623.2.31.FEg99s&code=ca190154ff)联系ECS迁云技术支持。更多联系方式，请参见[联系我们](cn.zh-CN/迁移服务/P2V 迁云工具/联系我们.md#)。

