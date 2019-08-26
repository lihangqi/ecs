# 快速搭建 Moodle 课程管理系统 {#concept_htd_qfb_ffb .concept}

Moodle 是一个开源课程管理系统，采用 PHP + MySQL 方式运行的自由开源软件，遵循 GNU 公共许可协议。世界各地教育工作者越来越喜欢使用 Moodle 为学生建立网上动态网站。Moodle 平台界面简单、精巧，您可以根据需要随时调整界面，增减内容。

本文档介绍如何使用云市场的 moodle **网络教学平台（Centos 7.0 64位）** 快速搭建 Moodle 课程管理系统。

## 适用对象 {#section_tqf_ghb_ffb .section}

适用于要搭建 Moodle 课程管理系统的用户。

## 操作流程 {#section_khx_ghb_ffb .section}

1.  创建使用 Moodle 网络教学平台镜像的 ECS 实例。
2.  远程连接 ECS 实例并查看权限。
3.  安装 Moodle 课程管理系统。
4.  （可选）在服务器里绑定域名。

**前提条件**

-   您已经拥有一个阿里云账号。
-   如果您希望用户通过域名访问您的站点，您应该已经有一个已备案的域名。如果域名没有备案，您购买ECS实例后到阿里云备案中心备案。备案地址为：[https://beian.aliyun.com](https://beian.aliyun.com/) 。
-   您已经明白 [远程连接 Linux 实例的方法](http://help.aliyun.com/document_detail/25434.html)。这里假设您本地使用的是 Windows 操作系统，并使用 PuTTy.exe 远程连接 Linux ECS 实例。这里是 PuTTY 的下载地址：[https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) 。

**创建 ECS 实例**

1.  在云市场中搜索 [moodle 网络教学平台（Centos 7.0 64位）](https://market.aliyun.com/products/56014009/cmjj012770.html)，并进入镜像详情页。
2.  在镜像详情页上，单击 **立即购买**，按提示步骤购买 ECS 实例。需要注意以下配置：
    -   **网络类型**：应选择 **经典网络**。
    -   **带宽**：不能为 0 Mbps。
    -   **付费方式**：如果您的站点需要备案，应选择 **包月套餐**。
    -   其他配置您可以按需选择。
3.  登录 [云服务器 ECS 管理控制台](https://ecs.console.aliyun.com/#/home)。
4.  在左侧导航栏里，单击 **实例**，进入 ECS 列表页。
5.  选择所购 ECS 实例所在的地域，找到所购 ECS 实例，开始管理实例。您需要做以下操作：
    -   在 **IP 地址** 列获取该实例的公网 IP 地址。
    -   确认 ECS 实例所在的安全组中 [已经添加了以下几个安全组规则](http://help.aliyun.com/document_detail/25471.html)：
        -   SSH 远程连接 ECS 实例：

            |网卡类型|规则方向|授权策略|协议类型|端口范围|授权类型|授权对象|优先级|
            |公网|入方向|允许|SSH\(22\)|22/22|地址段访问|0.0.0.0/0|1|

        -   HTTP 访问 Web 服务器：

            |网卡类型|规则方向|授权策略|协议类型|端口范围|授权类型|授权对象|优先级|
            |公网|入方向|允许|HTTP\(80\)|80/80|地址段访问|0.0.0.0/0|1|

        -   允许使用 FTP 上传或下载文件：

            |网卡类型|规则方向|授权策略|协议类型|端口范围|授权类型|授权对象|优先级|
            |公网|入方向|允许|自定义 TCP|20/21|地址段访问|0.0.0.0/0|1|

        -   允许使用 MySQL：

            |网卡类型|规则方向|授权策略|协议类型|端口范围|授权类型|授权对象|优先级|
            |公网|入方向|允许|自定义 TCP|3306/3306|地址段访问|0.0.0.0/0|1|

    -   使用 [重置实例密码](http://help.aliyun.com/document_detail/25439.html) 功能设置 ECS 实例的登录密码。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/154817578112543_zh-CN.png)


## 远程连接 ECS 实例并查看权限 {#section_rqq_j3b_ffb .section}

1.  [远程连接到 ECS 实例](http://help.aliyun.com/document_detail/25425.html)。
2.  运行命令 `cat default.pass` 查看随机生成的数据库权限及 FTP 权限。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/154817578112544_zh-CN.png)


**安装 Moodle 系统**

安装 Moodle 系统需要知道以下 2 个地址：

-   数据库的管理地址为：`http://您的公网 IP 地址/phpmyadmin/`。
-   Moodle 的安装地址为：`http://您的公网 IP 地址/install.php`。

按以下步骤安装 Moodle 系统：

1.  在浏览器地址栏里，输入 Moodle 的安装地址。
2.  选择您想要的语言，选择后单击 **向后**。本示例中，选择 **简体中文**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/154817578112545_zh-CN.png)

3.  在 确认路径 页面上，保持所有默认目录不变。单击 **向后**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/154817578112546_zh-CN.png)

4.  在 选择数据库驱动 页面上，采用默认类型。单击 **向后**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/154817578212547_zh-CN.png)

5.  设置数据库。其中：
    -   **数据库主机**：只能填 `127.0.0.1`。
    -   **数据库名**、**数据用户名** 和 **数据库密码** 采用上述步骤中查得的 MySQL 权限信息。
    -   **数据库服务端口**：填写 3306。

        确认所有信息后，单击 **向后**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/154817578212548_zh-CN.png)

6.  阅读并确认了解版权声明。单击 **继续**。
7.  下图中显示的是安装 Moodle 需要的一些组件，都已经部署好了。单击 **继续** 就可以安装系统。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/154817578212549_zh-CN.png)

8.  当安装页面底部出现 **继续** 时，说明已经完成安装。单击 **继续**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/154817578212550_zh-CN.png)

9.  按要求设置 Moodle 系统的登录信息后，单击 **保存更改**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/154817578212551_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/154817578212552_zh-CN.png)

10. 安装完成，自动进入管理后台首页。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/154817578212553_zh-CN.png)


**绑定域名**

用户可以使用公网 IP 地址访问您的站点。如果您希望用户使用域名访问您的站点，您应先将您的域名解析到公网 IP 地址。

如果需要在服务器里绑定域名，按以下步骤操作：

1.  远程连接 Linux 实例后，输入命令 `vim /etc/httpd/conf/httpd.conf` 打开配置文件，找到 Servername 选项。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9785/154817578212554_zh-CN.png)

2.  将 `localhost` 改为 `www.yourdomain.com` 即可。其中，`www.yourdomain.com` 必须替换为您自己的域名。

更多开源软件尽在云市场：[https://market.aliyun.com/software](https://market.aliyun.com/software)。

