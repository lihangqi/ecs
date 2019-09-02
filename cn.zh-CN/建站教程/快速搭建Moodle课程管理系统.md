# 快速搭建Moodle课程管理系统 {#concept_htd_qfb_ffb .concept}

本文档介绍如何使用云市场的Moodle网络教学平台（CentOS 7.0 64位）快速搭建Moodle课程管理系统。Moodle是一个课程管理系统，采用PHP加MySQL方式运行的自由开源软件。世界各地教育工作者越来越喜欢使用Moodle为学生建立网上动态网站，可以根据需要随时调整界面、增减内容。

## 前提条件 {#section_khx_ghb_ffb .section}

-   您已经拥有一个阿里云账号。
-   如果您希望用户通过域名访问您的站点，您应该已经有一个已备案的域名。如果域名没有备案，您购买ECS实例后到[阿里云备案中心](https://beian.aliyun.com/)备案 。
-   您已经了解远程连接Linux实例的方法，具体操作请参见[使用用户名密码验证连接Linux实例](../cn.zh-CN/实例/连接实例/连接Linux实例/使用用户名密码验证连接Linux实例.md#)。假设您本地使用的是Windows操作系统，并使用[PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)远程连接Linux ECS实例。
-   添加安全组规则。具体操作，请参见[添加安全组规则](../cn.zh-CN/安全/安全组/添加安全组规则.md#)。
    -   SSH远程连接ECS实例：

        |网卡类型|规则方向|授权策略|协议类型|端口范围|授权类型|授权对象|优先级|
        |公网|入方向|允许|SSH\(22\)|22/22|地址段访问|0.0.0.0/0|1|

    -   HTTP访问Web服务器：

        |网卡类型|规则方向|授权策略|协议类型|端口范围|授权类型|授权对象|优先级|
        |公网|入方向|允许|HTTP\(80\)|80/80|地址段访问|0.0.0.0/0|1|

    -   允许使用FTP上传或下载文件：

        |网卡类型|规则方向|授权策略|协议类型|端口范围|授权类型|授权对象|优先级|
        |公网|入方向|允许|自定义 TCP|21/21|地址段访问|0.0.0.0/0|1|

    -   允许使用MySQL：

        |网卡类型|规则方向|授权策略|协议类型|端口范围|授权类型|授权对象|优先级|
        |公网|入方向|允许|自定义 TCP|3306/3306|地址段访问|0.0.0.0/0|1|


## 操作步骤 {#section_rj2_sdg_xgb .section}

1.  在云市场中搜索[moodle 网络教学平台（Centos 7.0 64位）](https://market.aliyun.com/products/56014009/cmjj012770.html)，并进入镜像详情页。
2.  在镜像详情页上，单击**立即购买**，按提示步骤购买ECS实例。需要注意以下配置：
    -   **带宽**：不能为0Mbps。
    -   **付费方式**：如果您的站点需要备案，应选择**包月套餐**。
    -   其他配置您可以按需选择。
3.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。
4.  在左侧导航栏，选择**实例与镜像** \> **实例**。
5.  选择所购ECS实例所在的地域，找到所购ECS实例，在**IP 地址**列获取该实例的公网 IP 地址。
6.  在浏览器地址栏里，输入Moodle的安装地址`http://公网 IP 地址/install.php`。
7.  选择您想要的语言，选择后单击**向后**。本示例中，选择**简体中文**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/156705206012545_zh-CN.png)

8.  在确认路径页面上，保持所有默认目录不变。单击**向后**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/156705206012546_zh-CN.png)

9.  在选择数据库驱动页面上，采用默认类型。单击**向后**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/156705206012547_zh-CN.png)

10. 连接Linux实例。具体操作，请参见[使用用户名密码验证连接Linux实例](../cn.zh-CN/实例/连接实例/连接Linux实例/使用用户名密码验证连接Linux实例.md#)。
11. 运行命令`cat default.pass`查看随机生成的数据库权限及FTP权限。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/156705206012544_zh-CN.png)

12. 在浏览器中设置数据库。其中：
    -   **数据库主机**：只能填`127.0.0.1`。
    -   **数据库名**、**数据用户名**和**数据库密码**采用上一步中查得的MySQL权限信息。
    -   **数据库服务端口**：填写3306。

        确认所有信息后，单击**向后**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/156705206012548_zh-CN.png)

13. 阅读并确认了解版权声明。单击**继续**。
14. 下图中显示的是安装Moodle需要的一些组件，都已经部署好了。单击**继续**就可以安装系统。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/156705206012549_zh-CN.png)

15. 当安装页面底部出现**继续**时，说明已经完成安装。单击**继续**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/156705206112550_zh-CN.png)

16. 按要求设置Moodle系统的登录信息后，单击**保存更改**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/156705206112551_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/156705206112552_zh-CN.png)

17. 安装完成，自动进入管理后台首页。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/156705206112553_zh-CN.png)

    **说明：** 数据库的管理地址为：`http://公网 IP 地址/phpmyadmin/`。

18. （可选）用户可以使用公网IP地址访问您的站点。如果您希望用户使用域名访问您的站点，应先将域名解析到公网IP地址。您可以按以下步骤在服务器里绑定域名：
    1.  远程连接Linux实例后，输入命 `vim /etc/httpd/conf/httpd.conf`打开配置文件，添加Servername命令。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/156705206112554_zh-CN.png)

    2.  将`localhost`改为`www.yourdomain.com`即可。其中，`www.yourdomain.com`必须替换为您自己的域名。
    3.  按下`Esc`键，然后输入`:wq`并回车以保存并关闭文件。

